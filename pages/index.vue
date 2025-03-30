<template>
  <div>
    <!-- メインビジュアル -->
    <MainVisual />

    <!-- About us セクション -->
    <section class="about-us-section px-0 py-16 md:py-32">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">私たちについて</small>
          <h2>About us</h2>
          <p>世界中の湖を紹介するサイト。<br class="br-sp">観光スポットの参考になれば幸いです。</p>
          <SecondaryButton to="/about" label="もっと見る" class="justify-start mr-auto" />
        </div>
        <div class="content-column-right">
          <img src="~/assets/images/about-us.png" alt="About us" />
        </div>
      </div>
    </section>

    <!-- 事業内容セクション -->
    <section class="services-section px-0 py-16 md:py-32">
      <div class="content">
        <small>湖</small>
        <h2>Lake</h2>
        <p>世界中の湖の場所と写真を提供します。</p>
        <div class="services-grid">
          <div class="service-card" v-for="(service, index) in services" :key="index">
            <div class="service-text">
              <div class="service-number">{{ index < 10 ? '0' + (index + 1) : index + 1 }}</div>
                  <div class="service-title">{{ service.title }}</div>
                  <p class="service-description">{{ service.description }}</p>
              </div>
            </div>
          </div>
          <SecondaryButton to="/service" label="もっと見る" class="mt-4 justify-end ml-auto" />
        </div>
    </section>

    <!-- お知らせ一覧 -->
    <section class="news-section px-0 py-16 md:py-32">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">お知らせ</small>
          <h2>News</h2>
        </div>
        <div class="content-column-right">
          <ul v-if="newsList && newsList.length" class="news-list">
            <li v-for="news in limitedNewsList" :key="news.id" class="news-item">
              <NuxtLink :to="`/news/${news.id}`">
                <div class="news-date">{{ formatDate(news.publishedAt) }}</div>
                <div class="news-description">{{ news.title }}</div>
              </NuxtLink>
            </li>
          </ul>
          <SecondaryButton to="/news" label="もっと見る" class="mt-4 justify-end ml-auto" />
        </div>
      </div>
    </section>

    <!-- 会社概要 -->
    <section class="company-info-section py-16 md:py-32">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">運営者</small>
          <h2>Profile</h2>
        </div>
        <div class="content-column-right">
          <table>
            <tbody>
              <tr>
                <th>名前</th>
                <td>透湖</td>
              </tr>
              <tr>
                <th>詳細プロフィール</th>
                <td><a href="https://www.clear-lake.net/">https://www.clear-lake.net/</a></td>
              </tr>
              <tr>
                <th>サイト設立日</th>
                <td>2025年4月1日</td>
              </tr>
            </tbody>
          </table>
          <SecondaryButton to="/info" label="もっと見る" class="mt-4 justify-end ml-auto" />
        </div>
      </div>
    </section>

    <!-- お問い合わせ -->
    <section class="contact-section px-0 py-16 md:py-32 bg-[#3A4354] text-white">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">お問い合わせ</small>
          <h2>Contact</h2>
        </div>
        <div class="content-column-right">
          <p>
            追加してほしい湖について、<br class="br-sp">お気軽にご相談ください。
          </p>
          <div>
            <PrimaryButton to="/contact" label="お問い合わせする" />
          </div>
        </div>
      </div>
    </section>

  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: 'top',
  title: '透明な湖',
  description: '世界中の湖を紹介する総合サイト。旅行時の観光スポットの参考になれば幸いです。',
});
type Service = {
  title: string;
  description: string;
};

const services: Service[] = [
  { title: 'ユーラシア大陸', description: 'アジア圏、オセアニア、ヨーロッパ' },
  { title: 'アフリカ大陸', description: 'エジプト、ナイジェリア、スーダンなど' },
  { title: '北アメリカ大陸', description: 'カナダ、アメリカ合衆国、メキシコなど' },
  { title: '南アメリカ大陸', description: 'アルゼンチン、ブラジル、チリなど' },
  { title: 'オーストラリア大陸', description: 'オーストラリア' },
  { title: '日本', description: '日本国内' }
];

type News = {
  id: string;
  publishedAt: string;
  title: string;
};

// 日付フォーマット関数を作成
function formatDate(dateString: string): string {
  const date = new Date(dateString);
  return date.toLocaleDateString();
}

const { data: newsList } = await useAsyncData('newsList', async () => {
  const { data } = await useMicroCMSGetList<News>({
    endpoint: 'news',
    queries: { fields: ['id', 'publishedAt', 'title'] },
  });

  return data.value?.contents || [];
});

const limitedNewsList = computed(() => {
  return newsList.value?.slice(0, 3) || [];
});
</script>

<style lang="scss" scoped>
section:nth-of-type(odd) {
  background-color: #f8f8f8;
}

section:nth-of-type(even) {
  background-color: #fff;
}

section:last-of-type {
  background-color: #3A4354;
}
</style>