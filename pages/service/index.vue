<template>
  <div>
    <Breadcrumb :breadcrumbsArray="breadcrumbsArray" />

    <section class="services-section">
      <div class="content service-content">
        <div class="service-header">
          <small>湖</small>
          <h1>Lake</h1>
        </div>
        <ul v-if="lakeList && lakeList.length" class="lake-list">
          <li v-for="lake in lakeList" :key="lake.id" class="lake-item">
            <NuxtLink :to="`/service/${lake.id}`" class="lake-link">
              <div class="lake-date">{{ formatDate(lake.publishedAt) }}</div>
              <div class="lake-continent">{{ lake.continent.name }}</div>
              <div class="lake-area">{{ lake.area.name }}</div>
              <div class="lake-country">{{ lake.country.name }}</div>
              <div class="lake-description">{{ lake.title }}</div>
            </NuxtLink>
          </li>
        </ul>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  title: '湖一覧 | 透明な湖',
  description: '世界中の湖を紹介するサイト。観光スポットの参考になれば幸いです。',
});

const route = useRoute();

const breadcrumbsArray = [
  {
    name: '湖一覧',
    path: route.path
  }
]

type Lake = {
  id: string;
  publishedAt: string;
  title: string;
  continent: {
    id: string;
    name: string
  };
  area: {
    id: string;
    name: string
  };
  country: {
    id: string;
    name: string
  };
};

// 日付フォーマット関数を作成
function formatDate(dateString: string): string {
  const date = new Date(dateString);
  return date.toLocaleDateString();
}

const { data: lakeList } = await useAsyncData('lakeList', async () => {
  const { data } = await useMicroCMSGetList<Lake>({
    endpoint: 'lake',
    queries: { fields: ['id', 'publishedAt', 'title', 'continent', 'area', 'country' ] },
  });

  return data.value?.contents || [];
});
</script>


<style lang="scss" scoped>
.servise-section .servise-content {
  gap: 0;
  flex-direction: column;
}
</style>