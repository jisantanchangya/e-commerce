<script setup>
import { Heart, MapPin, Search, ShoppingCart, User } from 'lucide-vue-next'
</script>

<template>
  <header class="site-header">
    <div class="navbar">
      <div class="brand-section">
        <router-link class="brand" to="/" aria-label="My App home">NIHARIKA</router-link>
      </div>

      <form class="search-form" role="search" @submit.prevent>
        <input
          type="search"
          name="q"
          aria-label="Search products"
          placeholder="Search products..."
        />
        <button type="submit" aria-label="Search">
          <Search aria-hidden="true" />
        </button>
      </form>

      <nav class="main-navigation" aria-label="Main navigation">
        <router-link class="sale-link" to="/">HOLIDAY SALE</router-link>
        <router-link to="/about">SHOP ALL</router-link>
        <router-link to="/contact">MEN</router-link>
        <router-link to="/login">WOMEN</router-link>
      </nav>

      <div class="utility-navigation" aria-label="Shopping and account links">
        <router-link class="utility-link" to="/login">
          <MapPin aria-hidden="true" />
          <span>Location</span>
        </router-link>
        <router-link class="utility-link" to="/login">
          <Heart aria-hidden="true" />
          <span>Wish List</span>
        </router-link>
        <router-link class="utility-link" to="/login">
          <ShoppingCart class="cart-icon" aria-hidden="true" />
          <span>Cart</span>
        </router-link>
        <router-link class="utility-link" to="/login">
          <User aria-hidden="true" />
          <span>Login</span>
        </router-link>
      </div>
    </div>
  </header>
</template>

<style scoped>
.site-header {
  position: sticky;
  top: 0;
  z-index: 20;
  border-bottom: 1px solid #e8e8e8;
  background: #fff;
}

.navbar {
  display: grid;
  grid-template-columns: auto minmax(140px, 220px) auto auto;
  align-items: center;
  gap: 2.5rem;
  max-width: 1440px;
  min-height: 76px;
  margin: 0 auto;
  padding: 1.3rem 2.25rem;
  color: #202020;
  font-family: Arial, sans-serif;
}

.brand {
  color: inherit;
  font-size: 1.5rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-decoration: none;
  white-space: nowrap;
}

.search-form {
  display: flex;
  align-items: center;
  min-width: 0;
  height: 42px;
  border: 1px solid #d8d8d8;
  border-radius: 20px;
  background: #fafafa;
  transition: border-color 160ms ease, box-shadow 160ms ease;
}

.search-form:focus-within {
  border-color: #555;
  box-shadow: 0 0 0 2px rgb(32 32 32 / 8%);
}

.search-form input {
  width: 100%;
  min-width: 0;
  padding: 0 0.85rem;
  border: 0;
  outline: 0;
  background: transparent;
  color: inherit;
  font: inherit;
  font-size: 0.82rem;
}

.search-form input::placeholder {
  color: #777;
}

.search-form button {
  display: grid;
  flex: 0 0 42px;
  place-items: center;
  height: 100%;
  border: 0;
  background: transparent;
  color: inherit;
  cursor: pointer;
}

.search-form button :deep(svg) {
  width: 18px;
  height: 18px;
  stroke-width: 1.8;
}

.main-navigation,
.utility-navigation {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.main-navigation {
  gap: 2rem;
}

.main-navigation a,
.utility-link {
  color: inherit;
  font-size: 0.78rem;
  font-weight: 600;
  letter-spacing: 0.04em;
  text-decoration: none;
  transition: color 160ms ease;
}

.main-navigation a:hover,
.utility-link:hover {
  color: #777;
}

.main-navigation .sale-link {
  color: #b42318;
}

.utility-navigation {
  justify-content: flex-end;
  gap: 2rem;
}

.utility-link {
  display: inline-flex;
  flex-direction: column;
  align-items: center;
  gap: 0.55rem;
  white-space: nowrap;
}

.utility-link :deep(svg) {
  width: 22px;
  height: 22px;
  stroke-width: 1.7;
}

.utility-link :deep(.cart-icon) {
  width: 22px;
  height: 22px;
}

@media (max-width: 960px) {
  .navbar {
    grid-template-columns: auto 1fr;
    gap: 1rem;
    padding: 1rem 1.25rem;
  }

  .search-form {
    grid-column: 2;
  }

  .main-navigation {
    grid-column: 1 / -1;
    justify-content: center;
    gap: 1rem;
  }

  .utility-navigation {
    grid-column: 1 / -1;
    justify-content: center;
  }
}

@media (max-width: 600px) {
  .navbar {
    grid-template-columns: 1fr;
    justify-items: center;
    gap: 1rem;
  }

  .search-form {
    grid-column: 1;
    width: 100%;
  }

  .main-navigation {
    width: 100%;
    justify-content: center;
    flex-wrap: wrap;
    gap: 0.75rem 1rem;
  }

  .main-navigation a,
  .utility-link {
    font-size: 0.7rem;
  }

  .utility-navigation {
    width: 100%;
    justify-content: space-between;
    gap: 2rem;
  }

}
</style>
