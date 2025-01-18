<template>
  <div class="min-h-screen bg-white">
    <!-- Header -->
    <header class="header">
      <div class="flex items-center gap-2">
        <span class="title"><img src="../assets/01_01-2.jpg" alt=""></span>
      </div>
      <nav class="nav">
        <a href="#" class="nav-link">Home</a>
        <a href="#" class="nav-link">Our Services</a>
        <a href="#" class="nav-link">About Us</a>
        <a href="#" class="nav-link">Contact Us</a>
      </nav>
    </header>

    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-text">
        <h1 class="hero-title">Biocentral<br />Electronica</h1>
        <p class="hero-description">Portafolio de servicios 2024</p>
        <div class="info-cards">
          <section class="service-features">
            <div class="service-features__container">
              <div v-for="(feature, index) in features" :key="index" class="service-features__item">
                <div class="service-features__icon-container">
                  <component :is="feature.icon" class="service-features__icon" />
                </div>
                <div class="service-features__content">
                  <h3 class="service-features__heading">{{ feature.title }}</h3>
                  <p class="service-features__text">{{ feature.description }}</p>
                </div>
              </div>
            </div>
          </section>

        
        </div>
        
      </div>
      <div class="hero-image">
        <img src="../assets/pexels-artempodrez-5726706.jpg" alt="Medical Care" />
      </div>
    </section>

    <!-- Services Section -->
    <section class="services">
      <h2 class="section-title">Nuestros Servicios</h2>
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
      <h2 class="section-title">¿Por qué nosotros?</h2>
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
        <h2 class="section-title">Vision y Mision</h2>
      </div>
      <div class="doctor-cards">
        <div class="doctor-card" v-for="doctor in doctors" :key="doctor.name">
          <div class="doctor-info">
            <div class="doctor-image">
              <img src="" :alt="doctor.name" />
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
.service-features {
  padding: 20px;
  background-color: #FDF8F6;
  border-radius: 12px;
}

.service-features__container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
}

.service-features__item {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  padding: 16px;
  background-color: #FFFFFF;
  border-radius: 8px;
  transition: transform 0.2s ease;
}

.service-features__item:hover {
  transform: translateY(-2px);
}

.service-features__icon-container {
  display: flex;
  align-items: center;
  justify-content: center;
}

.service-features__icon {
  width: 24px;
  height: 24px;
  color: #F97316;
}

.service-features__content {
  flex: 1;
}

.service-features__heading {
  font-size: 16px;
  font-weight: 600;
  color: #334155;
  margin-bottom: 4px;
}

.service-features__text {
  font-size: 14px;
  color: #64748B;
  line-height: 1.4;
}

@media (max-width: 640px) {
  .service-features__container {
    grid-template-columns: 1fr;
  }
}
.title img{
  width: 200px;
}
.header {
  display: flex;
  justify-content: space-between;
  max-height: 100px;
}

.title {
  font-size: 15rem;
  font-weight: bold;
  margin: 0px;
}

.nav {
  display: flex; 
  justify-content: flex-end; 
  gap: 2rem; 
}


.nav-link {
  font-size: 1rem;
  font-weight: medium;
  margin-right: 2rem;
  color: #4b5563;
  text-decoration: none;
}

.nav-link:hover {
  color: #90b5e9;
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
  background: #9ca3af;
  border-radius: 15px;
  padding: 5px;
  display: flex;
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
  max-height: 850px;
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

.why-us {
  padding: 4rem 1rem;
  max-width: 1200px;
  margin: 0 auto;
}

.feature-cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

.feature-card {
  background-color: white;
  padding: 1.5rem;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.feature-icon {
  width: 64px;
  height: 64px;
  background-color: #E6F0FF;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 1rem;
}

.feature-title {
  font-size: 1.25rem;
  font-weight: 600;
  margin-top: 1rem;
  color: #1a1a1a;
}

.feature-description {
  color: #4b5563;
  margin-top: 0.5rem;
}

.doctors {
  padding: 4rem 1rem;
  max-width: 1200px;
  margin: 0 auto;
}

.doctors-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 3rem;
}

.btn-secondary {
  background-color: transparent;
  color: #3b82f6;
  border: 1px solid #3b82f6;
  padding: 0.5rem 1rem;
  border-radius: 0.375rem;
}

.btn-secondary:hover {
  background-color: #3b82f6;
  color: white;
}

.doctor-cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

.doctor-card {
  background-color: white;
  padding: 1.5rem;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.doctor-info {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1rem;
}

.doctor-image {
  width: 64px;
  height: 64px;
  border-radius: 50%;
  overflow: hidden;
}

.doctor-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.doctor-name {
  font-size: 1.25rem;
  font-weight: 600;
}

.doctor-specialty {
  color: #4b5563;
}

.doctor-availability {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #4b5563;
  font-size: 0.875rem;
}

@media (max-width: 1024px) {
  .service-cards,
  .feature-cards,
  .doctor-cards {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 640px) {
  .service-cards,
  .feature-cards,
  .doctor-cards {
    grid-template-columns: 1fr;
  }
}
</style>

