<template>
  <section class="relative w-full h-[85vh] overflow-hidden flex justify-start bg-gray-100 py-16 px-0">
    <div class="mv-area relative z-10 text-left max-w-1280 w-full mx-auto flex flex-col">
      <div class="max-md:text-3xl text-5xl font-bold mb-4 leading-tight">
        世界中の湖に関する情報を<br>手軽に閲覧</div>
      <p class="text-lg mb-8 leading-relaxed ">
        最新技術（Jamstack構成 + Nuxt3 + microCMS）で<br class="br-sp">本サイトを構築
      </p>
      <PrimaryButton to="/contact" label="お問い合わせする" />
    </div>
    <div class="absolute top-0 left-0 w-full h-full">
      <img src="~/assets/images/main-visual-sp.png" alt="Background" class="w-full md:hidden" />
      <img src="~/assets/images/main-visual.png" alt="Background" class="hidden md:block" />
    </div>
  </section>
</template>

<style lang="scss" scoped>
.mv-area {
  max-width: 1280px;
  width: 100%;
  margin: auto;
}

@media (max-width: 768px) {
  .mv-area {
    margin: 0 16px;
    align-self: end;
  }
}
</style>