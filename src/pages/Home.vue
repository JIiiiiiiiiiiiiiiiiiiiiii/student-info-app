<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const totalStudents = ref(150)
const activeCourses = ref(12)

const navigateToStudents = () => {
  router.push('/students')
}
</script>

<template>
  <div class="home">
    <div class="hero">
      <div class="hero-glow"></div>
      <div class="hero-content">
        <h2>Academic Management Dashboard</h2>
        <p class="subtitle">Comprehensive student information and records management system with real-time analytics</p>
      </div>
    </div>

    <div class="stats-section">
      <h3 class="section-title">
        <span class="title-icon">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <polyline points="22 12 18 12 15 21 9 3 6 12 2 12"></polyline>
          </svg>
        </span>
        System Overview
      </h3>
      <div class="stats-grid">
        <div class="stat-card">
          <div class="stat-header">
            <div class="stat-icon students">
              <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path>
                <circle cx="9" cy="7" r="4"></circle>
                <path d="M23 21v-2a4 4 0 0 0-3-3.87"></path>
                <path d="M16 3.13a4 4 0 0 1 0 7.75"></path>
              </svg>
            </div>
            <span class="stat-trend positive">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polyline points="23 6 13.5 15.5 8.5 10.5 1 18"></polyline>
                <polyline points="17 6 23 6 23 12"></polyline>
              </svg>
              +12%
            </span>
          </div>
          <div class="stat-value">{{ totalStudents }}</div>
          <div class="stat-label">Total Students</div>
          <div class="stat-footer">
            <span class="stat-subtext">From last semester</span>
          </div>
        </div>

        <div class="stat-card">
          <div class="stat-header">
            <div class="stat-icon courses">
              <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"></path>
                <path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"></path>
              </svg>
            </div>
            <span class="stat-trend neutral">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <circle cx="12" cy="12" r="10"></circle>
                <line x1="12" y1="8" x2="12" y2="16"></line>
                <line x1="8" y1="12" x2="16" y2="12"></line>
              </svg>
              4 programs
            </span>
          </div>
          <div class="stat-value">{{ activeCourses }}</div>
          <div class="stat-label">Active Courses</div>
          <div class="stat-footer">
            <span class="stat-subtext">Across departments</span>
          </div>
        </div>

        <div class="stat-card">
          <div class="stat-header">
            <div class="stat-icon performance">
              <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"></path>
                <polyline points="22 4 12 14.01 9 11.01"></polyline>
              </svg>
            </div>
            <span class="stat-trend positive">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polyline points="23 6 13.5 15.5 8.5 10.5 1 18"></polyline>
                <polyline points="17 6 23 6 23 12"></polyline>
              </svg>
              +3%
            </span>
          </div>
          <div class="stat-value">95%</div>
          <div class="stat-label">Pass Rate</div>
          <div class="stat-footer">
            <span class="stat-subtext">Year-over-year improvement</span>
          </div>
        </div>

        <div class="stat-card">
          <div class="stat-header">
            <div class="stat-icon excellence">
              <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"></polygon>
              </svg>
            </div>
            <span class="stat-trend positive">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polyline points="20 6 9 17 4 12"></polyline>
              </svg>
              Above target
            </span>
          </div>
          <div class="stat-value">3.45</div>
          <div class="stat-label">Average GPA</div>
          <div class="stat-footer">
            <span class="stat-subtext">Academic excellence</span>
          </div>
        </div>
      </div>
    </div>

    <div class="features-section">
      <h3 class="section-title">
        <span class="title-icon">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="12" cy="12" r="3"></circle>
            <path d="M12 1v6m0 6v6m5.196-14.196l-4.242 4.242m0 5.908l4.242 4.242M23 12h-6m-6 0H1m14.196 5.196l-4.242-4.242m0-5.908l4.242-4.242"></path>
          </svg>
        </span>
        Quick Access
      </h3>
      <div class="features-grid">
        <div class="feature-card primary">
          <div class="feature-glow"></div>
          <div class="feature-icon">
            <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M16 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path>
              <circle cx="8.5" cy="7" r="4"></circle>
              <line x1="20" y1="8" x2="20" y2="14"></line>
              <line x1="23" y1="11" x2="17" y2="11"></line>
            </svg>
          </div>
          <h4>Student Directory</h4>
          <p>Access comprehensive student profiles with complete academic records, contact information, and enrollment status tracking</p>
          <button @click="navigateToStudents" class="feature-btn">
            <span>View All Students</span>
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <line x1="5" y1="12" x2="19" y2="12"></line>
              <polyline points="12 5 19 12 12 19"></polyline>
            </svg>
          </button>
        </div>

        <div class="feature-card">
          <div class="feature-icon secondary">
            <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <circle cx="12" cy="12" r="10"></circle>
              <polyline points="12 6 12 12 16 14"></polyline>
            </svg>
          </div>
          <h4>Real-Time Synchronization</h4>
          <p>Live data integration with external APIs featuring automatic updates and instant synchronization across all platforms</p>
        </div>

        <div class="feature-card">
          <div class="feature-icon tertiary">
            <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <rect x="2" y="7" width="20" height="14" rx="2" ry="2"></rect>
              <path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"></path>
            </svg>
          </div>
          <h4>Modern Architecture</h4>
          <p>Built with Vue 3 Composition API, TypeScript, and cutting-edge web standards for maximum performance and scalability</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.home {
  animation: fadeIn 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Hero Section */
.hero {
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  border-radius: 16px;
  padding: 4rem 2.5rem;
  margin-bottom: 3rem;
  border: 1px solid #334155;
  box-shadow: 0 8px 20px -4px rgba(0, 0, 0, 0.4);
  position: relative;
  overflow: hidden;
}

.hero-glow {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, transparent, #6366f1, #8b5cf6, #6366f1, transparent);
  background-size: 200% 100%;
  animation: glow 3s linear infinite;
}

@keyframes glow {
  0% { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}

.hero-content {
  max-width: 900px;
  margin: 0 auto;
  text-align: center;
  color: white;
  position: relative;
  z-index: 1;
}

.hero h2 {
  font-size: 2.75rem;
  margin: 0 0 1.25rem 0;
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.15;
  background: linear-gradient(135deg, #f1f5f9 0%, #cbd5e1 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.subtitle {
  font-size: 1.188rem;
  color: #94a3b8;
  margin: 0;
  line-height: 1.6;
  font-weight: 400;
}

/* Section Title */
.section-title {
  color: #f1f5f9;
  font-size: 1.75rem;
  margin: 0 0 1.75rem 0;
  font-weight: 700;
  letter-spacing: -0.02em;
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.title-icon {
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}

/* Stats Section */
.stats-section {
  margin-bottom: 3rem;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.75rem;
}

.stat-card {
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  padding: 2rem;
  border-radius: 16px;
  border: 1px solid #334155;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

.stat-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 2px;
  background: linear-gradient(90deg, #6366f1, #8b5cf6);
  opacity: 0;
  transition: opacity 0.4s ease;
}

.stat-card:hover {
  border-color: #6366f1;
  transform: translateY(-8px);
  box-shadow: 0 20px 40px -8px rgba(99, 102, 241, 0.3);
}

.stat-card:hover::before {
  opacity: 1;
}

.stat-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1.5rem;
}

.stat-icon {
  width: 56px;
  height: 56px;
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  box-shadow: 0 8px 16px -4px rgba(0, 0, 0, 0.3);
}

.stat-icon.students {
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
}

.stat-icon.courses {
  background: linear-gradient(135deg, #8b5cf6 0%, #a855f7 100%);
}

.stat-icon.performance {
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
}

.stat-icon.excellence {
  background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
}

.stat-trend {
  display: flex;
  align-items: center;
  gap: 0.375rem;
  padding: 0.375rem 0.75rem;
  border-radius: 8px;
  font-size: 0.813rem;
  font-weight: 600;
}

.stat-trend.positive {
  background: rgba(16, 185, 129, 0.15);
  color: #6ee7b7;
  border: 1px solid rgba(16, 185, 129, 0.3);
}

.stat-trend.neutral {
  background: rgba(99, 102, 241, 0.15);
  color: #a5b4fc;
  border: 1px solid rgba(99, 102, 241, 0.3);
}

.stat-value {
  font-size: 3rem;
  font-weight: 700;
  color: #f1f5f9;
  line-height: 1;
  margin-bottom: 0.5rem;
}

.stat-label {
  color: #94a3b8;
  font-size: 0.875rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: 0.75rem;
}

.stat-footer {
  padding-top: 1rem;
  border-top: 1px solid #334155;
}

.stat-subtext {
  color: #64748b;
  font-size: 0.875rem;
  font-weight: 500;
}

/* Features Section */
.features-section {
  margin-bottom: 2rem;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 1.75rem;
}

.feature-card {
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  padding: 2.5rem;
  border-radius: 16px;
  border: 1px solid #334155;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  position: relative;
  overflow: hidden;
}

.feature-card.primary {
  border-color: rgba(99, 102, 241, 0.5);
  background: linear-gradient(135deg, rgba(30, 41, 59, 0.8) 0%, rgba(15, 23, 42, 0.8) 100%);
}

.feature-glow {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, #6366f1, #8b5cf6);
}

.feature-card:hover {
  border-color: #6366f1;
  transform: translateY(-8px);
  box-shadow: 0 20px 40px -8px rgba(99, 102, 241, 0.3);
}

.feature-icon {
  width: 72px;
  height: 72px;
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  margin-bottom: 1.5rem;
  box-shadow: 0 8px 20px -4px rgba(99, 102, 241, 0.5);
}

.feature-icon.secondary {
  background: linear-gradient(135deg, #8b5cf6 0%, #a855f7 100%);
}

.feature-icon.tertiary {
  background: linear-gradient(135deg, #10b981 0%, #059669 100%);
}

.feature-card h4 {
  margin: 0 0 1rem 0;
  color: #f1f5f9;
  font-size: 1.375rem;
  font-weight: 700;
  letter-spacing: -0.01em;
}

.feature-card p {
  color: #94a3b8;
  line-height: 1.7;
  margin: 0 0 1.5rem 0;
  font-size: 1rem;
}

.feature-btn {
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  color: white;
  border: none;
  padding: 1rem 1.75rem;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  font-size: 1rem;
  display: inline-flex;
  align-items: center;
  gap: 0.625rem;
  box-shadow: 0 4px 12px -2px rgba(99, 102, 241, 0.5);
}

.feature-btn:hover {
  transform: translateX(4px);
  box-shadow: 0 8px 20px -4px rgba(99, 102, 241, 0.7);
}

/* Responsive */
@media (max-width: 768px) {
  .hero {
    padding: 3rem 1.75rem;
  }
  
  .hero h2 {
    font-size: 2rem;
  }
  
  .subtitle {
    font-size: 1rem;
  }
  
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  
  .features-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 480px) {
  .stats-grid {
    grid-template-columns: 1fr;
  }
  
  .stat-value {
    font-size: 2.5rem;
  }
}
</style>