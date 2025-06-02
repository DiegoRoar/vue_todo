<template>
  <footer class="footer">
    <div class="footer-content">
      <div class="footer-info">
        <p class="developer">
          Developed by <a href="https://dheroroarweb.com" target="_blank" rel="noopener" class="developer-link">DiegoRoar</a>
        </p>
        <p class="copyright">
          © {{ new Date().getFullYear() }} All rights reserved
        </p>
      </div>
      <div class="footer-links">
        <a href="https://dheroroarweb.com" target="_blank" rel="noopener" class="footer-link">
          <span class="link-icon">🌐</span>
          dheroroarweb.com
        </a>
        <a href="https://github.com/DiegoRoar" target="_blank" rel="noopener" class="footer-link">
          <span class="link-icon">📦</span>
          GitHub
        </a>
        <a href="https://ko-fi.com/diegoroar" target="_blank" rel="noopener" class="footer-link ko-fi">
          <span class="link-icon">☕</span>
          Buy me a coffee
        </a>
      </div>
    </div>
  </footer>
</template>

<script lang="ts" setup>
// No props or logic needed for now
</script>

<style scoped>
.footer {
  margin-top: var(--spacing-2xl);
  padding: var(--spacing-xl) 0;
  border-top: 1px solid var(--border-color);
  background: var(--secondary-color);
  position: relative;
  overflow: hidden;
}

.footer::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent,
    var(--accent-color),
    transparent
  );
  opacity: 0.5;
}

.footer-content {
  max-width: var(--content-max-width);
  margin: 0 auto;
  padding: 0 var(--spacing-lg);
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: var(--spacing-lg);
  position: relative;
  z-index: 1;
}

.footer-info {
  display: flex;
  flex-direction: column;
  gap: var(--spacing-sm);
}

.developer {
  font-size: var(--text-base);
  color: var(--text-color);
  font-weight: 500;
}

.developer-link {
  color: var(--accent-color);
  text-decoration: none;
  transition: color var(--transition-fast);
  font-weight: 600;
}

.developer-link:hover {
  color: var(--accent-hover);
  text-decoration: underline;
}

.copyright {
  font-size: var(--text-sm);
  color: var(--text-muted);
}

.footer-links {
  display: flex;
  gap: var(--spacing-lg);
  align-items: center;
}

.footer-link {
  color: var(--text-muted);
  text-decoration: none;
  font-size: var(--text-sm);
  transition: all var(--transition-fast);
  display: flex;
  align-items: center;
  gap: var(--spacing-xs);
  padding: var(--spacing-xs) var(--spacing-sm);
  border-radius: var(--radius-sm);
  background: transparent;
}

.footer-link:hover {
  color: var(--accent-color);
  background: rgba(0, 113, 255, 0.1);
  transform: translateY(-1px);
}

.link-icon {
  font-size: var(--text-base);
}

.ko-fi {
  background: linear-gradient(45deg, #ff5e5b, #ff8e8c);
  color: white;
  font-weight: 500;
  padding: var(--spacing-xs) var(--spacing-md);
  border-radius: var(--radius-sm);
  box-shadow: 0 2px 8px rgba(255, 94, 91, 0.2);
}

.ko-fi:hover {
  background: linear-gradient(45deg, #ff8e8c, #ff5e5b);
  color: white;
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(255, 94, 91, 0.3);
}

@media (max-width: 768px) {
  .footer-content {
    flex-direction: column;
    text-align: center;
    gap: var(--spacing-xl);
  }

  .footer-info {
    align-items: center;
  }

  .footer-links {
    flex-direction: column;
    gap: var(--spacing-md);
    width: 100%;
  }

  .footer-link {
    width: 100%;
    justify-content: center;
    padding: var(--spacing-sm);
  }

  .ko-fi {
    margin-top: var(--spacing-sm);
  }
}

@media (max-width: 480px) {
  .footer {
    padding: var(--spacing-lg) 0;
  }

  .footer-content {
    padding: 0 var(--spacing-md);
  }
}
</style> 