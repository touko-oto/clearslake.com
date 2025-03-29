<template>
  <div>
    <Breadcrumb :breadcrumbsArray="breadcrumbsArray" />

    <section class="services-section">
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
        </div>
    </section>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  title: '湖 | 透明な湖',
  description: '世界中の湖を紹介するサイト。観光スポットの参考になれば幸いです。',
});

const route = useRoute();

const breadcrumbsArray = [
  {
    name: '湖',
    path: route.path
  }
]

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
</script>


<style lang="scss" scoped></style>