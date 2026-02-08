<template>
  <article class="blog-card">
    <div class="card-image">
      <img :src="`https://picsum.photos/seed/${title}/600/400`" :alt="title">
      <span class="category-badge">{{ category }}</span>
    </div>

    <div class="card-content">
      <h2 class="post-title">{{ title }}</h2>
      <p class="excerpt">{{ excerpt }}</p>

      <div class="tags">
        <span v-for="tag in tags" :key="tag" class="tag">
          #{{ tag }}
        </span>
      </div>

      <div class="card-footer">
        <div class="author-info">
          <img :src="author.avatar" :alt="author.name" class="avatar">
          <div class="author-meta">
            <span class="author-name">{{ author.name }}</span>
            <span class="post-date">{{ formattedDate }}</span>
          </div>
        </div>
        <div class="reading-time">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"></circle><polyline points="12 6 12 12 16 14"></polyline></svg>
          {{ readingTime }} min read
        </div>
      </div>
    </div>
  </article>
</template>

<script setup>
import {computed} from 'vue'

const props = defineProps({
  title: {
    type: String,
    required: true
  },
  author: {
    type: Object,
    required: true,
    validator: (value) => {
      return value.name && value.avatar
    }
  },
  date: {
    type: String,
    required: true
  },
  excerpt: {
    type: String,
    default: 'No excerpt available'
  },
  category: {
    type: String,
    required: true,
    validator: (value) => {
      return ['Technology', 'Science', 'Arts', 'Business'].includes(value)
    }
  },
  tags: {
    type: Array,
    default: () => []
  }
})

const formattedDate = computed(() => {
  return new Date(props.date).toLocaleDateString('en-US', {
    year: 'numeric',
    month: 'short',
    day: 'numeric'
  })
})

const readingTime = computed(() => {
  const wordsPerMinute = 200
  const words = props.excerpt.split(' ').length
  return Math.ceil(words / wordsPerMinute)
})
</script>

<style scoped>
.blog-card {
  background: white;
  border-radius: 1rem;
  overflow: hidden;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  transition: all 0.3s ease;
  display: flex;
  flex-direction: column;
  height: 100%;
  border: 1px solid #f3f4f6;
}

.blog-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
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

.category-badge {
  position: absolute;
  top: 1rem;
  right: 1rem;
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(4px);
  color: #4f46e5;
  padding: 0.25rem 0.75rem;
  border-radius: 2rem;
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.025em;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card-content {
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.post-title {
  margin: 0 0 0.75rem 0;
  font-size: 1.25rem;
  font-weight: 700;
  color: #111827;
  line-height: 1.4;
}

.excerpt {
  color: #4b5563;
  font-size: 0.9375rem;
  line-height: 1.6;
  margin: 0 0 1.25rem 0;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tag {
  font-size: 0.75rem;
  color: #6366f1;
  background: #f5f3ff;
  padding: 0.125rem 0.5rem;
  border-radius: 0.375rem;
  font-weight: 500;
}

.card-footer {
  margin-top: auto;
  padding-top: 1.25rem;
  border-top: 1px solid #f3f4f6;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.author-info {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.avatar {
  width: 2.5rem;
  height: 2.5rem;
  border-radius: 50%;
  object-fit: cover;
  border: 2px solid #fff;
  box-shadow: 0 0 0 1px #e5e7eb;
}

.author-meta {
  display: flex;
  flex-direction: column;
}

.author-name {
  font-size: 0.875rem;
  font-weight: 600;
  color: #111827;
}

.post-date {
  font-size: 0.75rem;
  color: #6b7280;
}

.reading-time {
  display: flex;
  align-items: center;
  gap: 0.25rem;
  font-size: 0.75rem;
  color: #9ca3af;
}
</style>