<script setup lang="ts">
const route = useRoute()
const contentId = route.params.id.toString()

type Lake = {
  id: string,
  publishedAt: Date,
  title: string,
  continent: { id: string; name: string; };
  area: { id: string; name: string; };
  country: { id: string; name: string; };
  content: string;
}

// 日付フォーマット関数を作成
function formatDate(dateString: string): string {
  const date = new Date(dateString);
  return date.toLocaleDateString();
}

// `useAsyncData` を使用して SSR 時にデータを取得
const { data: lakeDetail } = await useAsyncData(`lakeDetail-${contentId}`, async () => {
  const { data } = await useMicroCMSGetListDetail<Lake>({
    endpoint: 'lake',
    contentId,
    queries: { fields: ['id', 'publishedAt', 'title', 'continent', 'area', 'country', 'content'] },
  });

  return data.value || null;
});

const breadcrumbsArray = [
  {
    name: '湖一覧',
    path: '/service'
  },
  {
    name: lakeDetail?.value?.title,
    path: route.path
  }
]

const description = lakeDetail.value?.content.replace(/<[^>]+>/g, '').slice(0, 150);

useHead({
  title: lakeDetail.value?.title,
  meta: [
    { name: 'description', content: description },
    { property: 'og:title', content: lakeDetail.value?.title },
    { property: 'og:description', content: description },
    //{ property: 'og:image', content: 'https://example.com/path/to/image.jpg' },
  ],
  link: [
    { rel: 'canonical', href: `https://clearslake.com/service/${contentId}` }
  ]
});
</script>

<template>
  <div>
    <Breadcrumb :breadcrumbsArray="breadcrumbsArray" />

    <div class="service-detail">
      <h1 class="service-title">{{ lakeDetail?.title }}</h1>
      <time class="service-date">{{ formatDate(lakeDetail?.publishedAt) }}</time>
      <div class="service-category">
        <ul class="lake-category">
          <li class="lake-category-item">{{ lakeDetail?.continent?.name }}</li>
          <li class="lake-category-item">{{ lakeDetail?.area?.name }}</li>
          <li class="lake-category-item">{{ lakeDetail?.country?.name }}</li>
        </ul>
      </div>
      <section class="service-content" v-html="lakeDetail?.content" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
/* 全体レイアウト */
.service-detail {
  max-width: 960px;
  /* コンテンツの最大幅を設定 */
  margin: 0 auto;
  /* 水平方向中央揃え */
  padding: 60px 60px;
  background-color: #fff;

  .service-title {
    font-size: 32px;
    font-weight: bold;
    margin-bottom: 10px;
    text-align: center;
    word-break: break-word;
  }

  .service-date {
    display: block;
    text-align: center;
    font-size: 14px;
    color: #999;
    margin-bottom: 10px;
  }

  .service-category {
    display: block;
    text-align: center;
    font-size: 14px ;
    margin-bottom: 10px;
    ul {
      display: flex;
      li {
        list-style: none;
        margin-left: 20px;
      }
    }
  }

  .service-content {
    font-size: 18px;
    line-height: 1.8;
    word-wrap: break-word;
    /* テキストの折り返し */
    overflow-wrap: break-word;


    p {
      margin-bottom: 20px;
    }

    img {
      max-width: 100%;
      /* 画像が親要素の幅を超えないように */
      height: auto;
      margin: 20px 0;
      border-radius: 8px;
      display: block;
    }

    h2,
    h3 {
      font-size: 28px;
      margin: 30px 0 10px;
      font-weight: bold;
    }

    ul {
      list-style: disc;
      padding-left: 20px;

      li {
        margin-bottom: 10px;
      }
    }
  }
}

@media (max-width: 768px) {
  .service-detail {
    padding: 60px 16px;
  }
}
</style>