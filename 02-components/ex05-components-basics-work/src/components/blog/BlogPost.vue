<template>
  <article class="blog-card">
    <div class="card-image">
      <img src="https://proedu.com/cdn/shop/articles/What-Is-Post-Processing-Fundamentals-Blog-PRO-EDU.jpg?v=1704899902&width=1500" alt="Image de post">
      <div class="card-date">8 Fév 2026</div>
    </div>
    <div class="card-content">
      <span class="card-category">Technologie</span>
      <h2 class="card-title">Titre du post</h2>
      <p class="card-description">Ceci est un court extrait du contenu du post pour donner envie de lire la suite...</p>
      
      <div class="card-footer">
        <div class="author-info">
          <div class="author-avatar">JD</div>
          <p class="author-name">Par John Doe</p>
        </div>
        <button class="btn-more">Voir plus</button>
      </div>
    </div>
  </article>
</template>

<script setup>
</script>

<style scoped>
.blog-card {
  background: white;
  border-radius: 1rem;
  overflow: hidden;
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  max-width: 400px;
  display: flex;
  flex-direction: column;
}

.blog-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
}

.card-image {
  position: relative;
  height: 200px;
  overflow: hidden;
}

.card-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.blog-card:hover .card-image img {
  transform: scale(1.05);
}

.card-date {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(255, 255, 255, 0.9);
  padding: 0.25rem 0.75rem;
  border-radius: 2rem;
  font-size: 0.75rem;
  font-weight: 600;
  color: #4f46e5;
  backdrop-filter: blur(4px);
}

.card-content {
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.card-category {
  font-size: 0.75rem;
  font-weight: 700;
  color: #4f46e5;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: 0.5rem;
}

.card-title {
  margin: 0 0 0.75rem 0;
  font-size: 1.25rem;
  font-weight: 700;
  color: #111827;
  line-height: 1.4;
}

.card-description {
  margin: 0 0 1.5rem 0;
  font-size: 0.95rem;
  color: #4b5563;
  line-height: 1.6;
}

.card-footer {
  margin-top: auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-top: 1rem;
  border-top: 1px solid #f3f4f6;
}

.author-info {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.author-avatar {
  width: 32px;
  height: 32px;
  background: #e5e7eb;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.75rem;
  font-weight: 600;
  color: #6b7280;
}

.author-name {
  margin: 0;
  font-size: 0.875rem;
  font-weight: 500;
  color: #374151;
}

.btn-more {
  background: transparent;
  border: 1px solid #e5e7eb;
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
  font-size: 0.875rem;
  font-weight: 600;
  color: #4b5563;
  cursor: pointer;
  transition: all 0.2s ease;
}

.btn-more:hover {
  background: #f9fafb;
  border-color: #d1d5db;
  color: #111827;
}
</style>