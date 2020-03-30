<template>
  <div class="wrapper">
    <div class="container">
      <header class="header">
        <slot name="header" />
      </header>
      <section class="posts">
        <slot name="posts" />
      </section>
    </div>
  </div>
</template>

<style lang="scss">
.wrapper {
  width: 100%;
  overflow: hidden;
}
.container {
  width: 520px;
  position: relative;
  margin: 0 auto 50px;

  @media(min-width: 800px) {
    width: 750px;
  }
  @media(min-width: 1050px) {
    width: 1000px;
  }
}
.header {
  padding: 12px 10px 8px;
}
</style>
