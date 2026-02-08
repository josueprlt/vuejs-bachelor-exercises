<template>
  <footer class="footer">
    <div class="footer-container">
      <div class="footer-top">
        <div class="footer-brand">
          <h2 class="footer-logo">Blog<span>Site</span></h2>
          <p class="footer-description">The best site in the world</p>
        </div>
        
        <div class="footer-socials">
          <a href="#" class="social-link" aria-label="Facebook">
            <img src="https://upload.wikimedia.org/wikipedia/commons/6/6c/Facebook_Logo_2023.png" alt="Facebook">
          </a>
          <a href="#" class="social-link" aria-label="Twitter">
            <img src="https://cdn-icons-png.flaticon.com/512/145/145812.png" alt="Twitter">
          </a>
          <a href="#" class="social-link" aria-label="Instagram">
            <img src="https://upload.wikimedia.org/wikipedia/commons/a/a5/Instagram_icon.png" alt="Instagram">
          </a>
          <a href="#" class="social-link" aria-label="Youtube">
            <img src="https://upload.wikimedia.org/wikipedia/commons/e/ef/Youtube_logo.png" alt="Youtube">
          </a>
        </div>
      </div>

      <div class="footer-divider"></div>

      <div class="footer-bottom">
        <nav class="footer-links">
          <a href="#">Privacy Policy</a>
          <a href="#">Terms of Use</a>
          <a href="#">Privacy Rights</a>
          <a href="#">Ads</a>
          <a href="#">Do Not Sell My Info</a>
        </nav>
        <p class="footer-copyright">
          &copy; 1996 - 2026 BlogSite®. All rights reserved.
        </p>
      </div>
    </div>
  </footer>
</template>

<script setup>
</script>

<style scoped>
.footer {
  background-color: #ffffff;
  padding: 4rem 0 2rem 0;
  border-top: 1px solid #f3f4f6;
  font-family: 'Inter', sans-serif;
  color: #4b5563;
}

.footer-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.footer-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 3rem;
  flex-wrap: wrap;
  gap: 2rem;
}

.footer-logo {
  margin: 0 0 0.5rem 0;
  font-size: 1.5rem;
  font-weight: 800;
  color: #111827;
  letter-spacing: -0.025em;
}

.footer-logo span {
  color: #4f46e5;
}

.footer-description {
  margin: 0;
  font-size: 0.95rem;
  max-width: 300px;
  line-height: 1.5;
}

.footer-socials {
  display: flex;
  gap: 1.25rem;
}

.social-link {
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background: #f9fafb;
  transition: all 0.2s ease;
}

.social-link img {
  width: 20px;
  height: 20px;
  object-fit: contain;
  opacity: 0.7;
  transition: opacity 0.2s ease;
}

.social-link:hover {
  background: #eef2ff;
  transform: translateY(-2px);
}

.social-link:hover img {
  opacity: 1;
}

.footer-divider {
  height: 1px;
  background-color: #f3f4f6;
  margin-bottom: 2rem;
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1.5rem;
}

.footer-links {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.footer-links a {
  text-decoration: none;
  color: #6b7280;
  font-size: 0.875rem;
  font-weight: 500;
  transition: color 0.2s ease;
}

.footer-links a:hover {
  color: #4f46e5;
}

.footer-copyright {
  margin: 0;
  font-size: 0.875rem;
  color: #9ca3af;
}

@media (max-width: 768px) {
  .footer-top {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .footer-bottom {
    flex-direction: column;
    text-align: center;
  }

  .footer-links {
    justify-content: center;
  }
}
</style>