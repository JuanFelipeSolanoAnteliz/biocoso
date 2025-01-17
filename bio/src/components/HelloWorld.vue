<template>
  <div class="min-h-screen bg-white">
    <!-- Header -->
    <header class="header">
      <div class="flex items-center gap-2">
        <div class="logo" />
        <span class="title">MediCare</span>
      </div>
      <nav class="nav">
        <a href="#" class="nav-link">Home</a>
        <a href="#" class="nav-link">Our Services</a>
        <a href="#" class="nav-link">About Us</a>
        <a href="#" class="nav-link">Contact Us</a>
      </nav>
      <button class="btn-primary">Book Appointment</button>
    </header>

    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-text">
        <h1 class="hero-title">Feel Comfort<br />Be Healthy</h1>
        <p class="hero-description">Get the best medical services you deserve. We care about your health and well-being.</p>
        <div class="info-cards">
          <div class="info-card">
            <Calendar class="icon" />
            <div>
              <h3 class="info-card-title">Book an Appointment</h3>
              <p class="info-card-description">Schedule your visit at your convenience</p>
            </div>
          </div>
          <div class="info-card">
            <Star class="icon" />
            <div>
              <h3 class="info-card-title">Get the Best Service</h3>
              <p class="info-card-description">Professional and caring staff</p>
            </div>
          </div>
        </div>
        <button class="btn-primary">Make Appointment</button>
      </div>
      <div class="hero-image">
        <img src="https://hebbkx1anhila5yf.public.blob.vercel-storage.com/image-UtEq36A0JundWzV8HSoxv335NXhj77.png" alt="Medical Care" />
      </div>
    </section>

    <!-- Services Section -->
    <section class="services">
      <h2 class="section-title">Our Services</h2>
      <div class="service-cards">
        <div class="service-card" v-for="service in services" :key="service.title">
          <img :src="service.image" :alt="service.title" class="service-image" />
          <h3 class="service-title">{{ service.title }}</h3>
          <p class="service-description">{{ service.description }}</p>
        </div>
      </div>
    </section>

    <!-- Why Us Section -->
    <section class="why-us">
      <h2 class="section-title">Why Us?</h2>
      <div class="feature-cards">
        <div class="feature-card" v-for="feature in features" :key="feature.title">
          <div class="feature-icon">
            <component :is="feature.icon" class="icon" />
          </div>
          <h3 class="feature-title">{{ feature.title }}</h3>
          <p class="feature-description">{{ feature.description }}</p>
        </div>
      </div>
    </section>

    <!-- Doctors Section -->
    <section class="doctors">
      <div class="doctors-header">
        <h2 class="section-title">Our Qualified Doctors</h2>
        <button class="btn-secondary">See all Doctors</button>
      </div>
      <div class="doctor-cards">
        <div class="doctor-card" v-for="doctor in doctors" :key="doctor.name">
          <div class="doctor-info">
            <div class="doctor-image">
              <img src="/placeholder.svg" :alt="doctor.name" />
            </div>
            <div>
              <h3 class="doctor-name">{{ doctor.name }}</h3>
              <p class="doctor-specialty">{{ doctor.specialty }}</p>
            </div>
          </div>
          <div class="doctor-availability">
            <Clock class="icon" />
            <span>{{ doctor.availability }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats Section -->
    <section class="stats">
      <div class="stats-cards">
        <div class="stats-card">
          <div class="stats-value">99%</div>
          <p class="stats-description">Patient Satisfaction</p>
        </div>
        <div class="stats-card">
          <div class="stats-value">2,300+</div>
          <p class="stats-description">Medical Professionals</p>
        </div>
        <div class="stats-card">
          <div class="stats-value">43</div>
          <p class="stats-description">Professional Services</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { Calendar, Star, Activity, Shield, Users, Clock } from 'lucide-vue-next'

const services = [
  {
    title: "Immediate Care",
    description: "Get immediate medical attention when you need it most",
    image: "/placeholder.svg",
  },
  {
    title: "Dental Care",
    description: "Professional dental services for a healthy smile",
    image: "/placeholder.svg",
  },
  {
    title: "Diagnostic Center",
    description: "Advanced diagnostic services for accurate results",
    image: "/placeholder.svg",
  },
]

const features = [
  {
    title: "DNA Diagnostics",
    description: "Advanced genetic testing and analysis for personalized care",
    icon: Activity,
  },
  {
    title: "Insurance",
    description: "We work with major insurance providers for your convenience",
    icon: Shield,
  },
  {
    title: "Medical Support",
    description: "24/7 medical support from our qualified professionals",
    icon: Users,
  },
]

const doctors = [
  {
    name: "Dr. Jane Smith",
    specialty: "Cardiologist",
    availability: "MON-FRI, 09:00-17:00",
  },
  {
    name: "Dr. John Davis",
    specialty: "Neurologist",
    availability: "MON-THU, 10:00-18:00",
  },
  {
    name: "Dr. Sarah Wilson",
    specialty: "Pediatrician",
    availability: "TUE-SAT, 09:00-16:00",
  },
]
</script>

<style scoped>
/* Header */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 1rem;
  max-width: 1200px;
  margin: 0 auto;
}

.logo {
  width: 2rem;
  height: 2rem;
  background-color: #3b82f6;
  border-radius: 9999px;
}

.title {
  font-size: 1.25rem;
  font-weight: bold;
}

.nav {
  display: none;
}

.nav-link {
  font-size: 0.875rem;
  font-weight: medium;
  margin-right: 2rem;
  color: #4b5563;
}

.nav-link:hover {
  color: #1f2937;
}

.btn-primary {
  background-color: #3b82f6;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 0.375rem;
}

.btn-primary:hover {
  background-color: #2563eb;
}

/* Hero Section */
.hero {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  padding: 4rem 1rem;
  max-width: 1200px;
  margin: 0 auto;
}

.hero-text {
  max-width: 500px;
}

.hero-title {
  font-size: 3rem;
  font-weight: bold;
  line-height: 1.2;
}

.hero-description {
  color: #4b5563;
  font-size: 1.125rem;
  margin-top: 1rem;
}

.info-cards {
  margin-top: 2rem;
}

.info-card {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.info-card-title {
  font-weight: 600;
}

.info-card-description {
  font-size: 0.875rem;
  color: #4b5563;
}

.hero-image img {
  width: 100%;
  height: auto;
  border-radius: 1rem;
  object-fit: cover;
}

/* Services Section */
.services {
  padding: 4rem 1rem;
  max-width: 1200px;
  margin: 0 auto;
}

.section-title {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 3rem;
}

.service-cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

.service-card {
  background-color: white;
  padding: 1.5rem;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.service-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 0.5rem;
}

.service-title {
  font-size: 1.25rem;
  font-weight: 600;
  margin-top: 1rem;
}

.service-description {
  color: #4b5563;
}

/* Add other sections similarly... */

/* Stats Section */
.stats {
  background-color: #111827;
  color: white;
  padding: 4rem 1rem;
}

.stats-cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.stats-card {
  text-align: center;
}

.stats-value {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.stats-description {
  color: #9ca3af;
}
</style>
