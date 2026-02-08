<template>
  <div class="app-container">
    <Header/>
    <main class="content">
      <section class="hero-section">
        <h2 class="section-title">Derniers Articles</h2>
        <p class="section-subtitle">Découvrez nos dernières publications sur la technologie et le design.</p>
      </section>

      <div class="blog-grid">
        <BlogPost v-for="post in arrayPosts" :key="post.title" v-bind="post" :title="post.title"
                  :description="post.description" :theme="post.theme" :author="post.author" :imgUrl="post.imgUrl"
                  :imgAlt="post.imgAlt"/>
      </div>
    </main>
    <Footer/>
  </div>
</template>

<script setup>
import Header from './components/layout/Header.vue'
import BlogPost from './components/blog/BlogPost.vue'
import Footer from './components/layout/Footer.vue'

const arrayPosts = [
  {
    title: 'BlogPost 1',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod, libero quis tincidunt tincidunt, elit sapien tincidunt sapien.',
    theme: 'Technologie',
    author: 'Aura Delabase',
    imgUrl: "https://static.vecteezy.com/ti/photos-gratuite/t2/8749777-green-computing-green-technology-green-it-rss-and-it-ethics-concept-photo.jpg",
    imgAlt: "Image Technologie"
  },
  {
    title: 'BlogPost 2',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod, libero quis tincidunt tincidunt, elit sapien tincidunt sapien.',
    theme: 'Informatique',
    author: 'Fabrice',
    imgUrl: "https://media.istockphoto.com/id/2156599809/fr/photo/voler-%C3%A0-travers-le-paysage-de-la-technologie-num%C3%A9rique-futuriste-bleu-luisant-fond-de.jpg?s=612x612&w=0&k=20&c=sBY0BQxJVchoUzEj22CxRlsjQBOVY1N3h5zSwWrG4wU=",
    imgAlt: "Image Informatique"
  },
  {
    title: 'BlogPost 3',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod, libero quis tincidunt tincidunt, elit sapien tincidunt sapien.',
    theme: 'Design',
    author: 'Josué Perrault Leto',
    imgUrl: "https://www.shutterstock.com/image-illustration/mesmerizing-3d-illustration-featuring-colorful-600nw-2556435201.jpg",
    imgAlt: "Image Design"
  },
  {
    title: 'BlogPost 4',
    description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed euismod, libero quis tincidunt tincidunt, elit sapien tincidunt sapien.',
    theme: 'Web',
    author: 'josué',
    imgUrl: "https://media.istockphoto.com/id/1503858430/fr/vectoriel/concept-de-d%C3%A9veloppement-de-logiciels-de-site-web-site-de-conception-web-et-application.jpg?s=612x612&w=0&k=20&c=61b8_QRpZYivL0W0VJuDBnifG1W0gNmv1Hdqta1AN4U=",
    imgAlt: "Image Web"
  },
]
</script>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: #f9fafb;
}

.app-container {
  min-height: 100vh;
}

.content {
  max-width: 1200px;
  margin: 2rem auto;
  padding: 0 2rem;
  font-family: 'Inter', sans-serif;
  color: #1f2937;
}

.hero-section {
  text-align: center;
  margin-bottom: 3rem;
}

.section-title {
  font-size: 2.25rem;
  font-weight: 800;
  color: #111827;
  margin-bottom: 0.5rem;
}

.section-subtitle {
  font-size: 1.125rem;
  color: #6b7280;
}

.blog-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 2rem;
  justify-items: center;
}

@media (max-width: 640px) {
  .section-title {
    font-size: 1.75rem;
  }

  .blog-grid {
    grid-template-columns: 1fr;
  }
}
</style>