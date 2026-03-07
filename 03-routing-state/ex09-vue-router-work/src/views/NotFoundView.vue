<template>
  <div class="not-found">
    <h1>404</h1>
    <h2>Page Not Found</h2>
    <p>The page you're looking for doesn't exist.</p>
    <RouterLink to="/" class="home-btn">Go Home</RouterLink>
  </div>
</template>

<style scoped>
.not-found {
  text-align: center;
  padding: 100px 20px;
}

.not-found h1 {
  font-size: 120px;
  margin: 0;
  color: #42b883;
}

.home-btn {
  display: inline-block;
  margin-top: 20px;
  padding: 12px 24px;
  background: #42b883;
  color: white;
  text-decoration: none;
  border-radius: 4px;
}
</style>