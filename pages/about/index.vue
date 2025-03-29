<template>
  <div>
    <Breadcrumb :breadcrumbsArray="breadcrumbsArray" />

    <section class="about-us-section">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">私たちについて</small>
          <h2>About us</h2>
          <p>卓越したITスキル<br class="br-sp">世界中の湖の関する情報を収集しまとめます。</p>
        </div>
        <div class="content-column-right">
          <img src="~/assets/images/about-us.jpg" alt="About us" />
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  title: '私たちについて | 透明な湖',
  description: '私たちについての情報をご紹介します。世界中の湖を紹介する総合サイト。海外旅行の観光スポットの参考になれば幸いです。',
});

const route = useRoute();

const breadcrumbsArray = [
  {
    name: '私たちについて',
    path: route.path
  }
]
</script>


<style lang="scss" scoped></style>