<template>
  <div>
    <div class="header">
      <h2 class="header_title">Сеанс гемодиализа</h2>

      <h2 class="header_subtitle">
        № месяца:
        <span class="month">{{ new Date().getMonth() + 1 }}</span>
      </h2>
    </div>
  </div>
</template>
<style>
.header {
  margin-bottom: 50px;
}
.header_title,
.header_subtitle {
  display: inline-block;
  font-weight: 400;
  font-size: 22px;
}
.header_title {
  margin-right: 400px;
}
</style>
