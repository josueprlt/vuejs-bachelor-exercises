<template>
  <header class="header">
    <nav class="nav-container">
      <div class="logo-section">
        <h1 class="site-title">Blog<span>Site</span></h1>
        <p class="site-tagline">The best site in the world</p>
      </div>
      <div class="nav-actions">
        <button class="btn-join">Join us</button>
      </div>
    </nav>
  </header>
</template>

<script setup>
</script>

<style scoped>
:host {
  --primary-color: #4f46e5;
  --primary-hover: #4338ca;
  --text-main: #1f2937;
  --text-muted: #6b7280;
  --bg-white: #ffffff;
  --shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
}

.header {
  background-color: white;
  box-shadow: 0 1px 3px 0 rgb(0 0 0 / 0.1), 0 1px 2px -1px rgb(0 0 0 / 0.1);
  padding: 1rem 2rem;
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo-section {
  display: flex;
  flex-direction: column;
}

.site-title {
  margin: 0;
  font-size: 1.5rem;
  font-weight: 800;
  color: #111827;
  letter-spacing: -0.025em;
}

.site-title span {
  color: #4f46e5;
}

.site-tagline {
  margin: 0;
  font-size: 0.875rem;
  color: #6b7280;
}

.btn-join {
  background-color: #4f46e5;
  color: white;
  border: none;
  padding: 0.625rem 1.25rem;
  font-size: 0.875rem;
  font-weight: 600;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: all 0.2s ease;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
}

.btn-join:hover {
  background-color: #4338ca;
  transform: translateY(-1px);
}

.btn-join:active {
  transform: translateY(0);
}

@media (max-width: 640px) {
  .header {
    padding: 1rem;
  }
  
  .site-title {
    font-size: 1.25rem;
  }
  
  .site-tagline {
    display: none;
  }
}
</style>