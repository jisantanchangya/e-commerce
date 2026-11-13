<script setup>
defineOptions({ name: 'SiteFooter' })

const currentYear = new Date().getFullYear()
</script>

<template>
  <footer class="site-footer">
    <div class="footer-main">
      <div class="footer-brand">
        <a class="brand-name" href="/" aria-label="Niharika home">NIHARIKA</a>
        <p>
          Thoughtfully chosen styles for every day. Find your next favorite from our latest
          collections.
        </p>
        <a class="contact-link" href="mailto:info@ecommerce.com">info@ecommerce.com</a>
        <a class="contact-link" href="tel:+1234567890">+1 (234) 567-890</a>
      </div>

      <nav class="footer-column" aria-label="Shop">
        <h2>Shop</h2>
        <a href="#new-arrivals-title">New arrivals</a>
        <a href="#women-trending-title">Women</a>
        <a href="#men-trending-title">Men</a>
      </nav>

      <nav class="footer-column" aria-label="Customer care">
        <h2>Customer care</h2>
        <a href="mailto:info@ecommerce.com?subject=Order%20help">Order help</a>
        <a href="mailto:info@ecommerce.com?subject=Shipping%20question">Shipping</a>
        <a href="mailto:info@ecommerce.com?subject=Returns%20question">Returns</a>
      </nav>

      <div class="footer-column footer-note">
        <h2>Here to help</h2>
        <p>Have a question? Our team is happy to help you find what you need.</p>
        <a class="help-link" href="mailto:info@ecommerce.com">Get in touch <span aria-hidden="true">→</span></a>
      </div>
    </div>

    <div class="footer-bottom">
      <p>&copy; {{ currentYear }} Niharika. All rights reserved.</p>
      <a href="#app" class="back-to-top">Back to top <span aria-hidden="true">↑</span></a>
    </div>
  </footer>
</template>

<style scoped>
.site-footer {
  padding: 4rem max(2.25rem, calc((100% - 1350px) / 2)) 1.25rem;
  background: #202020;
  color: #f7f5f2;
  font-family: Arial, sans-serif;
}

.footer-main {
  display: grid;
  grid-template-columns: minmax(240px, 1.7fr) repeat(3, minmax(140px, 1fr));
  gap: 3rem;
  padding-bottom: 3rem;
}

.footer-brand {
  max-width: 340px;
}

.brand-name {
  display: inline-block;
  margin-bottom: 1rem;
  color: inherit;
  font-size: 1.55rem;
  font-weight: 700;
  letter-spacing: 0.14em;
  text-decoration: none;
}

.footer-brand p,
.footer-note p {
  margin: 0 0 1.25rem;
  color: #c1c1c1;
  font-size: 0.9rem;
  line-height: 1.7;
}

.contact-link,
.footer-column > a {
  display: block;
  width: fit-content;
  margin-top: 0.8rem;
  color: #c1c1c1;
  font-size: 0.88rem;
  text-decoration: none;
  transition: color 160ms ease;
}

.contact-link:hover,
.footer-column > a:hover,
.back-to-top:hover {
  color: #fff;
}

.footer-column h2 {
  margin: 0 0 1.2rem;
  color: #fff;
  font-size: 0.82rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}

.footer-note .help-link {
  color: #fff;
  font-weight: 600;
}

.help-link span {
  display: inline-block;
  margin-left: 0.35rem;
  transition: transform 160ms ease;
}

.help-link:hover span {
  transform: translateX(3px);
}

.footer-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  padding-top: 1.25rem;
  border-top: 1px solid #444;
}

.footer-bottom p {
  margin: 0;
  color: #aaa;
  font-size: 0.8rem;
}

.back-to-top {
  color: #c1c1c1;
  font-size: 0.8rem;
  text-decoration: none;
  transition: color 160ms ease;
}

.back-to-top span {
  margin-left: 0.35rem;
}

@media (max-width: 800px) {
  .footer-main {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 2.5rem 2rem;
  }
}

@media (max-width: 520px) {
  .site-footer {
    padding: 3rem 1.25rem 1rem;
  }

  .footer-main {
    grid-template-columns: 1fr 1fr;
    gap: 2rem 1rem;
  }

  .footer-brand {
    grid-column: 1 / -1;
  }

  .footer-bottom {
    align-items: flex-start;
    flex-direction: column;
  }
}
</style>
