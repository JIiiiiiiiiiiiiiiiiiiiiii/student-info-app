<script setup lang="ts">
import { ref } from 'vue'

const appTitle = ref('Student Information System')
</script>

<template>
  <header class="header">
    <div class="header-glow"></div>
    <div class="header-content">
      <div class="brand">
        <div class="logo">
          <div class="logo-ring"></div>
          <svg width="28" height="28" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M16 2L4 8V14C4 21 8.8 27.2 16 30C23.2 27.2 28 21 28 14V8L16 2Z" fill="currentColor" opacity="0.9"/>
            <circle cx="16" cy="14" r="4" fill="#0f172a"/>
            <path d="M16 20C12.69 20 10 20.9 10 22V24H22V22C22 20.9 19.31 20 16 20Z" fill="#0f172a"/>
          </svg>
        </div>
        <div class="brand-text">
          <h1>{{ appTitle }}</h1>
          <span class="subtitle">Academic Management Portal</span>
        </div>
      </div>
      <nav class="nav">
        <router-link to="/" class="nav-link">
          <span class="nav-icon">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
              <polyline points="9 22 9 12 15 12 15 22"></polyline>
            </svg>
          </span>
          Dashboard
          <span class="nav-indicator"></span>
        </router-link>
        <router-link to="/students" class="nav-link">
          <span class="nav-icon">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path>
              <circle cx="9" cy="7" r="4"></circle>
              <path d="M23 21v-2a4 4 0 0 0-3-3.87"></path>
              <path d="M16 3.13a4 4 0 0 1 0 7.75"></path>
            </svg>
          </span>
          Students
          <span class="nav-indicator"></span>
        </router-link>
      </nav>
    </div>
  </header>
</template>

<style scoped>
.header {
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  color: white;
  padding: 0;
  border-bottom: 1px solid #334155;
  position: relative;
  overflow: hidden;
}

.header-glow {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 2px;
  background: linear-gradient(90deg, transparent, #6366f1, #8b5cf6, #6366f1, transparent);
  background-size: 200% 100%;
  animation: glow 3s linear infinite;
}

@keyframes glow {
  0% {
    background-position: -200% 0;
  }
  100% {
    background-position: 200% 0;
  }
}

.header-content {
  max-width: 1600px;
  margin: 0 auto;
  padding: 1.5rem 2.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 2rem;
}

.brand {
  display: flex;
  align-items: center;
  gap: 1.25rem;
}

.logo {
  width: 56px;
  height: 56px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  border-radius: 14px;
  position: relative;
  box-shadow: 0 8px 20px -4px rgba(99, 102, 241, 0.5);
}

.logo-ring {
  position: absolute;
  inset: -4px;
  border: 2px solid rgba(99, 102, 241, 0.3);
  border-radius: 16px;
  animation: pulse-ring 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

@keyframes pulse-ring {
  0%, 100% {
    opacity: 0.3;
    transform: scale(1);
  }
  50% {
    opacity: 0.1;
    transform: scale(1.05);
  }
}

.logo svg {
  color: white;
  position: relative;
  z-index: 1;
}

.brand-text {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

h1 {
  margin: 0;
  font-size: 1.625rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  line-height: 1.2;
  background: linear-gradient(135deg, #f1f5f9 0%, #cbd5e1 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.subtitle {
  font-size: 0.875rem;
  color: #94a3b8;
  font-weight: 500;
  letter-spacing: 0.01em;
}

.nav {
  display: flex;
  gap: 0.75rem;
}

.nav-link {
  color: #cbd5e1;
  text-decoration: none;
  font-weight: 600;
  padding: 0.75rem 1.25rem;
  border-radius: 10px;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  background: rgba(51, 65, 85, 0.3);
  border: 1px solid #334155;
  display: flex;
  align-items: center;
  gap: 0.625rem;
  font-size: 0.938rem;
  position: relative;
  overflow: hidden;
}

.nav-link::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(99, 102, 241, 0.1) 0%, rgba(139, 92, 246, 0.1) 100%);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.nav-link:hover::before {
  opacity: 1;
}

.nav-icon {
  display: flex;
  align-items: center;
  opacity: 0.8;
  transition: all 0.3s ease;
}

.nav-indicator {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 2px;
  background: linear-gradient(90deg, #6366f1, #8b5cf6);
  transform: scaleX(0);
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.nav-link:hover {
  background: rgba(71, 85, 105, 0.3);
  border-color: #475569;
  transform: translateY(-2px);
  color: #f1f5f9;
  box-shadow: 0 4px 12px -2px rgba(0, 0, 0, 0.3);
}

.nav-link:hover .nav-icon {
  opacity: 1;
  transform: scale(1.1);
}

.nav-link.router-link-active {
  background: linear-gradient(135deg, rgba(99, 102, 241, 0.2) 0%, rgba(139, 92, 246, 0.2) 100%);
  border-color: rgba(99, 102, 241, 0.4);
  color: #f1f5f9;
  box-shadow: 0 0 0 1px rgba(99, 102, 241, 0.2);
}

.nav-link.router-link-active .nav-icon {
  opacity: 1;
  color: #a5b4fc;
}

.nav-link.router-link-active .nav-indicator {
  transform: scaleX(1);
}

@media (max-width: 768px) {
  .header-content {
    flex-direction: column;
    align-items: flex-start;
    padding: 1.25rem 1.5rem;
    gap: 1.5rem;
  }
  
  .brand {
    width: 100%;
  }
  
  h1 {
    font-size: 1.375rem;
  }
  
  .subtitle {
    font-size: 0.813rem;
  }
  
  .nav {
    width: 100%;
    flex-direction: column;
    gap: 0.625rem;
  }
  
  .nav-link {
    width: 100%;
    justify-content: flex-start;
  }
}
</style>