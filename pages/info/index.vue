<template>
  <div>
    <Breadcrumb :breadcrumbsArray="breadcrumbsArray" />

    <section class="company-info-section">
      <div class="content columns">
        <div class="content-column-left">
          <small class="ml-[0.2em]">運営情報</small>
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
        </div>
      </div>
    </section>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  title: '運営情報 | 透明な湖',
  description: '運営情報をご紹介します。世界中の湖を紹介する総合サイト。海外旅行の観光スポットの参考になれば幸いです。',
});

const route = useRoute();

const breadcrumbsArray = [
  {
    name: '運営情報',
    path: route.path
  }
]
</script>


<style lang="scss" scoped></style>