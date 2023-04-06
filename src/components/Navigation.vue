<template>
  <div class="navigation">
    <div class="container">
      <nav>
        <a>Каталог</a>
        <a>Доставка</a>
        <a>Оплата</a>
        <a>Контакты</a>
        <a>О компании</a>
      </nav>
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: "Navigation"
}
</script>

<style scoped>

</style>
