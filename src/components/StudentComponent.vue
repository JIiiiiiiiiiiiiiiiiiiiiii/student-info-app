<script setup lang="ts">
import { ref, computed } from 'vue'

// Define comprehensive props interface
interface StudentProps {
  name: string
  course: string
  year: number
  id: number
  email?: string
  phone?: string
  address?: string
  city?: string
  website?: string
  company?: string
  gpa?: number
  enrollmentDate?: string
  status?: string
}

// Accept props with defaults
const props = withDefaults(defineProps<StudentProps>(), {
  email: '',
  phone: '',
  address: '',
  city: '',
  website: '',
  company: '',
  gpa: 0,
  enrollmentDate: 'September 2023',
  status: 'Active'
})

// State management
const isExpanded = ref(false)
const enrollmentStatus = ref(props.status || 'Active')

// Computed properties
const studentInitials = computed(() => {
  return props.name
    .split(' ')
    .map(n => n[0])
    .join('')
    .toUpperCase()
    .slice(0, 2)
})

const generatedEmail = computed(() => {
  return props.email || props.name.toLowerCase().replace(/\s+/g, '.') + '@university.edu'
})

const generatedPhone = computed(() => {
  if (props.phone) return props.phone
  const randomPhone = Math.floor(Math.random() * 9000000000) + 1000000000
  return `+63 ${randomPhone.toString().slice(0, 3)} ${randomPhone.toString().slice(3, 6)} ${randomPhone.toString().slice(6)}`
})

const calculatedGPA = computed(() => {
  if (props.gpa) return props.gpa.toFixed(2)
  return (3.0 + Math.random()).toFixed(2)
})

const academicStanding = computed(() => {
  const gpa = parseFloat(calculatedGPA.value)
  if (gpa >= 3.7) return { text: 'Dean\'s List', class: 'excellent' }
  if (gpa >= 3.0) return { text: 'Good Standing', class: 'good' }
  if (gpa >= 2.0) return { text: 'Regular', class: 'regular' }
  return { text: 'Warning', class: 'warning' }
})

const creditsEarned = computed(() => {
  return props.year * 30 + Math.floor(Math.random() * 15)
})

// Event handlers
const toggleDetails = () => {
  isExpanded.value = !isExpanded.value
}

const changeStatus = () => {
  enrollmentStatus.value = enrollmentStatus.value === 'Active' ? 'Inactive' : 'Active'
}
</script>

<template>
  <div class="student-card">
    <!-- Compact Header -->
    <div class="card-header">
      <div class="student-avatar">
        <span class="initials">{{ studentInitials }}</span>
      </div>
      
      <div class="student-info">
        <h3>{{ props.name }}</h3>
        <div class="meta-row">
          <span class="student-id">{{ String(props.id).padStart(6, '0') }}</span>
          <span class="divider">•</span>
          <span class="course">{{ props.course }}</span>
          <span class="divider">•</span>
          <span class="year">Year {{ props.year }}</span>
        </div>
      </div>

      <span class="status-badge" :class="{ active: enrollmentStatus === 'Active', inactive: enrollmentStatus === 'Inactive' }">
        <span class="status-dot"></span>
        {{ enrollmentStatus }}
      </span>
    </div>

    <!-- Compact Stats -->
    <div class="stats-row">
      <div class="stat">
        <span class="stat-label">GPA</span>
        <span class="stat-value" :class="academicStanding.class">{{ calculatedGPA }}</span>
      </div>
      <div class="stat">
        <span class="stat-label">Credits</span>
        <span class="stat-value">{{ creditsEarned }}</span>
      </div>
      <div class="stat">
        <span class="stat-label">Standing</span>
        <span class="stat-badge" :class="academicStanding.class">{{ academicStanding.text }}</span>
      </div>
    </div>

    <!-- Compact Contact Info -->
    <div class="contact-grid">
      <div class="contact-item">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path>
          <polyline points="22,6 12,13 2,6"></polyline>
        </svg>
        <span>{{ generatedEmail }}</span>
      </div>
      <div class="contact-item">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"></path>
        </svg>
        <span>{{ generatedPhone }}</span>
      </div>
    </div>

    <!-- Expandable Details (Compact) -->
    <transition name="expand">
      <div v-if="isExpanded" class="expanded-details">
        <div class="detail-row">
          <span class="detail-label">Address</span>
          <span class="detail-value">{{ props.address || props.city || 'Not provided' }}</span>
        </div>
        <div class="detail-row" v-if="props.website">
          <span class="detail-label">Website</span>
          <span class="detail-value link">{{ props.website }}</span>
        </div>
        <div class="detail-row" v-if="props.company">
          <span class="detail-label">Company</span>
          <span class="detail-value">{{ props.company }}</span>
        </div>
        <div class="detail-row">
          <span class="detail-label">Enrolled</span>
          <span class="detail-value">{{ props.enrollmentDate }}</span>
        </div>
      </div>
    </transition>

    <!-- Compact Actions -->
    <div class="card-actions">
      <button @click="toggleDetails" class="btn btn-secondary">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
          <polyline :points="isExpanded ? '18 15 12 9 6 15' : '6 9 12 15 18 9'"></polyline>
        </svg>
        {{ isExpanded ? 'Less' : 'More' }}
      </button>
      <button @click="changeStatus" class="btn btn-primary">
        {{ enrollmentStatus === 'Active' ? 'Deactivate' : 'Activate' }}
      </button>
    </div>
  </div>
</template>

<style scoped>
.student-card {
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  border-radius: 12px;
  overflow: hidden;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border: 1px solid #334155;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
}

.student-card:hover {
  border-color: #6366f1;
  box-shadow: 0 8px 24px rgba(99, 102, 241, 0.25);
  transform: translateY(-2px);
}

/* Compact Header */
.card-header {
  padding: 1.25rem;
  display: flex;
  gap: 1rem;
  align-items: center;
  background: linear-gradient(135deg, rgba(99, 102, 241, 0.08) 0%, rgba(139, 92, 246, 0.05) 100%);
  border-bottom: 1px solid #334155;
}

.student-avatar {
  width: 48px;
  height: 48px;
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  box-shadow: 0 4px 12px rgba(99, 102, 241, 0.4);
}

.initials {
  color: white;
  font-size: 1.125rem;
  font-weight: 700;
}

.student-info {
  flex: 1;
  min-width: 0;
}

.student-info h3 {
  margin: 0 0 0.375rem 0;
  color: #f1f5f9;
  font-size: 1.125rem;
  font-weight: 700;
  line-height: 1.2;
}

.meta-row {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  flex-wrap: wrap;
  font-size: 0.813rem;
}

.student-id {
  color: #94a3b8;
  font-weight: 600;
  font-family: 'Courier New', monospace;
}

.divider {
  color: #475569;
}

.course,
.year {
  color: #cbd5e1;
  font-weight: 500;
}

.status-badge {
  padding: 0.375rem 0.75rem;
  border-radius: 6px;
  font-size: 0.75rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  display: flex;
  align-items: center;
  gap: 0.375rem;
  white-space: nowrap;
  flex-shrink: 0;
}

.status-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

.status-badge.active {
  background: rgba(16, 185, 129, 0.15);
  color: #6ee7b7;
  border: 1px solid rgba(16, 185, 129, 0.3);
}

.status-badge.active .status-dot {
  background: #10b981;
  box-shadow: 0 0 6px rgba(16, 185, 129, 0.6);
}

.status-badge.inactive {
  background: rgba(239, 68, 68, 0.15);
  color: #fca5a5;
  border: 1px solid rgba(239, 68, 68, 0.3);
}

.status-badge.inactive .status-dot {
  background: #ef4444;
  box-shadow: 0 0 6px rgba(239, 68, 68, 0.6);
}

/* Compact Stats */
.stats-row {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1px;
  background: #334155;
  border-bottom: 1px solid #334155;
}

.stat {
  padding: 0.875rem;
  background: rgba(15, 23, 42, 0.5);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.25rem;
}

.stat-label {
  color: #94a3b8;
  font-size: 0.688rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.stat-value {
  color: #f1f5f9;
  font-size: 1.125rem;
  font-weight: 700;
}

.stat-badge {
  font-size: 0.688rem;
  font-weight: 600;
  padding: 0.25rem 0.5rem;
  border-radius: 4px;
  text-transform: uppercase;
  letter-spacing: 0.03em;
}

.stat-value.excellent,
.stat-badge.excellent {
  color: #6ee7b7;
}

.stat-value.good,
.stat-badge.good {
  color: #93c5fd;
}

.stat-value.regular,
.stat-badge.regular {
  color: #fcd34d;
}

.stat-value.warning,
.stat-badge.warning {
  color: #fca5a5;
}

/* Compact Contact */
.contact-grid {
  padding: 1rem 1.25rem;
  display: flex;
  flex-direction: column;
  gap: 0.625rem;
  border-bottom: 1px solid #334155;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 0.625rem;
  color: #cbd5e1;
  font-size: 0.875rem;
}

.contact-item svg {
  color: #6366f1;
  flex-shrink: 0;
}

.contact-item span {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/* Expanded Details */
.expanded-details {
  padding: 1rem 1.25rem;
  background: rgba(15, 23, 42, 0.3);
  border-bottom: 1px solid #334155;
}

.detail-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 0;
  border-bottom: 1px solid #334155;
}

.detail-row:last-child {
  border-bottom: none;
}

.detail-label {
  color: #94a3b8;
  font-size: 0.813rem;
  font-weight: 600;
}

.detail-value {
  color: #e2e8f0;
  font-size: 0.875rem;
  font-weight: 500;
  text-align: right;
}

.detail-value.link {
  color: #a5b4fc;
  text-decoration: underline;
}

/* Actions */
.card-actions {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 0.75rem;
  padding: 1rem 1.25rem;
  background: rgba(15, 23, 42, 0.5);
}

.btn {
  padding: 0.625rem 1rem;
  border: none;
  border-radius: 8px;
  font-weight: 600;
  font-size: 0.875rem;
  cursor: pointer;
  transition: all 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
}

.btn-primary {
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  color: white;
  box-shadow: 0 2px 8px rgba(99, 102, 241, 0.3);
}

.btn-primary:hover {
  box-shadow: 0 4px 12px rgba(99, 102, 241, 0.5);
  transform: translateY(-1px);
}

.btn-secondary {
  background: rgba(51, 65, 85, 0.5);
  color: #cbd5e1;
  border: 1px solid #475569;
}

.btn-secondary:hover {
  background: rgba(71, 85, 105, 0.5);
  border-color: #64748b;
}

/* Expand Animation */
.expand-enter-active,
.expand-leave-active {
  transition: all 0.3s ease;
  overflow: hidden;
}

.expand-enter-from,
.expand-leave-to {
  opacity: 0;
  max-height: 0;
}

.expand-enter-to,
.expand-leave-from {
  opacity: 1;
  max-height: 300px;
}

/* Responsive */
@media (max-width: 640px) {
  .card-header {
    flex-wrap: wrap;
  }
  
  .status-badge {
    width: 100%;
    justify-content: center;
  }
  
  .stats-row {
    grid-template-columns: repeat(3, 1fr);
  }
  
  .detail-row {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.25rem;
  }
  
  .detail-value {
    text-align: left;
  }
}
</style>