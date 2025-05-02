<template>
  <div class="portfolio" :class="{ 'dark-mode': isDarkMode }">
    <!-- Navigation -->
    <header class="header">
      <div class="logo">
        <span class="logo-text">Portfolio</span>
      </div>
      <nav class="nav">
        <a href="#about" class="nav-link">About</a>
        <a href="#projects" class="nav-link">Projects</a>
        <a href="#skills" class="nav-link">Skills</a>
        <a href="#contact" class="nav-link">Contact</a>
      </nav>
      <!-- Theme Toggle Button -->
      <button
        @click="toggleTheme"
        class="theme-toggle"
        :aria-label="isDarkMode ? 'Switch to light mode' : 'Switch to dark mode'"
      >
        <div class="toggle-icon">
          <div v-if="isDarkMode" class="sun-icon">☀️</div>
          <div v-else class="moon-icon">🌙</div>
        </div>
      </button>
      <button class="menu-toggle" @click="isMenuOpen = !isMenuOpen">
        <div class="hamburger" :class="{ active: isMenuOpen }">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </button>
      <div class="mobile-nav" :class="{ open: isMenuOpen }">
        <a href="#about" class="mobile-nav-link" @click="isMenuOpen = false">About</a>
        <a href="#projects" class="mobile-nav-link" @click="isMenuOpen = false">Projects</a>
        <a href="#skills" class="mobile-nav-link" @click="isMenuOpen = false">Skills</a>
        <a href="#contact" class="mobile-nav-link" @click="isMenuOpen = false">Contact</a>
      </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-content">
        <h1 class="hero-title">
          <span class="greeting">Hello, I'm</span>
          <span class="name">Your Name</span>
        </h1>
        <p class="hero-subtitle">Creative Developer & Designer</p>
        <div class="hero-cta">
          <a href="#projects" class="btn btn-primary">View My Work</a>
          <a href="#contact" class="btn btn-secondary">Get In Touch</a>
        </div>
      </div>
      <div class="hero-visual">
        <div class="shape shape-1"></div>
        <div class="shape shape-2"></div>
        <div class="shape shape-3"></div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="about">
      <div class="section-header">
        <h2 class="section-title">About Me</h2>
        <div class="section-divider"></div>
      </div>
      <div class="about-content">
        <div class="about-image">
          <div class="image-container">
            <div class="image-placeholder">
              <span>Your Photo</span>
            </div>
          </div>
        </div>
        <div class="about-text">
          <p class="about-bio">
            I'm a passionate developer with a creative mindset. I love building beautiful,
            functional applications that solve real-world problems. With a background in design and
            development, I bring a unique perspective to every project.
          </p>
          <div class="about-details">
            <div class="detail-item">
              <span class="detail-icon">🎓</span>
              <div class="detail-content">
                <h3>Education</h3>
                <p>Bachelor's in Computer Science</p>
              </div>
            </div>
            <div class="detail-item">
              <span class="detail-icon">💼</span>
              <div class="detail-content">
                <h3>Experience</h3>
                <p>5+ years in web development</p>
              </div>
            </div>
            <div class="detail-item">
              <span class="detail-icon">🌟</span>
              <div class="detail-content">
                <h3>Interests</h3>
                <p>UI/UX, Animation, Creative Coding</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="projects">
      <div class="section-header">
        <h2 class="section-title">My Projects</h2>
        <div class="section-divider"></div>
      </div>
      <div class="projects-filter">
        <button
          v-for="category in ['All', 'Web', 'Mobile', 'Design']"
          :key="category"
          @click="filterProjects(category)"
          :class="{ active: activeFilter === category }"
          class="filter-btn"
        >
          {{ category }}
        </button>
      </div>
      <div class="projects-grid">
        <div
          v-for="(project, index) in filteredProjects"
          :key="index"
          class="project-card"
          :style="{ 'animation-delay': `${index * 0.1}s` }"
        >
          <div class="project-image">
            <div class="image-placeholder">
              <span>{{ project.title }}</span>
            </div>
          </div>
          <div class="project-info">
            <h3 class="project-title">{{ project.title }}</h3>
            <p class="project-description">{{ project.description }}</p>
            <div class="project-tags">
              <span v-for="(tag, tagIndex) in project.tags" :key="tagIndex" class="tag">
                {{ tag }}
              </span>
            </div>
            <div class="project-links">
              <a :href="project.demoLink" class="project-link" target="_blank">
                <span>Demo</span>
              </a>
              <a :href="project.codeLink" class="project-link" target="_blank">
                <span>Code</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="skills">
      <div class="section-header">
        <h2 class="section-title">My Skills</h2>
        <div class="section-divider"></div>
      </div>
      <div class="skills-content">
        <div class="skills-category" v-for="(category, index) in skills" :key="index">
          <h3 class="category-title">{{ category.name }}</h3>
          <div class="skills-grid">
            <div class="skill-item" v-for="(skill, skillIndex) in category.items" :key="skillIndex">
              <div class="skill-icon">{{ skill.icon }}</div>
              <div class="skill-info">
                <h4 class="skill-name">{{ skill.name }}</h4>
                <div class="skill-level">
                  <div class="level-bar">
                    <div class="level-fill" :style="{ width: `${skill.level}%` }"></div>
                  </div>
                  <span class="level-text">{{ skill.level }}%</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact">
      <div class="section-header">
        <h2 class="section-title">Get In Touch</h2>
        <div class="section-divider"></div>
      </div>
      <div class="contact-content">
        <div class="contact-info">
          <div class="contact-item">
            <div class="contact-icon">✉️</div>
            <div class="contact-text">
              <h3>Email</h3>
              <p>your.email@example.com</p>
            </div>
          </div>
          <div class="contact-item">
            <div class="contact-icon">📱</div>
            <div class="contact-text">
              <h3>Phone</h3>
              <p>+1 (123) 456-7890</p>
            </div>
          </div>
          <div class="contact-item">
            <div class="contact-icon">📍</div>
            <div class="contact-text">
              <h3>Location</h3>
              <p>City, Country</p>
            </div>
          </div>
          <div class="social-links">
            <a href="#" class="social-link" target="_blank">GitHub</a>
            <a href="#" class="social-link" target="_blank">LinkedIn</a>
            <a href="#" class="social-link" target="_blank">Twitter</a>
          </div>
        </div>
        <form class="contact-form" @submit.prevent="submitForm">
          <div class="form-group">
            <label for="name">Name</label>
            <input type="text" id="name" v-model="formData.name" required />
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input type="email" id="email" v-model="formData.email" required />
          </div>
          <div class="form-group">
            <label for="message">Message</label>
            <textarea id="message" v-model="formData.message" rows="5" required></textarea>
          </div>
          <button type="submit" class="btn btn-primary" :disabled="isSubmitting">
            {{ isSubmitting ? 'Sending...' : 'Send Message' }}
          </button>
          <p v-if="formSubmitted" class="form-success">Message sent successfully!</p>
        </form>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="footer-content">
        <p class="copyright">© {{ new Date().getFullYear() }} Your Name. All rights reserved.</p>
        <div class="footer-links">
          <a href="#about" class="footer-link">About</a>
          <a href="#projects" class="footer-link">Projects</a>
          <a href="#skills" class="footer-link">Skills</a>
          <a href="#contact" class="footer-link">Contact</a>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, watch } from 'vue'

// Theme state
const isDarkMode = ref(false)

// Initialize theme from localStorage
onMounted(() => {
  // Check if user has a saved preference
  const savedTheme = localStorage.getItem('theme')

  if (savedTheme) {
    isDarkMode.value = savedTheme === 'dark'
  } else {
    // Check if user prefers dark mode at OS level
    const prefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches
    isDarkMode.value = prefersDark
  }
})

// Toggle theme function
const toggleTheme = () => {
  isDarkMode.value = !isDarkMode.value
}

// Save theme preference when it changes
watch(isDarkMode, (newValue) => {
  localStorage.setItem('theme', newValue ? 'dark' : 'light')
})

// Menu state
const isMenuOpen = ref(false)

// Projects data
const projects = ref([
  {
    title: 'E-Commerce Platform',
    description:
      'A full-featured online store with product catalog, cart, and checkout functionality.',
    tags: ['Vue.js', 'Node.js', 'MongoDB'],
    category: 'Web',
    demoLink: '#',
    codeLink: '#',
  },
  {
    title: 'Task Management App',
    description:
      'A productivity app for managing tasks, projects, and deadlines with team collaboration.',
    tags: ['Vue.js', 'Firebase', 'Tailwind CSS'],
    category: 'Web',
    demoLink: '#',
    codeLink: '#',
  },
  {
    title: 'Fitness Tracker',
    description: 'Mobile application for tracking workouts, nutrition, and health metrics.',
    tags: ['Vue Native', 'GraphQL', 'Chart.js'],
    category: 'Mobile',
    demoLink: '#',
    codeLink: '#',
  },
  {
    title: 'Portfolio Website',
    description: 'Creative portfolio website showcasing projects and skills.',
    tags: ['Vue.js', 'GSAP', 'CSS Animations'],
    category: 'Design',
    demoLink: '#',
    codeLink: '#',
  },
  {
    title: 'Weather Dashboard',
    description: 'Real-time weather information with forecasts and interactive maps.',
    tags: ['Vue.js', 'API Integration', 'D3.js'],
    category: 'Web',
    demoLink: '#',
    codeLink: '#',
  },
  {
    title: 'UI Component Library',
    description: 'Collection of reusable UI components with comprehensive documentation.',
    tags: ['Vue.js', 'Storybook', 'SCSS'],
    category: 'Design',
    demoLink: '#',
    codeLink: '#',
  },
])

// Skills data
const skills = ref([
  {
    name: 'Frontend',
    items: [
      { name: 'HTML/CSS', level: 95, icon: '🌐' },
      { name: 'JavaScript', level: 90, icon: '📜' },
      { name: 'Vue.js', level: 92, icon: '⚡' },
      { name: 'React', level: 85, icon: '⚛️' },
      { name: 'Responsive Design', level: 88, icon: '📱' },
    ],
  },
  {
    name: 'Backend',
    items: [
      { name: 'Node.js', level: 80, icon: '🖥️' },
      { name: 'Express', level: 78, icon: '🚂' },
      { name: 'MongoDB', level: 75, icon: '🍃' },
      { name: 'Firebase', level: 82, icon: '🔥' },
    ],
  },
  {
    name: 'Tools & Others',
    items: [
      { name: 'Git/GitHub', level: 88, icon: '🔄' },
      { name: 'Figma', level: 85, icon: '🎨' },
      { name: 'Webpack', level: 75, icon: '📦' },
      { name: 'Testing', level: 70, icon: '🧪' },
    ],
  },
])

// Project filtering
const activeFilter = ref('All')
const filterProjects = (category) => {
  activeFilter.value = category
}

const filteredProjects = computed(() => {
  if (activeFilter.value === 'All') {
    return projects.value
  }
  return projects.value.filter((project) => project.category === activeFilter.value)
})

// Contact form
const formData = ref({
  name: '',
  email: '',
  message: '',
})
const isSubmitting = ref(false)
const formSubmitted = ref(false)

const submitForm = () => {
  isSubmitting.value = true

  // Simulate form submission
  setTimeout(() => {
    isSubmitting.value = false
    formSubmitted.value = true

    // Reset form
    formData.value = {
      name: '',
      email: '',
      message: '',
    }

    // Hide success message after 3 seconds
    setTimeout(() => {
      formSubmitted.value = false
    }, 3000)
  }, 1500)
}
</script>

<style scoped>
/* Base Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --primary-color: #6c5ce7;
  --secondary-color: #a29bfe;
  --accent-color: #fd79a8;
  --text-color: #2d3436;
  --light-text: #636e72;
  --background: #ffffff;
  --light-bg: #f9f9f9;
  --border-color: #dfe6e9;
  --card-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  --transition: all 0.3s ease;
}

/* Dark Mode Variables */
.dark-mode {
  --primary-color: #8c7ae6;
  --secondary-color: #9c88ff;
  --accent-color: #ff6b81;
  --text-color: #f5f6fa;
  --light-text: #dcdde1;
  --background: #1e272e;
  --light-bg: #2d3436;
  --border-color: #485460;
  --card-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

body {
  font-family:
    'Inter',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    sans-serif;
  color: var(--text-color);
  line-height: 1.6;
  background-color: var(--background);
}

.portfolio {
  overflow-x: hidden;
  background-color: var(--background);
  color: var(--text-color);
  transition:
    background-color 0.3s ease,
    color 0.3s ease;
}

section {
  padding: 100px 20px;
}

.section-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  margin-bottom: 15px;
  position: relative;
  display: inline-block;
  color: var(--text-color);
}

.section-divider {
  height: 4px;
  width: 70px;
  background: linear-gradient(to right, var(--primary-color), var(--accent-color));
  margin: 0 auto;
  border-radius: 2px;
}

.btn {
  display: inline-block;
  padding: 12px 28px;
  border-radius: 30px;
  font-weight: 600;
  text-decoration: none;
  transition: var(--transition);
  cursor: pointer;
  border: none;
  font-size: 1rem;
}

.btn-primary {
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  color: white;
  box-shadow: 0 4px 15px rgba(108, 92, 231, 0.4);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 20px rgba(108, 92, 231, 0.6);
}

.btn-secondary {
  background: transparent;
  color: var(--primary-color);
  border: 2px solid var(--primary-color);
  margin-left: 15px;
}

.btn-secondary:hover {
  background: rgba(108, 92, 231, 0.1);
  transform: translateY(-3px);
}

/* Theme Toggle */
.theme-toggle {
  background: none;
  border: none;
  cursor: pointer;
  margin-right: 15px;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--transition);
  background-color: rgba(108, 92, 231, 0.1);
}

.theme-toggle:hover {
  background-color: rgba(108, 92, 231, 0.2);
}

.toggle-icon {
  font-size: 1.2rem;
}

/* Header & Navigation */
.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  padding: 20px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 1000;
  background-color: var(--background);
  backdrop-filter: blur(10px);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  transition: var(--transition);
}

.dark-mode .header {
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.logo-text {
  font-size: 1.8rem;
  font-weight: 700;
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.nav {
  display: flex;
  gap: 30px;
}

.nav-link {
  text-decoration: none;
  color: var(--text-color);
  font-weight: 500;
  position: relative;
  transition: var(--transition);
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(to right, var(--primary-color), var(--accent-color));
  transition: var(--transition);
}

.nav-link:hover {
  color: var(--primary-color);
}

.nav-link:hover::after {
  width: 100%;
}

.menu-toggle {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
}

.hamburger {
  width: 24px;
  height: 18px;
  position: relative;
  transform: rotate(0deg);
  transition: 0.5s ease-in-out;
}

.hamburger span {
  display: block;
  position: absolute;
  height: 2px;
  width: 100%;
  background: var(--text-color);
  border-radius: 9px;
  opacity: 1;
  left: 0;
  transform: rotate(0deg);
  transition: 0.25s ease-in-out;
}

.hamburger span:nth-child(1) {
  top: 0px;
}

.hamburger span:nth-child(2) {
  top: 8px;
}

.hamburger span:nth-child(3) {
  top: 16px;
}

.hamburger.active span:nth-child(1) {
  top: 8px;
  transform: rotate(135deg);
}

.hamburger.active span:nth-child(2) {
  opacity: 0;
  left: -60px;
}

.hamburger.active span:nth-child(3) {
  top: 8px;
  transform: rotate(-135deg);
}

.mobile-nav {
  display: none;
  position: fixed;
  top: 70px;
  left: 0;
  width: 100%;
  background: var(--background);
  padding: 20px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  transform: translateY(-100%);
  opacity: 0;
  transition: var(--transition);
  z-index: 999;
}

.mobile-nav.open {
  transform: translateY(0);
  opacity: 1;
}

.mobile-nav-link {
  display: block;
  padding: 15px 0;
  text-decoration: none;
  color: var(--text-color);
  font-weight: 500;
  border-bottom: 1px solid var(--border-color);
  transition: var(--transition);
}

.mobile-nav-link:hover {
  color: var(--primary-color);
  padding-left: 10px;
}

/* Hero Section */
.hero {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  padding-top: 70px;
  overflow: hidden;
  background-color: var(--background);
}

.hero-content {
  max-width: 600px;
  text-align: center;
  z-index: 2;
}

.hero-title {
  font-size: 3.5rem;
  margin-bottom: 20px;
  line-height: 1.2;
  color: var(--text-color);
}

.greeting {
  display: block;
  font-weight: 400;
  font-size: 1.8rem;
  margin-bottom: 10px;
  color: var(--light-text);
}

.name {
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  font-weight: 800;
}

.hero-subtitle {
  font-size: 1.5rem;
  margin-bottom: 40px;
  color: var(--light-text);
}

.hero-cta {
  display: flex;
  justify-content: center;
  gap: 10px;
}

.hero-visual {
  position: absolute;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.shape {
  position: absolute;
  border-radius: 50%;
  filter: blur(60px);
  opacity: 0.5;
}

.shape-1 {
  width: 300px;
  height: 300px;
  background: var(--primary-color);
  top: 20%;
  right: 15%;
  animation: float 8s ease-in-out infinite;
}

.shape-2 {
  width: 200px;
  height: 200px;
  background: var(--accent-color);
  bottom: 15%;
  left: 10%;
  animation: float 6s ease-in-out infinite 1s;
}

.shape-3 {
  width: 150px;
  height: 150px;
  background: var(--secondary-color);
  top: 30%;
  left: 20%;
  animation: float 7s ease-in-out infinite 0.5s;
}

@keyframes float {
  0% {
    transform: translateY(0) rotate(0deg);
  }
  50% {
    transform: translateY(-20px) rotate(5deg);
  }
  100% {
    transform: translateY(0) rotate(0deg);
  }
}

/* About Section */
.about {
  background-color: var(--light-bg);
}

.about-content {
  display: flex;
  gap: 60px;
  max-width: 1200px;
  margin: 0 auto;
  align-items: center;
}

.about-image {
  flex: 1;
}

.image-container {
  position: relative;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: var(--card-shadow);
}

.image-placeholder {
  width: 100%;
  aspect-ratio: 1;
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: 600;
  font-size: 1.2rem;
}

.about-text {
  flex: 1;
}

.about-bio {
  font-size: 1.1rem;
  margin-bottom: 30px;
  color: var(--light-text);
}

.about-details {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}

.detail-item {
  display: flex;
  align-items: flex-start;
  gap: 15px;
}

.detail-icon {
  font-size: 1.8rem;
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.detail-content h3 {
  font-size: 1.1rem;
  margin-bottom: 5px;
  color: var(--text-color);
}

.detail-content p {
  color: var(--light-text);
}

/* Projects Section */
.projects-filter {
  display: flex;
  justify-content: center;
  gap: 15px;
  margin-bottom: 40px;
  flex-wrap: wrap;
}

.filter-btn {
  padding: 8px 20px;
  border: none;
  background: transparent;
  border-radius: 30px;
  cursor: pointer;
  font-weight: 500;
  transition: var(--transition);
  color: var(--light-text);
}

.filter-btn:hover {
  color: var(--primary-color);
}

.filter-btn.active {
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  color: white;
  box-shadow: 0 4px 10px rgba(108, 92, 231, 0.3);
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 30px;
  max-width: 1200px;
  margin: 0 auto;
}

.project-card {
  border-radius: 15px;
  overflow: hidden;
  background: var(--background);
  box-shadow: var(--card-shadow);
  transition: var(--transition);
  animation: fadeInUp 0.5s forwards;
  opacity: 0;
  transform: translateY(30px);
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.project-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
}

.project-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.project-info {
  padding: 25px;
}

.project-title {
  font-size: 1.3rem;
  margin-bottom: 10px;
  color: var(--text-color);
}

.project-description {
  color: var(--light-text);
  margin-bottom: 15px;
  font-size: 0.95rem;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 20px;
}

.tag {
  padding: 5px 12px;
  background-color: var(--light-bg);
  border-radius: 20px;
  font-size: 0.8rem;
  color: var(--light-text);
}

.project-links {
  display: flex;
  gap: 15px;
}

.project-link {
  text-decoration: none;
  color: var(--primary-color);
  font-weight: 600;
  font-size: 0.9rem;
  transition: var(--transition);
}

.project-link:hover {
  color: var(--accent-color);
}

/* Skills Section */
.skills {
  background-color: var(--light-bg);
}

.skills-content {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  gap: 50px;
}

.category-title {
  font-size: 1.5rem;
  margin-bottom: 25px;
  position: relative;
  display: inline-block;
  padding-bottom: 10px;
  color: var(--text-color);
}

.category-title::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 40px;
  height: 3px;
  background: linear-gradient(to right, var(--primary-color), var(--accent-color));
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 25px;
}

.skill-item {
  background: var(--background);
  border-radius: 12px;
  padding: 20px;
  box-shadow: var(--card-shadow);
  display: flex;
  align-items: center;
  gap: 15px;
  transition: var(--transition);
}

.skill-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}

.skill-icon {
  font-size: 1.8rem;
}

.skill-info {
  flex: 1;
}

.skill-name {
  margin-bottom: 8px;
  font-size: 1rem;
  color: var(--text-color);
}

.skill-level {
  display: flex;
  align-items: center;
  gap: 10px;
}

.level-bar {
  flex: 1;
  height: 6px;
  background-color: var(--light-bg);
  border-radius: 3px;
  overflow: hidden;
}

.level-fill {
  height: 100%;
  background: linear-gradient(to right, var(--primary-color), var(--accent-color));
  border-radius: 3px;
}

.level-text {
  font-size: 0.8rem;
  color: var(--light-text);
  font-weight: 600;
}

/* Contact Section */
.contact-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  max-width: 1200px;
  margin: 0 auto;
}

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.contact-item {
  display: flex;
  align-items: flex-start;
  gap: 20px;
}

.contact-icon {
  font-size: 2rem;
  background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.contact-text h3 {
  font-size: 1.2rem;
  margin-bottom: 5px;
  color: var(--text-color);
}

.contact-text p {
  color: var(--light-text);
}

.social-links {
  display: flex;
  gap: 15px;
  margin-top: 20px;
}

.social-link {
  text-decoration: none;
  color: var(--text-color);
  font-weight: 500;
  transition: var(--transition);
}

.social-link:hover {
  color: var(--primary-color);
}

.contact-form {
  background: var(--background);
  padding: 40px;
  border-radius: 15px;
  box-shadow: var(--card-shadow);
}

.form-group {
  margin-bottom: 25px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: 500;
  color: var(--text-color);
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 12px 15px;
  border: 1px solid var(--border-color);
  border-radius: 8px;
  font-family: inherit;
  font-size: 1rem;
  transition: var(--transition);
  background-color: var(--background);
  color: var(--text-color);
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--primary-color);
  box-shadow: 0 0 0 3px rgba(108, 92, 231, 0.1);
}

.form-success {
  color: #2ecc71;
  margin-top: 15px;
  font-weight: 500;
}

/* Footer */
.footer {
  background-color: var(--light-bg);
  padding: 40px 20px;
  text-align: center;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
}

.copyright {
  margin-bottom: 20px;
  color: var(--light-text);
}

.footer-links {
  display: flex;
  justify-content: center;
  gap: 30px;
}

.footer-link {
  text-decoration: none;
  color: var(--light-text);
  transition: var(--transition);
}

.footer-link:hover {
  color: var(--primary-color);
}

/* Responsive Design */
@media (max-width: 1024px) {
  .about-content {
    flex-direction: column;
    text-align: center;
  }

  .about-image {
    max-width: 400px;
    margin: 0 auto;
  }

  .detail-item {
    justify-content: center;
  }

  .category-title {
    text-align: center;
    display: block;
  }

  .category-title::after {
    left: 50%;
    transform: translateX(-50%);
  }

  .contact-content {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 768px) {
  section {
    padding: 80px 20px;
  }

  .nav {
    display: none;
  }

  .menu-toggle {
    display: block;
  }

  .mobile-nav {
    display: block;
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .hero-subtitle {
    font-size: 1.2rem;
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }

  .contact-info {
    text-align: center;
  }

  .contact-item {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .social-links {
    justify-content: center;
  }
}

@media (max-width: 480px) {
  .hero-cta {
    flex-direction: column;
  }

  .btn-secondary {
    margin-left: 0;
    margin-top: 15px;
  }

  .section-title {
    font-size: 2rem;
  }

  .theme-toggle {
    margin-right: 5px;
  }
}
</style>
