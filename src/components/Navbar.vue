<template>
  <nav class="main-nav">
    <Breadcrumb>
      <BreadcrumbItem :to="{ name: 'Home' }">
        <Icon type="ios-home-outline" /> Project
      </BreadcrumbItem>
      <BreadcrumbItem :to="{ name: 'AddProject' }">
        <Icon type="logo-buffer" /> Add a new Project
      </BreadcrumbItem>
    </Breadcrumb>
  </nav>
</template>

<style>
.main-nav {
  text-align: center;
  margin: 40px auto;
}
.main-nav a {
  display: inline-block;
  text-decoration: none;
  margin: 0 10px;
  color: #999;
  font-size: 18px;
}
a.router-link-active {
  border-bottom: 2px solid #00ce89;
  padding-bottom: 4px;
}
</style>