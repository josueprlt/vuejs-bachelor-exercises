<template>
  <div class="app">
    <Header/>

    <div class="hero">
      <h1 class="hero-title">Welcome to Our Blog</h1>
      <p class="hero-subtitle">Discover amazing stories from our community of writers.</p>
    </div>

    <div class="main-layout">
      <main class="blog-container">
        <BlogPost
            v-for="post in blogPosts"
            :key="post.id"
            :title="post.title"
            :author="post.author"
            :date="post.date"
            :excerpt="post.excerpt"
            :category="post.category"
            :tags="post.tags"
        />
      </main>

      <aside class="sidebar">
        <div class="sidebar-section">
          <h3 class="sidebar-title">Featured Authors</h3>
          <div class="authors-list">
            <UserCard
                v-for="user in authors"
                :key="user.id"
                :user="user"
                :show-bio="true"
                size="small"
            />
          </div>
        </div>

        <div class="sidebar-section">
          <h3 class="sidebar-title">Categories</h3>
          <div class="category-list">
            <span class="category-item">Technology</span>
            <span class="category-item">Science</span>
            <span class="category-item">Arts</span>
            <span class="category-item">Business</span>
          </div>
        </div>
      </aside>
    </div>

    <Footer/>
  </div>
</template>

<script setup>
import {ref} from 'vue'
import Header from './components/layout/Header.vue'
import Footer from './components/layout/Footer.vue'
import BlogPost from './components/blog/BlogPost.vue'
import UserCard from './components/UserCard.vue'

const blogPosts = ref([
  {
    id: 1,
    title: 'Getting Started with Vue.js',
    author: {
      name: 'Jane Doe',
      avatar: 'https://i.pravatar.cc/150?img=1'
    },
    date: '2026-01-20',
    excerpt: 'Learn the basics of Vue.js and build your first application from scratch. We cover components, reactivity, and more...',
    category: 'Technology',
    tags: ['Vue.js', 'JavaScript', 'Tutorial']
  },
  {
    id: 2,
    title: 'Understanding Component Props',
    author: {
      name: 'John Smith',
      avatar: 'https://i.pravatar.cc/150?img=2'
    },
    date: '2026-01-22',
    excerpt: 'Deep dive into Vue component props and how to use them effectively to build scalable applications...',
    category: 'Technology',
    tags: ['Vue.js', 'Components', 'Props']
  },
  {
    id: 3,
    title: 'The Future of Web Design',
    author: {
      name: 'Jane Doe',
      avatar: 'https://i.pravatar.cc/150?img=1'
    },
    date: '2026-01-25',
    excerpt: 'Exploring the latest trends in web design, from minimal interfaces to complex animations and AI-driven layouts...',
    category: 'Arts',
    tags: ['Design', 'UI/UX', 'Trends']
  }
])

const authors = ref([
  {
    id: 1,
    name: 'Jane Doe',
    email: 'jane@example.com',
    avatar: 'https://i.pravatar.cc/150?img=1',
    bio: 'Vue.js enthusiast and senior frontend developer'
  },
  {
    id: 2,
    name: 'John Smith',
    email: 'john@example.com',
    avatar: 'https://i.pravatar.cc/150?img=2',
    bio: 'Frontend developer specializing in Vue and UI Design'
  }
])
</script>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: #f9fafb;
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  color: #1f2937;
}
</style>

<style scoped>
.app {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.hero {
  background: white;
  padding: 4rem 2rem;
  text-align: center;
  border-bottom: 1px solid #f3f4f6;
}

.hero-title {
  font-size: 3rem;
  font-weight: 800;
  color: #111827;
  margin: 0 0 1rem 0;
  letter-spacing: -0.025em;
}

.hero-subtitle {
  font-size: 1.25rem;
  color: #6b7280;
  max-width: 600px;
  margin: 0 auto;
}

.main-layout {
  max-width: 1200px;
  margin: 3rem auto;
  padding: 0 2rem;
  display: grid;
  grid-template-columns: 1fr 300px;
  gap: 3rem;
  width: 100%;
  box-sizing: border-box;
}

.blog-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 2rem;
}

.sidebar {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

.sidebar-title {
  font-size: 1.125rem;
  font-weight: 700;
  color: #111827;
  margin: 0 0 1.25rem 0;
  padding-bottom: 0.75rem;
  border-bottom: 2px solid #f3f4f6;
}

.authors-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.category-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.category-item {
  padding: 0.5rem 1rem;
  background: white;
  border: 1px solid #e5e7eb;
  border-radius: 0.5rem;
  font-size: 0.875rem;
  font-weight: 500;
  color: #4b5563;
  cursor: pointer;
  transition: all 0.2s ease;
}

.category-item:hover {
  border-color: #4f46e5;
  color: #4f46e5;
  background: #f5f3ff;
}

@media (max-width: 1024px) {
  .main-layout {
    grid-template-columns: 1fr;
  }
  
  .sidebar {
    order: -1;
  }
}

@media (max-width: 640px) {
  .hero-title {
    font-size: 2.25rem;
  }
  
  .main-layout {
    margin: 1.5rem auto;
    padding: 0 1rem;
  }
  
  .blog-container {
    grid-template-columns: 1fr;
  }
}
</style>