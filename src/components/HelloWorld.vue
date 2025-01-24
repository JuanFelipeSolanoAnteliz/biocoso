<template>
  <div class="min-h-screen bg-white">
      <!-- intro section -->
      <section id='intro' class='section section-main active' v-show="showMainSection">
      <div class='container-fluid'>
        <div class='v-align'>
          <div class='inner'>
            <div class='intro-text'>
                <img class="imgLogoIntro" src="../assets/BiocentralElectronica-removebg.png" alt="" srcset="">
              <div class='intro-btns'>
                <a href='#about' class='btn-custom section-toggle' data-section='about' @click.prevent="toggleMainSection">
                  Descubre más
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  <div v-show="!showMainSection">
    <!-- Header -->
    <header id="header" class="header animate-on-scroll">
      <div class="flex items-center gap-2">
        <span class="title"><img src="../assets/BiocentralElectronica.JPG" alt=""></span>
      </div>
      <nav class="nav">
        <a href="#" class="nav-link" @click.prevent="scrollTo('.header')">Inicio</a>
        <a href="#" class="nav-link" @click.prevent="scrollTo('.services')">Servicios</a>
        <a href="#" class="nav-link" @click.prevent="scrollTo('.why-us')">Conocenos</a>
        <a href="#" class="nav-link" @click.prevent="scrollTo('.stats')">Contacto</a>
      </nav>
    </header>

    <!-- Hero Section -->
    <section id="hero" class="hero animate-on-scroll">
      <div class="hero-text">
        <h1 class="hero-title">Biocentral<br />Electronica</h1>
        <div class="flex2">
        <span class="title"><img src="../assets/BiocentralElectronica.JPG" alt=""></span>
      </div>
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
      <h2 id="blanco" class="section-title">Nuestros Servicios</h2>
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
      <h2  class="section-title">¿Por qué nosotros?</h2>
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
        <h2 class="section-title">Visión, Misión y Objetivo general</h2>
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
          <div class="stats-value"><img src="../assets/mail-free-material-svgrepo-com.svg" alt=""></div>
          <p class="stats-description">biocentralelectronica@gmail.com</p>
        </div>
        <div class="stats-card">
          <div class="stats-value"><img src="https://www.svgrepo.com/show/432064/whatsapp.svg" alt=""></div>
          <p class="stats-description">+57 315 600 3326</p>
          <p class="stats-description">+57 315 076 3333</p>
        </div>
        <div class="stats-card">
          <div class="stats-value"><img src="https://www.svgrepo.com/show/526085/phone-calling.svg" alt=""></div>
          <p class="stats-description">Fijo</p>
          <p class="stats-description">+57 608 849 9505</p>
        </div>
        <div class="stats-card">
          <div class="stats-value"><img src="../assets/location-svgrepo-com.svg" alt=""></div>
          <p class="stats-description">Neiva, Huila</p>
        </div>
      </div>
    </section>
  </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import { Calendar, Star, Activity, Shield, Users, Clock } from 'lucide-vue-next'

const showMainSection = ref(true)

const toggleMainSection = () => {
  showMainSection.value = !showMainSection.value
}

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
    image: "https://avamedicalcolombia.com/wp-content/uploads/2019/07/DSC_0050.jpg",
    more:"hola esta es la info extra"
  },
  {
    title: "Elaboración de planes de mantenimiento",
    description: `El plan incluye los objetivos, las metas y la programación de actividades.   
    Para esto la empresa cuenta con un software que facilita un mejor manejo
    de la información de los equipos médicos.`,
    image: "https://images.pexels.com/photos/9574405/pexels-photo-9574405.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
    more:"hola esta es la info extra"
  },
  {
    title: "Asesorías",
    description: `Asesoramos y acompañamos a nuestros clientes en la adquisición de nuevos equipos, adecuaciones físicas, cumplimiento de requisitos de habilitación, creación de hojas de vida de los equipos y el desarrollo de programas de mantenimiento.`,
    image: "https://images.pexels.com/photos/3183197/pexels-photo-3183197.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1",
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
    image: "https://equimed.es/wp-content/uploads/2023/11/mantenimiento_cuidado_equipos_medicos_pic02_20231124_blog_equimed.jpg",
    more:"hola esta es la info extra"
  },
  {
    title: "Asesoría y Capacitación Técnica en Mantenimiento",
    description: `Prestamos este tipo de servicio con el fin de que cada uno de nuestros clientes garanticen a sus pacientes que son atendidos con equipos e instrumentos en funcionamiento permanente, bajo criterios enfocados en la mejora continua de la calidad`,
    image: "https://images.pexels.com/photos/305565/pexels-photo-305565.jpeg?auto=compress&cs=tinysrgb&w=600",
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

.doctors{
  display:flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

#service{
  margin-top:10px;
  background: #06173d;
  width: 100vw;
  text-align: center;
}

.animate-on-scroll {
  opacity: 0;
  transform: translateY(0px);
  transition: opacity 0.6s ease-out, transform 0.6s ease-out;
  margin: 0px;
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
  /* background: red; */
  width: 100%;
  margin: 0px;
  padding: 0px;
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
  padding-right:50px ;
}

.title {
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
  padding: 2rem 6rem;
  margin: 0 auto;
  min-width: 430px;
  max-width:100% ;
}

.section-title {
  font-size: 2rem;
  font-weight: bold;
  margin-bottom: 2rem;

}

#blanco{
  color:#fff;
}

.service-cards {
  display: grid;
  grid-template-columns: repeat(3, minmax(300px, 1fr)); /* Forzamos 3 columnas */
  grid-template-rows: repeat(2, auto); /* 2 filas */
  gap: 2rem;
  justify-content: center;
  align-items: start; /* Alinea las tarjetas al inicio para mantener consistencia */
  margin: 0 auto;
}

.service-card {
  perspective: 1000px;
  height: 450px;
  background: #06173d;
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
  height: 300px;
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
  background-color:#fff;
  color: #0000;
  padding:  2rem;
  min-width: 430px;
  min-height: 100px;
}

.stats-cards {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
  min-height:10px ;
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
  color: #000000;
}

.why-us {
  padding: 4rem 1rem;
  max-width: 1200px;
  margin: 0 auto;
  min-width: 430px;
  text-align: center;
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
  padding: 4rem 8rem;
  margin: 0 auto;
  min-width: 430px;
  background-color: #06173d;
}

.doctors-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 3rem;
  color:white;
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

.flex2{
  display: none;
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
  .doctors{
    padding: 2rem 2rem;
  }
  .seccion-title{
    margin-bottom: 0px;
  }

  .service-features{
    width: 100%;
  }
  
}




@media (max-width: 768px) {

.doctors {
    margin: 0 ;
    min-width: 430px;
    background-color: #06173d;
  }
.doctors-header{
  margin-bottom: 0rem;
}
.section-title{
  margin: 0px;
  margin-bottom: 20px;
}

.doctors-header{
  margin-bottom: 0px;
}

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
.title{
  background:red ;
  font-size: 0rem;
}
.hero{
  grid-template-columns: 1fr;
  gap:0;
  display: flex;
  justify-content: center;
}


.hero-title{
  display: none;
  text-align: center;
}

.flex{
  display: none;
}

.flex2{
  display: block;
}

.hero-description{
  text-align: center;
}

.hero-image{
  display: none;
}
}

.imgLogoIntro{
  width: 70vw;
  position: relative;
  top: 40px;
  min-width: 90vw;
  margin-bottom: 30px;
}



.section-main {
  background-size: cover;
  background-image: url(../assets/DALLE_2025-01-19_14.27.50_-_A_modern_empty_operating_room_in_a_wide_horizontal_layout_with_surgical_lights_on_the_ceiling_and_an_adjustable_operating_table_in_the_center._The_de.webp);
  background-color: rgba(255, 255, 255, 0.3);
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  filter: blur(.1px);
  position: relative;
  overflow: hidden;
}

.section-main:before {
  content: ' ';
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background-image: url(https://cdn.discordapp.com/attachments/1330014896540352522/1330619812648325232/DALLE_2025-01-19_14.27.50_-_A_modern_empty_operating_room_in_a_wide_horizontal_layout_with_surgical_lights_on_the_ceiling_and_an_adjustable_operating_table_in_the_center._The_de.webp?ex=678ea3c5&is=678d5245&hm=f849717fa815823a6a4cc20e3fc5ef39d0f376d0cad2fef508c71c186780b612&);
  background-size: cover; 
  background-position: center; 
  filter: blur(1px);
  z-index: -1;
}

.section-main .container-fluid {
  position: relative;
  z-index: 1;
}

.imgMissionVisison{
	width: 10%;
}

.intro-text{
	padding:20px;
	text-align:center;
  justify-content: center;
  align-items: center;
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 98vw;
  z-index: 1;
  position: relative;
}
.intro-text > h1{
	margin:0;
	color:#FFF;
	text-transform:uppercase;
	font-weight:900;
	letter-spacing:8px;
	font-size:78px;
}
.intro-text > p{
	font-size:18px;
	color:#FFF;
	color:rgba(255,255,255,.8);
	margin-top:15px;
	margin-bottom:0;
	font-weight:300;
	font-style:italic;
	letter-spacing:2px;
}
.intro-text > .intro-btns{
  /* background:red; */
  display: flex;
  width: 300px;
  height: 100%;
  justify-content: center;
  align-items: center;
	/* margin-top:45px; */
  position: relative;
  max-height:100px;
}

a.btn-custom {
  color: #FFF;
  text-decoration: none;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(74, 99, 145, 0.699);
  padding: 16px 16px;
  width: 500px; /* Ancho responsive para pantallas pequeñas */
  max-width: 310px; /* Límite máximo de ancho */
  min-height: 50px; /* Altura mínima */
  border-style: solid;
  border-width: 1.5px;
  border-color: rgb(253, 253, 253);
  letter-spacing: 4px;
  text-transform: uppercase;
  text-decoration: none;
  position: absolute;
  top: 0px;
  left: 16px;
}

.btn-custom:after{
	content: ' ';
	position:absolute;
	top:0;
	left:-10px;
	right:-10px;
	bottom:0;
	-webkit-transform:rotate(-4deg);
	-moz-transform:rotate(-4deg);
	-ms-transform:rotate(-4deg);
	-o-transform:rotate(-4deg);
	transform:rotate(-4deg);
	z-index:-1;
	opacity:0;
	visibility:hidden;
	background:#06173d;
	-webkit-transition:all .3s cubic-bezier(.785,.135,.15,.86);
	-moz-transition:all .3s cubic-bezier(.785,.135,.15,.86);
	transition:all .3s cubic-bezier(.785,.135,.15,.86);
}
.btn-custom:before{
	content: ' ';
	position:absolute;
	top:0;
	left:0;
	right:0;
	bottom:0;
	z-index:2;
	border:solid 1px #FFF;
	border-color:rgba(255,255,255,.8);
} 

.btn-custom:hover:after{
	opacity:1;
	visibility:visible;
}

.btn-custom.btn-color:after{
	background:#303F9F;
}

.btn-custom.btn-color:hover:after{
	opacity:.4;
}

.btn-custom.btn-color{
	color:#06173d;
}

.btn-custom.btn-color > span:before,
.btn-custom.btn-color > span:after{
	background:#06173d;
}
.btn-custom.btn-color:before{
	border-color:#06173d;
}

body.section-switching .animation-block{
	position:absolute;
	left:0;
	height:0%;
	width:100%;
	background:#E0E0E0;
	z-index:199;
}
body.section-switching.down .animation-block{
	-webkit-animation: anim-down 2.5s cubic-bezier(.785,.135,.15,.86);
	-moz-animation: anim-down 2.5s cubic-bezier(.785,.135,.15,.86);
	animation: anim-down 2.5s cubic-bezier(.785,.135,.15,.86);
}
body.section-switching.up .animation-block{
	-webkit-animation: anim-up 2.5s cubic-bezier(.785,.135,.15,.86);
	-moz-animation: anim-up 2.5s cubic-bezier(.785,.135,.15,.86);
	animation: anim-up 2.5s cubic-bezier(.785,.135,.15,.86);
}
@-webkit-keyframes anim-down{
	0%{
		bottom:0;
		height:0;
	}
	45%{
		bottom:0;
		height:100%;
	}
	55%{
		bottom:0;
		height:100%;
	}
	100%{
		height:0%;
		top:0;
	}
}
@-moz-keyframes anim-down{
	0%{
		bottom:0;
		height:0;
	}
	45%{
		bottom:0;
		height:100%;
	}
	55%{
		bottom:0;
		height:100%;
	}
	100%{
		height:0%;
		top:0;
	}
}
@keyframes anim-down{
	0%{
		bottom:0;
		height:0;
	}
	45%{
		bottom:0;
		height:100%;
	}
	55%{
		bottom:0;
		height:100%;
	}
	100%{
		height:0%;
		top:0;
	}
}
@-webkit-keyframes anim-up{
	0%{
		top:0;
		height:0;
	}
	45%{
		top:0;
		height:100%;
	}
	55%{
		top:0;
		height:100%;
	}
	55.1%{
		bottom:0;
		top:auto;
		height:100%;
	}
	100%{
		height:0%;
		bottom:0;
		top:auto;
	}
}
@-moz-keyframes anim-up{
	0%{
		top:0;
		height:0;
	}
	45%{
		top:0;
		height:100%;
	}
	55%{
		top:0;
		height:100%;
	}
	55.1%{
		bottom:0;
		top:auto;
		height:100%;
	}
	100%{
		height:0%;
		bottom:0;
		top:auto;
	}
}
@keyframes anim-up{
	0%{
		top:0;
		height:0;
	}
	45%{
		top:0;
		height:100%;
	}
	55%{
		top:0;
		height:100%;
	}
	55.1%{
		bottom:0;
		top:auto;
		height:100%;
	}
	100%{
		height:0%;
		bottom:0;
		top:auto;
	}
}
.section-main{
	padding:0;
}
.section-main, .section-main > .container-fluid{
	height:100%;
	width:100%;
}
.v-align{
	display:table;
	height:100%;
	width:100%;
}
.v-align > .inner{
	height:100%;
	width:100%;
	display:table-cell;
	vertical-align:middle;
}

@media (max-width: 1024px) {
  .service-cards,
  .feature-cards,
  .doctor-cards {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 640px) {
  .service-features__container {
    grid-template-columns: 1fr;
  }
  .hero-title{
  display: none;
  font-size: 3rem;
}
.flex2{
  display: block;
}

}

@media (max-width: 430px) {

.min-h-screen {
  width: 100%;
  overflow-x: hidden;
  padding: 0;
  margin: 0;
}
.doctors {
  margin: 0 auto;
  min-width: 430px;
  background-color: #06173d;
}
.hero-description{
  text-align: center;
}
.header {
  padding-right:0px;
  margin-bottom: 0px;
}

.flex2{
  display: block;
}

.service-cards,
.feature-cards,
.doctor-cards {
  grid-template-columns: 1fr;
}
.info-cards{
  min-width: 90px;
}
.hero-text{
  width: 96vw;
  margin-left: 8px;
}
.hero-title{
  display: none;
  font-size: 3rem;
}
.service-features__item{
  height: 90px;
}
.services{
  min-width: 100vw;
  padding: 2rem ;
}

.service-card-front {
  /* background: red; */
  padding: 0 1rem;

}
.service-image{
  height: 250px;
}


.why-us{
  padding: 2rem .5rem;
  min-width: 90px;
}
.doctors{
  min-width: 90px;
}

.doctors-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color:white;
  margin:0;
}

.hero-image{
  display: none;
}
.title{
  
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
  font-size: 1rem;
}
.stats-cards{
  grid-template-columns: 1fr;
}
.stats{
  min-width: 90px;
}

.intro-text > .intro-btns{
  /* background:red; */
  max-height:250px;

}

a.btn-custom{
  /* background-color: red; */
  left:85px;
  width: 150px;
  top:190px;
  bottom: 0px;
  font-size: 10px;
  padding: 0;
}

.imgLogoIntro{
  top:140px;
  width: 450px;
}
.flex2{
  display: block;
}

}
</style>

