<template>
  <div class="min-h-screen bg-white">
    <div class="animated-background"></div>
    <!-- Header -->
    <header id="header" class="header animate-on-scroll">
      <div class="flex items-center gap-2">
        <span class="title"><img src="../assets/BiocentralElectronica.JPG" alt=""></span>
      </div>
      <nav class="nav">
        <a href="#" class="nav-link" @click.prevent="scrollTo('.header')">Inicio</a>
        <a href="#" class="nav-link"@click.prevent="scrollTo('.services')">Servicios</a>
        <a href="#" class="nav-link"@click.prevent="scrollTo('.why-us')">Conocenos</a>
        <a href="#" class="nav-link"@click.prevent="scrollTo('.stats')">Contacto</a>
      </nav>
    </header>

    <!-- Hero Section -->
    <section id="hero" class="hero animate-on-scroll">
      <div class="hero-text">
        <h1 class="hero-title">Biocentral<br />Electronica</h1>
        <p class="hero-description">Cuidamos la tecnología que protege vidas, asegurando su rendimiento y confiabilidad para un mejor cuidado de la salud.</p>
        <div class="info-cards">
          <section class="service-features">
            <div class="service-features__container">
              <div v-for="(feature, index) in features" :key="index" class="service-features__item">
                <div class="service-features__icon-container">
                  <img :src="feature.icon" class="service-features__icon" />
                </div>
                <div class="service-features__content">
                  <h3 class="service-features__heading">{{ feature.title }}</h3>
                  <p class="service-features__text" v-html="formatDescription(feature.description)"></p>
                </div>
              </div>
            </div>
          </section>

        
        </div>
        
      </div>
      <div class="hero-image">
        <img src="https://equimed.es/wp-content/uploads/2023/11/mantenimiento_cuidado_equipos_medicos_pic03_20231124_blog_equimed.jpg" alt="Medical Care" />
      </div>
    </section>

    <!-- Services Section -->
    <section id="service" class="services animate-on-scroll">
      <h2 class="section-title">Nuestros Servicios</h2>
      <div class="service-cards">
        <div class="service-card" v-for="service in services" :key="service.title">
          <div class="service-card-inner">
            <div class="service-card-front">
              <img :src="service.image" class="service-image" />
              <h3 class="service-title">{{ service.title }}</h3>
            </div>
            <div class="service-card-back">
              <h3 class="service-title">{{ service.title }}</h3>
              <p class="service-description" v-html="formatDescription(service.description)"></p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Why Us Section -->
    <section id="why" class="why-us animate-on-scroll">
      <h2 class="section-title">¿Por qué nosotros?</h2>
      <div class="feature-cards">
        <div class="feature-card" v-for="about in about" :key="about.title">
          <div class="feature-icon">
            <component :is="about.icon" class="icon" />
          </div>
          <h3 class="feature-title">{{ about.title }}</h3>
          <p class="feature-description">{{ about.description }}</p>
        </div>
      </div>
    </section>

    <!-- Doctors Section -->
    <section class="doctors animate-on-scroll">
      <div class="doctors-header">
        <h2 class="section-title">Vision, Mision y Objetivo general</h2>
      </div>
      <div class="doctor-cards">
        <div class="doctor-card" v-for="doctor in doctors" :key="doctor.name">
          <div class="doctor-info">
            <div>
              <h3 class="doctor-name">{{ doctor.name }}</h3>
              <p class="doctor-specialty">{{ doctor.specialty }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Stats Section -->
    <section id="stats" class="stats animate-on-scroll">
      <div class="stats-cards">
        <div class="stats-card">
          <div class="stats-value"><img src="https://www.svgrepo.com/show/499760/mail-mail-email.svg" alt=""></div>
          <p class="stats-description">biocentralelectronica@gmail.com</p>
        </div>
        <div class="stats-card">
          <div class="stats-value"><img src="https://www.svgrepo.com/show/499767/volume-on.svg" alt=""></div>
          <p class="stats-description">+57 315 600 3326</p>
        </div>
        <div class="stats-card">
          <div class="stats-value"><img src="https://www.svgrepo.com/show/499777/navigation.svg" alt=""></div>
          <p class="stats-description">Neiva, Huila</p>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { Calendar, Star, Activity, Shield, Users, Clock } from 'lucide-vue-next'


const setupIntersectionObserver = () => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('show')
      }
    })
  }, { threshold: 0.1 })

  document.querySelectorAll('.animate-on-scroll').forEach((el) => {
    observer.observe(el)
  })
}

// Add the animation setup to the onMounted hook
onMounted(() => {
  setupIntersectionObserver()
})

// Función para formatear la descripción
const formatDescription = (text) => {
  return text.replace(/\n/g, '<br>')
}

const scrollTo = (sectionRef) => {
  const element = document.querySelector(sectionRef); // Busca el elemento con el selector
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' }); // Scroll suave hacia el elemento
  }
};

const services = [
  {
    title: "Servicio Tecnico",
    description: "Prestamos el servicio de mantenimiento preventivo y correctivo a los equipos de todas las especialidades. Todo nuestro personal posee registro ante el INVIMA y las capacitaciones requeridas para atender sus requerimientos.",
    image: "https://images.pexels.com/photos/305565/pexels-photo-305565.jpeg?auto=compress&cs=tinysrgb&w=600",
    more:"hola esta es la info extra"
  },
  {
    title: "Elaboración de planes de mantenimiento",
    description: `El plan incluye los objetivos, las metas y la programación de actividades.   
    Para esto la empresa cuenta con un software que facilita un mejor manejo
    de la información de los equipos médicos.`,
    image: "https://media.istockphoto.com/id/2148853397/es/foto/ventana-trabajo-en-equipo-y-pizarra-para-lluvia-de-ideas-en-reuniones-gente-de-negocios-con.jpg?b=1&s=612x612&w=0&k=20&c=p9vrM9FGMbqo0HJjhmFW59H4F0LP3AgUBM3vm7hajLM=",
    more:"hola esta es la info extra"
  },
  {
    title: "Asesorías",
    description: `Asesoramos y acompañamos a nuestros clientes en la adquisición de nuevos equipos, adecuaciones físicas, cumplimiento de requisitos de habilitación, creación de hojas de vida de los equipos y el desarrollo de programas de mantenimiento.`,
    image: "https://media.istockphoto.com/id/2159445929/es/foto/negocios-personas-y-redacci%C3%B3n-de-plan-informe-y-papeleo-para-el-discurso-de-pol%C3%ADticos-y.jpg?b=1&s=612x612&w=0&k=20&c=vovHHZYzx2b1EllV-3kNhQpYoK8J1Xau7DPSSmI83zo=",
    more:"hola esta es la info extra"
  },
  {
    title: "Servicios de calidad",
    description: `Biocentral cuenta con simuladores y patrones para la verificación del mantenimiento, buscando garantizar que los equipos funcionen correctamente en momento de entrar nuevamente al servicio después de un preventivo y/o correctivo garantizado la calidad del mismo.`,
    image: "https://images.pexels.com/photos/5996650/pexels-photo-5996650.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    more:"hola esta es la info extra"
  },
  {
    title: "Outsourcing de Mantenimiento",
    description: `Buscamos que las empresas de salud, Clínicas, IPS, Hospitales, Centros de Estética y afines se dediquen a su Core de Negocio. Nos encargamos del departamento de Mantenimiento aumentando la eficiencia y eficacia del servicio técnico dentro de la institución.`,
    image: "https://images.pexels.com/photos/5439439/pexels-photo-5439439.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    more:"hola esta es la info extra"
  },
  {
    title: "Asesoría y Capacitación Técnica en Mantenimiento",
    description: `Prestamos este tipo de servicio con el fin de que cada uno de nuestros clientes garanticen a sus pacientes que son atendidos con equipos e instrumentos en funcionamiento permanente, bajo criterios enfocados en la mejora continua de la calidad`,
    image: "https://images.pexels.com/photos/7698715/pexels-photo-7698715.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    more:"hola esta es la info extra"
  },
]

const features = [
  {
    title: "Honestidad",
    description: " Respetar derechos y cumplir deberes.",
    icon: "https://www.svgrepo.com/show/196250/loyalty.svg",
  },
  {
    title: "Competitividad",
    description: "Efectividad para el crecimiento constante.",
    icon: "https://www.svgrepo.com/show/506985/gen-flag-6.svg",
  },
  {
    title: "Oportunidad",
    description: "Servicios puntuales y respuestas efectivas.",
    icon: "https://www.svgrepo.com/show/418145/check.svg",
  },
  {
    title: "Compromiso",
    description: "Pasión y empoderamiento en nuestras acciones.",
    icon: "https://www.svgrepo.com/show/493428/hands-to-shake-hands.svg",
  },
]

const about = [
  {
    title: "Experiencia en el campo",
    description: "Somos expertos en servicios biomédicos, ofreciendo mantenimiento preventivo y correctivo para equipos médicos, estéticos y odontológicos. Garantizamos soluciones efectivas para el óptimo desempeño de sus equipos.",
    icon: Activity,
  },
  {
    title: "Estandares de Seguridad",
    description: "Cumplimos con estándares y normativas vigentes, priorizando la seguridad, el cumplimiento legal y la confianza de nuestros clientes.",
    icon: Shield,
  },
  {
    title: "Personal Calificado",
    description: "Contamos con un equipo altamente calificado, capacitado constantemente y con amplia experiencia, asegurando resultados confiables y de calidad en cada servicio.",
    icon: Users,
  }
]

const doctors = [
  {
    name: "Misión",
    specialty: "Ofrecer servicios biomédicos de excelencia, apoyados en tecnología y cumplimiento de estándares nacionales.",
    availability: "MON-FRI, 09:00-17:00",
  },
  {
    name: "Visión",
    specialty: "Ser líderes en servicios biomédicos en Colombia para 2030, ampliando nuestra oferta y fortaleciendo la confianza de nuestros clientes.",
    availability: "MON-THU, 10:00-18:00",
  },
  {
    name: "Objetivo",
    specialty: "Ofrecer servicios biomédicos de excelencia, apoyados en tecnología y cumplimiento de estándares nacionales.",
    availability: "TUE-SAT, 09:00-16:00",
  },
]

// Exportamos la función formatDescription para usarla en el template
defineExpose({ formatDescription })

</script>

<style scoped>

.animate-on-scroll {
  opacity: 0;
  transform: translateY(50px);
  transition: opacity 0.6s ease-out, transform 0.6s ease-out;
}

.animate-on-scroll.show {
  opacity: 1;
  transform: translateY(0);
}

*{
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
  font-family: "Rubik", serif;
}

@keyframes scale-up{
  to { scale:1.5; }
}
@keyframes fade-away{
  to { opacity: 0; }
}

header {
  view-timeline: --scroll;
}

header span {
  animation: fade-away both linear;
  animation-timeline: --scroll;
  animation-range:exit 20% exit 90%;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.service-card,
.feature-card,
.doctor-card,
.stats-card {
  transition: transform 0.3s ease-in-out;
}

.service-card:hover,
.feature-card:hover,
.doctor-card:hover,
.stats-card:hover {
  transform: translateY(-5px);
}

@keyframes pop {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.05);
  }
  100% {
    transform: scale(1);
  }
}

.pop-animation {
  animation: pop 0.3s ease-in-out;
}

/* Responsive styles */
@media (max-width: 768px) {
  .nav-links {
    display: flex;
    flex-direction: column;
    position: absolute;
    top: 100%;
    right: 0;
    background-color: white;
    padding: 1rem;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
  }
}

.animated-background {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: -1;
  background: #ffff;
  animation: scale-up-ver-top 0.4s ease-out both;
}

@keyframes scale-up-ver-top {
  0% {
    transform: scaleY(0.4);
    transform-origin: 100% 0%;
  }
  100% {
    transform: scaleY(1);
    transform-origin: 100% 0%;
  }
}

.min-h-screen {
  position: relative;
  z-index: 1;
  background: transparent !important;
}




.stats-value img {
  width: 35px;
}

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
  transition: transform 0.4s ease;
  box-shadow: 10px 7px 20px rgba(0, 0, 0, 0.1);

}

.service-features__item:hover {
  transform: translateY(-2px);
  background:rgb(204, 233, 252);
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
  width: 100%;
  max-height: 150px;

}
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-height: 100px;
  overflow: hidden;
  margin-bottom: 25px;
  min-width: 95vw;
}

.title {
  font-size: 15rem;
  font-weight: bold;
  margin: 0px;
}

.nav {
  display: flex; 
  gap: 2rem; 
}


.nav-link {
  font-size: 1.3rem;
  font-weight: lighter;
  color: #2f343a;
  text-decoration: none;
  transition-duration: 0.4s;
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
  /* padding: 4rem 1rem; */
  max-width: 1200px;
  margin: 0 auto;
  /* background: red; */
}

.hero-text {
  max-width: 500px;
}

.hero-title {
  font-size: 5rem;
  font-weight: bold;
  line-height: 1.2;
  margin: 0px;
  color: #112e5f;
}

.hero-description {
  color: #4b5563;
  font-size: 1.125rem;
  margin-top: 1rem;
}

.info-cards {
  margin-top: 2rem;
  background: #112e5f;
  border-radius: 15px;
  padding: 5px;
  display: flex;
  min-width: 420px;
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
  margin-top: 28px;
  height: auto;
  border-radius: 1rem;
  object-fit: cover;
  max-height: 450px;
  min-height: 550px;
}

/* Services Section */
.services {
  padding: 4rem 1rem;
  max-width: 1200px;
  margin: 0 auto;
  min-width: 430px;
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
  perspective: 1000px;
  height: 400px; /* Adjust as needed */
}

.service-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s;
  transform-style: preserve-3d;
}

.service-card:hover .service-card-inner {
  transform: rotateY(180deg);
}

.service-card-front, .service-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 1.5rem;
  border-radius: 0.5rem;
  box-shadow: 10px 7px 20px rgba(0, 0, 0, 0.1);
}

.service-card-front {
  background-color: #ffffff;
}

.service-card-back {
  background-color: #f3f4f6;
  transform: rotateY(180deg);
  overflow-y: auto;
}

.service-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 0.5rem;
  margin-bottom: 1rem;
}

.service-title {
  font-size: 1.25rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.service-description {
  color: #4b5563;
  font-size: 0.875rem;
  line-height: 1.4;
}


.stats {
  background-color: #111827;
  color: white;
  padding: 4rem 1rem;
  min-width: 430px;
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
  min-width: 430px;
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
  box-shadow: 10px 7px 20px rgba(0, 0, 0, 0.1);

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
  min-width: 430px;
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
  box-shadow: 10px 7px 20px rgba(0, 0, 0, 0.1);
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
  .hero-image{
    display: none;
  }

  .hero-title{
    max-width: 100vw;
    font-size: 4rem;
    text-align: center;
  }
  .stats-cards{
    grid-template-columns: 1fr;
  }
}

@media (max-width: 430px) {
    .service-cards,
    .feature-cards,
    .doctor-cards {
      grid-template-columns: 1fr;
    }
    .hero-image{
      display: none;
    }
    .title{
      display: none;
    }
    .header{
      min-height: 50px;
    }
    .flex{
      display: none;
    }
    .nav{
      gap: 0px;
      justify-content: space-around;
      width: 100%;
    }
    .nav-link{
      display: flex;
      text-align:center ;
      align-items: center;
      justify-content: center;
      justify-items: center;
    }
    .stats-cards{
      grid-template-columns: 1fr;
    }
  }
</style>

