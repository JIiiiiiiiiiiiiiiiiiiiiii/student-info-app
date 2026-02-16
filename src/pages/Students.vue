<script setup lang="ts">
import { ref, onMounted } from 'vue'
import axios from 'axios'
import StudentComponent from '../components/StudentComponent.vue'

// TypeScript interface for API user data
interface User {
  id: number
  name: string
  username: string
  email: string
  phone: string
  website: string
  address: {
    street: string
    suite: string
    city: string
    zipcode: string
  }
  company: {
    name: string
    catchPhrase: string
    bs: string
  }
}

// Local student data with ALL possible fields
const localStudents = ref([
  { 
    id: 1001, 
    name: 'Juan Dela Cruz', 
    course: 'Computer Science', 
    year: 3,
    email: 'juan.delacruz@university.edu',
    phone: '+63 917 123 4567',
    address: '123 Taft Avenue, Malate',
    city: 'Manila',
    gpa: 3.75,
    enrollmentDate: 'August 2022',
    status: 'Active',
    website: 'juandelacruz.dev',
    company: 'Tech Innovations Inc.'
  },
  { 
    id: 1002, 
    name: 'Maria Santos', 
    course: 'Information Technology', 
    year: 2,
    email: 'maria.santos@university.edu',
    phone: '+63 918 234 5678',
    address: '456 Katipunan Avenue, Loyola Heights',
    city: 'Quezon City',
    gpa: 3.92,
    enrollmentDate: 'August 2023',
    status: 'Active',
    website: 'mariasantos.com',
    company: 'Digital Solutions Ltd.'
  },
  { 
    id: 1003, 
    name: 'Pedro Reyes', 
    course: 'Computer Engineering', 
    year: 4,
    email: 'pedro.reyes@university.edu',
    phone: '+63 919 345 6789',
    address: '789 España Boulevard, Sampaloc',
    city: 'Manila',
    gpa: 3.45,
    enrollmentDate: 'August 2021',
    status: 'Active',
    company: 'Engineering Systems Corp.'
  },
  { 
    id: 1004, 
    name: 'Ana Garcia', 
    course: 'Data Science', 
    year: 1,
    email: 'ana.garcia@university.edu',
    phone: '+63 920 456 7890',
    address: '321 EDSA, Cubao',
    city: 'Quezon City',
    gpa: 3.88,
    enrollmentDate: 'August 2024',
    status: 'Active',
    website: 'anagarcia.io',
    company: 'Data Analytics Group'
  },
  { 
    id: 1005, 
    name: 'Carlos Mendoza', 
    course: 'Software Engineering', 
    year: 3,
    email: 'carlos.mendoza@university.edu',
    phone: '+63 921 567 8901',
    address: '654 Aurora Boulevard, Araneta Center',
    city: 'Quezon City',
    gpa: 3.67,
    enrollmentDate: 'August 2022',
    status: 'Active',
    website: 'carlosmendoza.tech'
  },
  { 
    id: 1006, 
    name: 'Isabella Cruz', 
    course: 'Computer Science', 
    year: 2,
    email: 'isabella.cruz@university.edu',
    phone: '+63 922 678 9012',
    address: '987 Roxas Boulevard, Baclaran',
    city: 'Parañaque',
    gpa: 3.95,
    enrollmentDate: 'August 2023',
    status: 'Active',
    company: 'Software Innovations Inc.'
  }
])

// API data
const apiUsers = ref<User[]>([])
const loading = ref(false)
const error = ref<string | null>(null)

// Courses array for random assignment
const courses = [
  'Computer Science',
  'Information Technology',
  'Computer Engineering',
  'Data Science',
  'Software Engineering',
  'Cybersecurity',
  'Artificial Intelligence'
]

// Fetch data from JSONPlaceholder API with 3-second delay
const fetchUsers = async () => {
  loading.value = true
  error.value = null
  
  try {
    // Add 3-second delay to show loading state
    await new Promise(resolve => setTimeout(resolve, 3000))
    
    const response = await axios.get('https://jsonplaceholder.typicode.com/users')
    apiUsers.value = response.data
    console.log('API Users fetched:', apiUsers.value)
  } catch (err) {
    if (axios.isAxiosError(err)) {
      error.value = `Failed to fetch users: ${err.message}`
    } else {
      error.value = 'An unexpected error occurred while fetching student data'
    }
    console.error('Error fetching users:', err)
  } finally {
    loading.value = false
  }
}

// Convert API user to student format with ALL available data
const convertToStudent = (user: User, index: number) => {
  const student = {
    id: user.id,
    name: user.name,
    course: courses[index % courses.length],
    year: (index % 4) + 1,
    email: user.email,
    phone: user.phone,
    address: `${user.address.suite}, ${user.address.street}`,
    city: user.address.city,
    website: user.website,
    company: user.company.name,
    gpa: 3.0 + Math.random(),
    enrollmentDate: 'September 2023',
    status: 'Active'
  }
  return student
}

// Retry function
const retryFetch = () => {
  fetchUsers()
}

// Fetch on component mount
onMounted(() => {
  console.log('Students page mounted, local students:', localStudents.value)
  fetchUsers()
})
</script>

<template>
  <div class="students-page">
    <div class="page-header">
      <div class="header-content">
        <div class="header-text">
          <h2>Student Directory</h2>
          <p class="header-subtitle">Comprehensive academic records and enrollment management system</p>
        </div>
        <div class="header-stats">
          <div class="stat-pill">
            <div class="stat-icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"></path>
                <circle cx="9" cy="7" r="4"></circle>
                <path d="M23 21v-2a4 4 0 0 0-3-3.87"></path>
                <path d="M16 3.13a4 4 0 0 1 0 7.75"></path>
              </svg>
            </div>
            <div class="stat-content">
              <span class="stat-number">{{ localStudents.length + apiUsers.length }}</span>
              <span class="stat-text">Total Students</span>
            </div>
          </div>
          <div class="stat-pill">
            <div class="stat-icon">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <polyline points="22 12 18 12 15 21 9 3 6 12 2 12"></polyline>
              </svg>
            </div>
            <div class="stat-content">
              <span class="stat-number">95%</span>
              <span class="stat-text">Active Status</span>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Local Students Section -->
    <section class="students-section">
      <div class="section-header">
        <div class="section-title-group">
          <div class="section-icon">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
              <polyline points="9 22 9 12 15 12 15 22"></polyline>
            </svg>
          </div>
          <div>
            <h3 class="section-title">Enrolled Students</h3>
            <p class="section-subtitle">Currently active student records in the system</p>
          </div>
        </div>
        <div class="section-badge">
          <span class="badge-number">{{ localStudents.length }}</span>
          <span class="badge-text">Students</span>
        </div>
      </div>
      
      <div v-if="localStudents.length > 0" class="students-grid">
        <StudentComponent
          v-for="student in localStudents"
          :key="student.id"
          :id="student.id"
          :name="student.name"
          :course="student.course"
          :year="student.year"
          :email="student.email"
          :phone="student.phone"
          :address="student.address"
          :city="student.city"
          :website="student.website"
          :company="student.company"
          :gpa="student.gpa"
          :enrollment-date="student.enrollmentDate"
          :status="student.status"
        />
      </div>
    </section>

    <!-- API Students Section -->
    <section class="students-section">
      <div class="section-header">
        <div class="section-title-group">
          <div class="section-icon external">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <circle cx="12" cy="12" r="10"></circle>
              <line x1="2" y1="12" x2="22" y2="12"></line>
              <path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"></path>
            </svg>
          </div>
          <div>
            <h3 class="section-title">External Database</h3>
            <p class="section-subtitle">Live data synchronized from JSONPlaceholder API</p>
          </div>
        </div>
        <button @click="fetchUsers" class="refresh-btn" :disabled="loading">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" :class="{ spinning: loading }">
            <polyline points="23 4 23 10 17 10"></polyline>
            <polyline points="1 20 1 14 7 14"></polyline>
            <path d="M3.51 9a9 9 0 0 1 14.85-3.36L23 10M1 14l4.64 4.36A9 9 0 0 0 20.49 15"></path>
          </svg>
          {{ loading ? 'Loading...' : 'Refresh Data' }}
        </button>
      </div>

      <!-- Loading State -->
      <div v-if="loading" class="loading-container">
        <div class="loading-spinner">
          <div class="spinner-ring"></div>
          <div class="spinner-ring"></div>
          <div class="spinner-ring"></div>
        </div>
        <p class="loading-text">Fetching student records...</p>
        <p class="loading-subtext">Please wait while we retrieve the data</p>
      </div>

      <!-- Error State -->
      <div v-else-if="error" class="error-container">
        <div class="error-icon">
          <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="12" cy="12" r="10"></circle>
            <line x1="12" y1="8" x2="12" y2="12"></line>
            <line x1="12" y1="16" x2="12.01" y2="16"></line>
          </svg>
        </div>
        <h4>Connection Failed</h4>
        <p class="error-message">{{ error }}</p>
        <button @click="retryFetch" class="retry-btn">
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <polyline points="23 4 23 10 17 10"></polyline>
            <polyline points="1 20 1 14 7 14"></polyline>
            <path d="M3.51 9a9 9 0 0 1 14.85-3.36L23 10M1 14l4.64 4.36A9 9 0 0 0 20.49 15"></path>
          </svg>
          Retry Connection
        </button>
      </div>

      <!-- Success State -->
      <div v-else-if="apiUsers.length > 0" class="students-grid">
        <StudentComponent
          v-for="(user, index) in apiUsers"
          :key="`api-${user.id}`"
          v-bind="convertToStudent(user, index)"
        />
      </div>

      <!-- Empty State -->
      <div v-else class="empty-state">
        <div class="empty-icon">
          <svg width="64" height="64" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
            <circle cx="12" cy="12" r="10"></circle>
            <path d="M12 8v4m0 4h.01"></path>
          </svg>
        </div>
        <p class="empty-title">No External Records</p>
        <p class="empty-text">Click "Refresh Data" to synchronize with the external database</p>
      </div>
    </section>
  </div>
</template>

<style scoped>
.students-page {
  animation: fadeIn 0.6s cubic-bezier(0.4, 0, 0.2, 1);
  padding-bottom: 2rem;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* Page Header */
.page-header {
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  padding: 2rem;
  border-radius: 12px;
  margin-bottom: 2rem;
  border: 1px solid #334155;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  position: relative;
  overflow: hidden;
}

.page-header::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 2px;
  background: linear-gradient(90deg, #6366f1, #8b5cf6, #6366f1);
  background-size: 200% 100%;
  animation: shimmer 3s linear infinite;
}

@keyframes shimmer {
  0% { background-position: -200% 0; }
  100% { background-position: 200% 0; }
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 2rem;
  flex-wrap: wrap;
}

.header-text h2 {
  margin: 0 0 0.5rem 0;
  color: #f1f5f9;
  font-size: 1.875rem;
  font-weight: 700;
  letter-spacing: -0.02em;
}

.header-subtitle {
  margin: 0;
  color: #94a3b8;
  font-size: 0.938rem;
}

.header-stats {
  display: flex;
  gap: 1rem;
}

.stat-pill {
  background: linear-gradient(135deg, rgba(99, 102, 241, 0.15) 0%, rgba(139, 92, 246, 0.15) 100%);
  padding: 1rem 1.25rem;
  border-radius: 10px;
  display: flex;
  align-items: center;
  gap: 0.875rem;
  border: 1px solid rgba(99, 102, 241, 0.3);
}

.stat-icon {
  width: 40px;
  height: 40px;
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  flex-shrink: 0;
}

.stat-content {
  display: flex;
  flex-direction: column;
  gap: 0.125rem;
}

.stat-number {
  color: #f1f5f9;
  font-size: 1.5rem;
  font-weight: 700;
  line-height: 1;
}

.stat-text {
  color: #cbd5e1;
  font-size: 0.75rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

/* Section */
.students-section {
  margin-bottom: 2.5rem;
}

.section-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1.5rem;
  flex-wrap: wrap;
  gap: 1rem;
  padding: 1.25rem;
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  border-radius: 10px;
  border: 1px solid #334155;
}

.section-title-group {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.section-icon {
  width: 44px;
  height: 44px;
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  flex-shrink: 0;
}

.section-icon.external {
  background: linear-gradient(135deg, #8b5cf6 0%, #a855f7 100%);
}

.section-title {
  color: #f1f5f9;
  font-size: 1.25rem;
  margin: 0 0 0.25rem 0;
  font-weight: 700;
}

.section-subtitle {
  color: #94a3b8;
  font-size: 0.813rem;
  margin: 0;
}

.section-badge {
  background: rgba(99, 102, 241, 0.15);
  border: 1px solid rgba(99, 102, 241, 0.3);
  padding: 0.625rem 1rem;
  border-radius: 8px;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.badge-number {
  color: #a5b4fc;
  font-size: 1.25rem;
  font-weight: 700;
}

.badge-text {
  color: #cbd5e1;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
}

.refresh-btn {
  background: linear-gradient(135deg, rgba(51, 65, 85, 0.8) 0%, rgba(30, 41, 59, 0.8) 100%);
  color: #cbd5e1;
  border: 1px solid #475569;
  padding: 0.75rem 1.25rem;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 0.875rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.refresh-btn:hover:not(:disabled) {
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  border-color: #6366f1;
  color: white;
  transform: translateY(-1px);
}

.refresh-btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.spinning {
  animation: spin 1s linear infinite;
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

.students-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
  gap: 1.5rem;
}

/* Loading State */
.loading-container {
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  padding: 4rem 2rem;
  border-radius: 12px;
  text-align: center;
  border: 1px solid #334155;
}

.loading-spinner {
  width: 64px;
  height: 64px;
  margin: 0 auto 1.5rem;
  position: relative;
}

.spinner-ring {
  position: absolute;
  width: 100%;
  height: 100%;
  border: 3px solid transparent;
  border-top-color: #6366f1;
  border-radius: 50%;
  animation: spin 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
}

.spinner-ring:nth-child(2) {
  border-top-color: #8b5cf6;
  animation-delay: -0.4s;
}

.spinner-ring:nth-child(3) {
  border-top-color: #a855f7;
  animation-delay: -0.8s;
}

.loading-text {
  color: #f1f5f9;
  font-size: 1.125rem;
  margin: 0 0 0.5rem 0;
  font-weight: 600;
}

.loading-subtext {
  color: #94a3b8;
  font-size: 0.875rem;
  margin: 0;
}

/* Error State */
.error-container {
  background: linear-gradient(135deg, rgba(30, 41, 59, 0.8) 0%, rgba(15, 23, 42, 0.8) 100%);
  padding: 3rem 2rem;
  border-radius: 12px;
  text-align: center;
  border: 1px solid rgba(239, 68, 68, 0.3);
}

.error-icon {
  width: 72px;
  height: 72px;
  background: rgba(239, 68, 68, 0.15);
  border: 2px solid rgba(239, 68, 68, 0.3);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #f87171;
  margin: 0 auto 1.25rem;
}

.error-container h4 {
  color: #f1f5f9;
  margin: 0 0 0.75rem 0;
  font-size: 1.5rem;
  font-weight: 700;
}

.error-message {
  color: #fca5a5;
  margin: 0 0 1.5rem 0;
  font-weight: 500;
}

.retry-btn {
  background: linear-gradient(135deg, #ef4444 0%, #dc2626 100%);
  color: white;
  border: none;
  padding: 0.875rem 1.75rem;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  box-shadow: 0 4px 12px rgba(239, 68, 68, 0.4);
}

.retry-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(239, 68, 68, 0.5);
}

/* Empty State */
.empty-state {
  background: linear-gradient(135deg, #1e293b 0%, #0f172a 100%);
  padding: 4rem 2rem;
  border-radius: 12px;
  text-align: center;
  border: 1px solid #334155;
}

.empty-icon {
  width: 80px;
  height: 80px;
  background: rgba(51, 65, 85, 0.3);
  border: 2px solid #475569;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #64748b;
  margin: 0 auto 1.25rem;
}

.empty-title {
  color: #f1f5f9;
  font-size: 1.25rem;
  font-weight: 600;
  margin: 0 0 0.5rem 0;
}

.empty-text {
  color: #94a3b8;
  margin: 0;
}

/* Responsive */
@media (max-width: 768px) {
  .students-grid {
    grid-template-columns: 1fr;
  }
  
  .header-content {
    flex-direction: column;
  }
  
  .header-stats {
    width: 100%;
    flex-direction: column;
  }
  
  .stat-pill {
    width: 100%;
  }
  
  .section-header {
    flex-direction: column;
    align-items: flex-start;
  }
  
  .refresh-btn {
    width: 100%;
    justify-content: center;
  }
}
</style>s