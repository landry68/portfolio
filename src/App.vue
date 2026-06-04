<template>
  <div id="app">
    <!-- NAV -->
    <nav class="navbar" :class="{ scrolled: scrolled }">
      <div class="nav-inner">
        <span class="nav-logo">SL</span>
        <ul class="nav-links">
          <li><a href="#home" @click.prevent="scrollTo('home')">Home</a></li>
          <li><a href="#about" @click.prevent="scrollTo('about')">About</a></li>
          <li><a href="#skills" @click.prevent="scrollTo('skills')">Skills</a></li>
          <li><a href="#projects" @click.prevent="scrollTo('projects')">Projects</a></li>
          <li><a href="#education" @click.prevent="scrollTo('education')">Education</a></li>
          <li><a href="#contact" @click.prevent="scrollTo('contact')">Contact</a></li>
        </ul>
        <button class="hamburger" @click="menuOpen = !menuOpen">☰</button>
      </div>
      <div class="mobile-menu" v-if="menuOpen">
        <a v-for="link in navLinks" :key="link.id" :href="'#'+link.id" @click.prevent="scrollTo(link.id); menuOpen=false">{{ link.label }}</a>
      </div>
    </nav>

    <!-- HOME -->
    <section id="home" class="hero">
      <div class="paper-texture"></div>
      <div class="hero-content">
        <div class="hero-headline">
          <div class="hero-text-block">
            <p class="hero-greeting">Hello, I'm</p>
            <h1 class="hero-name">Shema Landry</h1>
            <div class="hero-title">
              <span class="typing-text">{{ displayedTitle }}</span><span class="cursor">|</span>
            </div>
          </div>
          <div class="profile-wrap">
            <div class="profile-circle">
              <img src="/src/assets/bb.jpg" alt="Shema Landry" class="profile-pic" />
              <div class="profile-initials">SL</div>
            </div>
            <div class="profile-ring"></div>
          </div>
        </div>
        <p class="hero-tagline">
          I build websites and apps that actually work.<br>
          No fluff, just solid design and code.
        </p>
        <div class="hero-cta">
          <button class="btn-primary" @click="scrollTo('projects')">View My Work</button>
          <button class="btn-outline" @click="scrollTo('contact')">Let's Talk</button>
        </div>
        <div class="hero-scroll-hint" @click="scrollTo('about')">
          <span>Scroll to explore</span>
          <div class="scroll-line"></div>
        </div>
      </div>
      <div class="ink-splash left"></div>
      <div class="ink-splash right"></div>
    </section>

    <!-- ABOUT -->
    <section id="about" class="section about-section">
      <div class="section-inner">
        <div class="section-label">01 — About Me</div>
        <div class="about-grid">
          <div class="about-text">
            <h2 class="section-heading">Building things<br><em>that actually work</em></h2>
            <p>
              I'm a developer and designer from Rwanda. I like building things that work well and don't waste your time.
              Good design shouldn't be complicated — it should just make sense.
            </p>
            <p>
              Started learning code out of curiosity, now it's what I do. I enjoy figuring out how to solve problems with code,
              and making interfaces that people don't hate using. Pretty straightforward stuff.
            </p>
            <p>
              Outside of work, I'm probably experimenting with something, reading about design, or just learning whatever looks interesting.
            </p>
            <div class="about-stats">
              <div class="stat">
                <span class="stat-num">3+</span>
                <span class="stat-label">Years Building</span>
              </div>
              <div class="stat">
                <span class="stat-num">20+</span>
                <span class="stat-label">Projects Done</span>
              </div>
              <div class="stat">
                <span class="stat-num">100%</span>
                <span class="stat-label">Dedicated</span>
              </div>
            </div>
          </div>
          <div class="about-visual">
            <div class="about-card">
              <div class="card-ink-border"></div>
              <div class="about-avatar-large">
                <img src="/src/assets/bb.jpg" alt="Shema Landry" class="about-profile-pic" />
                <div class="avatar-text">SL</div>
              </div>
              <div class="about-card-info">
                <div class="info-row"><span class="info-label">Name</span><span class="info-val">Shema Landry</span></div>
                <div class="info-row"><span class="info-label">Role</span><span class="info-val">Developer & Designer</span></div>
                <div class="info-row"><span class="info-label">Location</span><span class="info-val">Rwanda</span></div>
                <div class="info-row"><span class="info-label">Status</span><span class="info-val available">Available for work</span></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- SKILLS -->
    <section id="skills" class="section skills-section">
      <div class="section-inner">
        <div class="section-label">02 — Skills & Tools</div>
        <h2 class="section-heading">What I work with</h2>
        <div class="skills-grid">
          <div class="skill-category" v-for="cat in skillCategories" :key="cat.title">
            <div class="skill-cat-icon">{{ cat.icon }}</div>
            <h3 class="skill-cat-title">{{ cat.title }}</h3>
            <div class="skill-list">
              <div class="skill-item" v-for="skill in cat.skills" :key="skill.name">
                <div class="skill-header">
                  <span class="skill-name">{{ skill.name }}</span>
                  <span class="skill-pct">{{ skill.level }}%</span>
                </div>
                <div class="skill-bar">
                  <div class="skill-fill" :style="{ width: skill.level + '%' }"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- PROJECTS -->
    <section id="projects" class="section projects-section">
      <div class="section-inner">
        <div class="section-label">03 — Projects</div>
        <h2 class="section-heading">Things I've built</h2>
        <div class="projects-grid">
          <div class="project-card" v-for="(proj, i) in projects" :key="i" @mouseenter="proj.hovered=true" @mouseleave="proj.hovered=false">
            <div class="project-num">{{ String(i+1).padStart(2,'0') }}</div>
            <div class="project-top">
              <div class="project-icon">{{ proj.icon }}</div>
              <div class="project-links" v-if="proj.links">
                <a v-if="proj.links.demo" :href="proj.links.demo" class="proj-link" target="_blank" title="Live demo">↗</a>
                <a v-if="proj.links.github" :href="proj.links.github" class="proj-link" target="_blank" title="GitHub">⌥</a>
              </div>
            </div>
            <h3 class="project-title">{{ proj.title }}</h3>
            <p class="project-desc">{{ proj.desc }}</p>
            <div class="project-tags">
              <span class="tag" v-for="tag in proj.tags" :key="tag">{{ tag }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- EDUCATION -->
    <section id="education" class="section education-section">
      <div class="section-inner">
        <div class="section-label">04 — Education</div>
        <h2 class="section-heading">My academic journey</h2>
        <div class="timeline">
          <div class="timeline-item" v-for="(edu, i) in education" :key="i">
            <div class="timeline-dot"></div>
            <div class="timeline-line" v-if="i < education.length - 1"></div>
            <div class="timeline-card">
              <div class="timeline-badge">{{ edu.badge }}</div>
              <div class="timeline-content">
                <span class="timeline-period">{{ edu.period }}</span>
                <h3 class="timeline-school">{{ edu.school }}</h3>
                <p class="timeline-level">{{ edu.level }}</p>
                <p class="timeline-desc">{{ edu.desc }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CONTACT -->
    <section id="contact" class="section contact-section">
      <div class="section-inner">
        <div class="section-label">05 — Contact</div>
        <h2 class="section-heading">Let's build<br><em>something real</em></h2>
        <p class="contact-sub">
          Got a project or just want to chat? Drop me a message. I'm always open to interesting work.
        </p>
        <div class="contact-grid">
          <div class="contact-form-wrap">
            <div class="contact-form">
              <div class="form-group">
                <label>Your Name</label>
                <input type="text" v-model="form.name" placeholder="John Doe" />
              </div>
              <div class="form-group">
                <label>Email Address</label>
                <input type="email" v-model="form.email" placeholder="john@example.com" />
              </div>
              <div class="form-group">
                <label>Message</label>
                <textarea v-model="form.message" placeholder="Tell me about your project..." rows="5"></textarea>
              </div>
              <button class="btn-primary full" @click="submitForm">
                {{ formSent ? '✓ Message Sent!' : 'Send Message' }}
              </button>
            </div>
          </div>
          <div class="contact-info">
            <div class="contact-block">
              <div class="contact-icon">✉</div>
              <div>
                <p class="ci-label">Email</p>
                <p class="ci-val">shemalandry@gmail.com</p>
              </div>
            </div>
            <div class="contact-block">
              <div class="contact-icon"></div>
              <div>
                <p class="ci-label">Location</p>
                <p class="ci-val">Kigali, Rwanda</p>
              </div>
            </div>
            <div class="contact-block">
              <div class="contact-icon"></div>
              <div>
                <p class="ci-label">LinkedIn</p>
                <p class="ci-val">linkedin.com/in/shemalendry</p>
              </div>
            </div>
            <div class="contact-block">
              <div class="contact-icon"></div>
              <div>
                <p class="ci-label">GitHub</p>
                <p class="ci-val">github.com/shemalendry</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="footer">
      <div class="footer-inner">
        <span class="footer-name">Shema Landry</span>
        <span class="footer-copy">© {{ new Date().getFullYear() }} — Crafted with care & coffee ☕</span>
        <span class="footer-back" @click="scrollTo('home')">Back to top ↑</span>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      scrolled: false,
      menuOpen: false,
      formSent: false,
      form: { name: '', email: '', message: '' },
      navLinks: [
        { id: 'home', label: 'Home' },
        { id: 'about', label: 'About' },
        { id: 'skills', label: 'Skills' },
        { id: 'projects', label: 'Projects' },
        { id: 'education', label: 'Education' },
        { id: 'contact', label: 'Contact' },
      ],
      titles: [
        'Vue.js Developer',
        'UI/UX Designer',
        'Frontend Engineer',
        'JavaScript Enthusiast',
        'Digital Craftsman',
      ],
      currentTitleIndex: 0,
      displayedTitle: '',
      typingForward: true,
      typingIndex: 0,
      skillCategories: [
        {
          icon: '',
          title: 'Frontend Development',
          skills: [
            { name: 'Vue.js', level: 90 },
            { name: 'JavaScript (ES6+)', level: 88 },
            { name: 'HTML5 & CSS3', level: 95 },
            { name: 'Responsive Design', level: 92 },
          ],
        },
        {
          icon: '',
          title: 'Design',
          skills: [
            { name: 'UI/UX Design', level: 85 },
            { name: 'Figma', level: 80 },
            { name: 'Typography', level: 88 },
            { name: 'Color Theory', level: 82 },
          ],
        },
        {
          icon: '',
          title: 'Tools & Workflow',
          skills: [
            { name: 'Git & GitHub', level: 85 },
            { name: 'VS Code', level: 95 },
            { name: 'npm / Vite', level: 80 },
            { name: 'REST APIs', level: 78 },
          ],
        },
      ],
      projects: [
        {
          icon: '',
          title: 'E-Commerce Platform',
          desc: 'Built a shopping site with Vue 3. Has a cart, product filters, and checkout that actually works. Made it mobile-friendly too.',
          tags: ['Vue.js', 'JavaScript', 'CSS Grid'],
          hovered: false,
          links: { demo: '#', github: '#' },
        },
        {
          icon: '',
          title: 'Analytics Dashboard',
          desc: 'Dashboard that shows real data with charts. You can switch between dark and light mode. Keeps things readable even with lots of info.',
          tags: ['Vue.js', 'Chart.js', 'REST API'],
          hovered: false,
          links: { demo: '#', github: '#' },
        },
        {
          icon: '',
          title: 'Component Library',
          desc: 'Made a set of reusable UI components — buttons, cards, forms, layouts. Just copy and use them in your project.',
          tags: ['HTML5', 'CSS3', 'JavaScript'],
          hovered: false,
          links: { github: '#' },
        },
        {
          icon: '',
          title: 'Blog Platform',
          desc: 'Simple blog where you can write, edit, and organize posts. Supports markdown. Everything saves to local storage.',
          tags: ['Vue.js', 'Markdown', 'LocalStorage'],
          hovered: false,
          links: { demo: '#', github: '#' },
        },
        {
          icon: '',
          title: 'Business Landing Page',
          desc: 'Fast loading site for a local business. SEO-friendly and designed to actually convert visitors into customers.',
          tags: ['HTML', 'CSS', 'JavaScript'],
          hovered: false,
          links: { demo: '#' },
        },
        {
          icon: '',
          title: 'Task Manager',
          desc: 'Drag-and-drop boards to organize tasks. Add priorities and due dates. Actually useful for daily work.',
          tags: ['Vue.js', 'LocalStorage', 'CSS'],
          hovered: false,
          links: { demo: '#', github: '#' },
        },
      ],
      education: [
        {
          badge: '',
          period: 'Technical Training',
          school: 'SOS Technical High School',
          level: 'Technical Diploma — Web & IT',
          desc: 'Specialized in web technologies, networking fundamentals, and software development. Built my first real web projects here and discovered my passion for the craft.',
        },
        {
          badge: '',
          period: 'A-Level Secondary',
          school: 'IFAK Secondary School',
          level: 'Advanced Level (A-Level)',
          desc: 'Completed Advanced Level studies with a focus on Mathematics, Computer Science, and Sciences — developing the analytical thinking that powers my development approach today.',
        },
        {
          badge: '',
          period: 'O-Level Secondary',
          school: 'St. Joseph Secondary School',
          level: 'Ordinary Level (O-Level)',
          desc: 'Built a solid academic foundation across all core subjects. Discovered early interest in technology, logic, and problem-solving that would shape my career path.',
        },
        {
          badge: '',
          period: 'Primary Education',
          school: 'St. Joseph Primary School',
          level: 'Primary Education',
          desc: 'Where curiosity began. A nurturing environment that encouraged creativity, discipline, and a love for learning that I carry to this day.',
        },
      ],
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll)
    this.startTyping()
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll)
  },
  methods: {
    handleScroll() {
      this.scrolled = window.scrollY > 60
    },
    scrollTo(id) {
      const el = document.getElementById(id)
      if (el) el.scrollIntoView({ behavior: 'smooth' })
    },
    startTyping() {
      const type = () => {
        const current = this.titles[this.currentTitleIndex]
        if (this.typingForward) {
          if (this.typingIndex < current.length) {
            this.displayedTitle = current.slice(0, ++this.typingIndex)
            setTimeout(type, 75)
          } else {
            setTimeout(() => { this.typingForward = false; type() }, 1800)
          }
        } else {
          if (this.typingIndex > 0) {
            this.displayedTitle = current.slice(0, --this.typingIndex)
            setTimeout(type, 40)
          } else {
            this.currentTitleIndex = (this.currentTitleIndex + 1) % this.titles.length
            this.typingForward = true
            setTimeout(type, 300)
          }
        }
      }
      type()
    },
    submitForm() {
      if (!this.form.name || !this.form.email || !this.form.message) return
      this.formSent = true
      setTimeout(() => {
        this.formSent = false
        this.form = { name: '', email: '', message: '' }
      }, 3000)
    },
  },
}
</script>

<style>
/* ─── IMPORTS ─── */
@import url('https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Josefin+Sans:wght@300;400;600&display=swap');

/* ─── RESET & ROOT ─── */
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

:root {
  --parchment: #f5ede0;
  --parchment-dark: #e8d9c0;
  --parchment-mid: #ede0cc;
  --ink: #2c1f0e;
  --ink-light: #5a3e28;
  --ink-faint: #8b6b4a;
  --accent: #8b4513;
  --accent-warm: #c46a1f;
  --gold: #b8860b;
  --gold-light: #d4a843;
  --cream: #faf5ec;
  --shadow: rgba(44, 31, 14, 0.12);
  --font-display: 'Cormorant Garamond', Georgia, serif;
  --font-body: 'Josefin Sans', sans-serif;
}

html { scroll-behavior: smooth; }

body {
  font-family: var(--font-body);
  background: var(--parchment);
  color: var(--ink);
  font-size: 15px;
  line-height: 1.7;
  overflow-x: hidden;
}

/* ─── PAPYRUS TEXTURE BACKGROUND ─── */
body::before {
  content: '';
  position: fixed;
  inset: 0;
  background-image:
    url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='400' height='400'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3CfeColorMatrix type='saturate' values='0'/%3E%3C/filter%3E%3Crect width='400' height='400' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
  pointer-events: none;
  z-index: 0;
  opacity: 0.6;
}

/* ─── NAVBAR ─── */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 20px 40px;
  transition: all 0.35s ease;
  background: transparent;
}
.navbar.scrolled {
  background: rgba(245, 237, 224, 0.96);
  backdrop-filter: blur(10px);
  padding: 14px 40px;
  box-shadow: 0 2px 20px var(--shadow);
  border-bottom: 1px solid var(--parchment-dark);
}
.nav-inner {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.nav-logo {
  font-family: var(--font-display);
  font-size: 1.6rem;
  font-weight: 600;
  color: var(--accent);
  letter-spacing: 2px;
  cursor: pointer;
}
.nav-links {
  display: flex;
  list-style: none;
  gap: 36px;
}
.nav-links a {
  font-family: var(--font-body);
  font-size: 0.78rem;
  font-weight: 400;
  letter-spacing: 2px;
  text-transform: uppercase;
  text-decoration: none;
  color: var(--ink-light);
  transition: color 0.2s;
  position: relative;
}
.nav-links a::after {
  content: '';
  position: absolute;
  bottom: -3px;
  left: 0;
  width: 0;
  height: 1px;
  background: var(--accent);
  transition: width 0.3s;
}
.nav-links a:hover { color: var(--accent); }
.nav-links a:hover::after { width: 100%; }
.hamburger {
  display: none;
  background: none;
  border: none;
  font-size: 1.4rem;
  color: var(--ink);
  cursor: pointer;
}
.mobile-menu {
  display: flex;
  flex-direction: column;
  gap: 12px;
  padding: 20px 0 10px;
}
.mobile-menu a {
  font-family: var(--font-body);
  font-size: 0.9rem;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  text-decoration: none;
  color: var(--ink-light);
}

/* ─── HERO ─── */
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  background:
    radial-gradient(ellipse at 20% 50%, rgba(184, 134, 11, 0.06) 0%, transparent 60%),
    radial-gradient(ellipse at 80% 20%, rgba(139, 69, 19, 0.05) 0%, transparent 50%),
    linear-gradient(160deg, var(--cream) 0%, var(--parchment) 50%, var(--parchment-dark) 100%);
}
.paper-texture {
  position: absolute;
  inset: 0;
  background-image: repeating-linear-gradient(
    0deg,
    transparent,
    transparent 28px,
    rgba(139, 107, 74, 0.04) 28px,
    rgba(139, 107, 74, 0.04) 29px
  );
  pointer-events: none;
}
.ink-splash {
  position: absolute;
  border-radius: 50%;
  filter: blur(60px);
  opacity: 0.07;
  pointer-events: none;
}
.ink-splash.left {
  width: 400px; height: 400px;
  background: var(--accent);
  top: 10%; left: -100px;
}
.ink-splash.right {
  width: 300px; height: 300px;
  background: var(--gold);
  bottom: 10%; right: -60px;
}
.hero-content {
  text-align: center;
  position: relative;
  z-index: 1;
  padding: 0 20px;
  animation: fadeUp 1s ease both;
}
.hero-headline {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 24px;
  flex-wrap: wrap;
  margin-bottom: 24px;
}
.hero-text-block {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.profile-wrap {
  position: relative;
  width: 110px;
  height: 110px;
  margin: 0;
}
.profile-circle {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--accent) 0%, var(--gold) 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  z-index: 2;
  box-shadow: 0 8px 30px rgba(139,69,19,0.3), 0 2px 8px rgba(0,0,0,0.1);
  overflow: hidden;
}
.profile-circle::before {
  content: '';
  position: absolute;
  inset: 3px;
  border-radius: 50%;
  background: linear-gradient(135deg, #c46a1f 0%, #8b4513 100%);
  z-index: 0;
}
.profile-pic {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 50%;
  position: relative;
  z-index: 1;
}
.profile-initials {
  font-family: var(--font-display);
  font-size: 2rem;
  font-weight: 600;
  color: var(--parchment);
  letter-spacing: 2px;
  position: relative;
  z-index: 1;
  display: none;
}
.profile-ring {
  position: absolute;
  inset: -5px;
  border-radius: 50%;
  border: 1.5px solid var(--gold-light);
  opacity: 0.5;
  animation: rotateSlow 12s linear infinite;
  border-top-color: transparent;
  border-left-color: transparent;
}

.hero-greeting {
  font-family: var(--font-body);
  font-size: 0.82rem;
  letter-spacing: 4px;
  text-transform: uppercase;
  color: var(--ink-faint);
  margin-bottom: 6px;
}
.hero-name {
  font-family: var(--font-display);
  font-size: clamp(3rem, 7vw, 5.5rem);
  font-weight: 600;
  color: var(--ink);
  letter-spacing: -1px;
  line-height: 1.1;
  margin-bottom: 14px;
}
.hero-title {
  font-family: var(--font-display);
  font-size: clamp(1.2rem, 3vw, 1.8rem);
  font-style: italic;
  color: var(--accent-warm);
  min-height: 2.2rem;
  margin-bottom: 22px;
}
.cursor {
  animation: blink 0.8s step-end infinite;
  color: var(--gold);
}
.hero-tagline {
  font-family: var(--font-body);
  font-size: 0.95rem;
  color: var(--ink-light);
  max-width: 520px;
  margin: 0 auto 36px;
  line-height: 1.8;
  font-weight: 300;
}
.hero-cta {
  display: flex;
  gap: 16px;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 56px;
}
.hero-scroll-hint {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  color: var(--ink-faint);
  font-size: 0.72rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  opacity: 0.7;
  transition: opacity 0.2s;
}
.hero-scroll-hint:hover { opacity: 1; }
.scroll-line {
  width: 1px;
  height: 40px;
  background: linear-gradient(to bottom, var(--gold), transparent);
  animation: pulse 2s ease-in-out infinite;
}

/* ─── BUTTONS ─── */
.btn-primary {
  font-family: var(--font-body);
  font-size: 0.78rem;
  letter-spacing: 2.5px;
  text-transform: uppercase;
  padding: 14px 34px;
  background: linear-gradient(135deg, var(--accent) 0%, var(--accent-warm) 100%);
  color: var(--cream);
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 18px rgba(139,69,19,0.25);
  position: relative;
  overflow: hidden;
}
.btn-primary::before {
  content: '';
  position: absolute;
  top: 0; left: -100%;
  width: 100%; height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
  transition: left 0.4s;
}
.btn-primary:hover::before { left: 100%; }
.btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 28px rgba(139,69,19,0.35); }
.btn-primary.full { width: 100%; }

.btn-outline {
  font-family: var(--font-body);
  font-size: 0.78rem;
  letter-spacing: 2.5px;
  text-transform: uppercase;
  padding: 14px 34px;
  background: transparent;
  color: var(--ink);
  border: 1.5px solid var(--ink-faint);
  cursor: pointer;
  transition: all 0.3s ease;
}
.btn-outline:hover {
  border-color: var(--accent);
  color: var(--accent);
  transform: translateY(-2px);
}

/* ─── SECTIONS ─── */
.section {
  padding: 100px 40px;
  position: relative;
  z-index: 1;
}
.section-inner {
  max-width: 1100px;
  margin: 0 auto;
}
.section-label {
  font-family: var(--font-body);
  font-size: 0.72rem;
  letter-spacing: 3px;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 16px;
}
.section-heading {
  font-family: var(--font-display);
  font-size: clamp(2.2rem, 4vw, 3.2rem);
  font-weight: 400;
  color: var(--ink);
  line-height: 1.25;
  margin-bottom: 48px;
}
.section-heading em {
  color: var(--accent);
  font-style: italic;
}

/* ─── ABOUT ─── */
.about-section {
  background:
    linear-gradient(180deg, var(--parchment) 0%, var(--parchment-mid) 100%);
  border-top: 1px solid rgba(139,107,74,0.12);
}
.about-grid {
  display: grid;
  grid-template-columns: 1fr 380px;
  gap: 72px;
  align-items: center;
}
.about-text p {
  color: var(--ink-light);
  font-weight: 300;
  font-size: 0.95rem;
  margin-bottom: 18px;
  line-height: 1.9;
}
.about-stats {
  display: flex;
  gap: 40px;
  margin-top: 40px;
  padding-top: 32px;
  border-top: 1px solid rgba(139,107,74,0.15);
}
.stat { display: flex; flex-direction: column; }
.stat-num {
  font-family: var(--font-display);
  font-size: 2.5rem;
  font-weight: 600;
  color: var(--accent);
  line-height: 1;
}
.stat-label {
  font-size: 0.72rem;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--ink-faint);
  margin-top: 4px;
}
.about-card {
  background: var(--cream);
  border: 1px solid var(--parchment-dark);
  padding: 40px 32px;
  position: relative;
  box-shadow: 6px 6px 0 var(--parchment-dark), 0 20px 60px var(--shadow);
}
.card-ink-border {
  position: absolute;
  top: 8px; left: 8px; right: -8px; bottom: -8px;
  border: 1px solid rgba(139,107,74,0.2);
  pointer-events: none;
}
.about-avatar-large {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  background: linear-gradient(135deg, var(--accent), var(--gold));
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 28px;
  overflow: hidden;
}
.about-profile-pic {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.avatar-text {
  font-family: var(--font-display);
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--cream);
  display: none;
}
.info-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 11px 0;
  border-bottom: 1px solid rgba(139,107,74,0.1);
  font-size: 0.85rem;
}
.info-label {
  color: var(--ink-faint);
  letter-spacing: 1px;
  text-transform: uppercase;
  font-size: 0.72rem;
}
.info-val { color: var(--ink); font-weight: 400; }
.available {
  color: #2d7a3a;
  background: rgba(45,122,58,0.1);
  padding: 2px 10px;
  font-size: 0.75rem;
  letter-spacing: 1px;
}

/* ─── SKILLS ─── */
.skills-section {
  background: var(--parchment-dark);
  background-image: repeating-linear-gradient(
    90deg,
    transparent,
    transparent 60px,
    rgba(139,107,74,0.03) 60px,
    rgba(139,107,74,0.03) 61px
  );
}
.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}
.skill-category {
  background: var(--cream);
  border: 1px solid var(--parchment-dark);
  padding: 36px 28px;
  transition: transform 0.3s, box-shadow 0.3s;
}
.skill-category:hover {
  transform: translateY(-4px);
  box-shadow: 0 16px 48px var(--shadow);
}
.skill-cat-icon {
  font-size: 1.8rem;
  margin-bottom: 12px;
}
.skill-cat-title {
  font-family: var(--font-display);
  font-size: 1.3rem;
  font-weight: 600;
  color: var(--ink);
  margin-bottom: 24px;
}
.skill-item { margin-bottom: 18px; }
.skill-header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 6px;
}
.skill-name {
  font-size: 0.82rem;
  letter-spacing: 0.5px;
  color: var(--ink-light);
}
.skill-pct {
  font-size: 0.78rem;
  color: var(--accent);
  font-weight: 600;
}
.skill-bar {
  height: 3px;
  background: var(--parchment-dark);
  overflow: hidden;
}
.skill-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--accent) 0%, var(--gold-light) 100%);
  transition: width 1.2s cubic-bezier(0.4, 0, 0.2, 1);
}

/* ─── PROJECTS ─── */
.projects-section {
  background: var(--parchment);
}
.projects-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 28px;
}
.project-card {
  background: var(--cream);
  border: 1px solid var(--parchment-dark);
  padding: 32px 28px;
  position: relative;
  transition: all 0.35s ease;
  cursor: default;
  overflow: hidden;
}
.project-card::before {
  content: '';
  position: absolute;
  top: 0; left: 0;
  width: 3px; height: 0;
  background: linear-gradient(to bottom, var(--accent), var(--gold));
  transition: height 0.4s ease;
}
.project-card:hover { transform: translateY(-6px); box-shadow: 0 20px 56px var(--shadow); }
.project-card:hover::before { height: 100%; }
.project-num {
  position: absolute;
  top: 20px; right: 20px;
  font-family: var(--font-display);
  font-size: 3rem;
  font-weight: 600;
  color: var(--parchment-dark);
  line-height: 1;
  pointer-events: none;
}
.project-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 20px;
}
.project-icon { font-size: 2rem; }
.project-links { display: flex; gap: 10px; }
.proj-link {
  font-size: 1rem;
  color: var(--ink-faint);
  text-decoration: none;
  transition: color 0.2s;
}
.proj-link:hover { color: var(--accent); }
.project-title {
  font-family: var(--font-display);
  font-size: 1.25rem;
  font-weight: 600;
  color: var(--ink);
  margin-bottom: 10px;
  line-height: 1.3;
}
.project-desc {
  font-size: 0.87rem;
  color: var(--ink-light);
  line-height: 1.75;
  font-weight: 300;
  margin-bottom: 20px;
}
.project-tags { display: flex; flex-wrap: wrap; gap: 8px; }
.tag {
  font-size: 0.7rem;
  letter-spacing: 1px;
  text-transform: uppercase;
  padding: 4px 10px;
  border: 1px solid var(--parchment-dark);
  color: var(--ink-faint);
  background: var(--parchment);
}

/* ─── EDUCATION TIMELINE ─── */
.education-section {
  background: var(--parchment-mid);
}
.timeline {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 0;
}
.timeline-item {
  display: flex;
  gap: 28px;
  position: relative;
  padding-bottom: 48px;
}
.timeline-dot {
  width: 14px;
  height: 14px;
  min-width: 14px;
  border-radius: 50%;
  background: var(--accent);
  margin-top: 8px;
  position: relative;
  z-index: 1;
  box-shadow: 0 0 0 4px var(--parchment-mid);
}
.timeline-line {
  position: absolute;
  left: 6px;
  top: 22px;
  bottom: 0;
  width: 1px;
  background: linear-gradient(to bottom, var(--accent), var(--parchment-dark));
  opacity: 0.4;
}
.timeline-card {
  flex: 1;
  background: var(--cream);
  border: 1px solid var(--parchment-dark);
  padding: 28px 32px;
  display: flex;
  gap: 24px;
  align-items: flex-start;
  transition: transform 0.3s, box-shadow 0.3s;
}
.timeline-card:hover {
  transform: translateX(4px);
  box-shadow: 0 8px 32px var(--shadow);
}
.timeline-badge {
  font-size: 1.8rem;
  min-width: 40px;
}
.timeline-period {
  font-size: 0.72rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: var(--accent);
  display: block;
  margin-bottom: 4px;
}
.timeline-school {
  font-family: var(--font-display);
  font-size: 1.3rem;
  font-weight: 600;
  color: var(--ink);
  margin-bottom: 4px;
}
.timeline-level {
  font-size: 0.78rem;
  letter-spacing: 1px;
  color: var(--gold);
  text-transform: uppercase;
  margin-bottom: 10px;
}
.timeline-desc {
  font-size: 0.88rem;
  color: var(--ink-light);
  font-weight: 300;
  line-height: 1.75;
}

/* ─── CONTACT ─── */
.contact-section {
  background:
    linear-gradient(160deg, var(--ink) 0%, #3d2a15 100%);
  color: var(--parchment);
}
.contact-section .section-label { color: var(--gold-light); }
.contact-section .section-heading { color: var(--parchment); }
.contact-sub {
  color: rgba(245,237,224,0.65);
  font-size: 0.95rem;
  font-weight: 300;
  max-width: 520px;
  margin-bottom: 56px;
  line-height: 1.8;
}
.contact-grid {
  display: grid;
  grid-template-columns: 1fr 360px;
  gap: 64px;
  align-items: start;
}
.contact-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.form-group label {
  font-size: 0.72rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: rgba(245,237,224,0.55);
}
.form-group input,
.form-group textarea {
  font-family: var(--font-body);
  font-size: 0.9rem;
  padding: 13px 16px;
  background: rgba(245,237,224,0.06);
  border: 1px solid rgba(245,237,224,0.15);
  color: var(--parchment);
  outline: none;
  transition: border-color 0.3s;
  resize: vertical;
}
.form-group input::placeholder,
.form-group textarea::placeholder { color: rgba(245,237,224,0.3); }
.form-group input:focus,
.form-group textarea:focus { border-color: var(--gold-light); }

.contact-info {
  display: flex;
  flex-direction: column;
  gap: 28px;
  padding-top: 6px;
}
.contact-block {
  display: flex;
  gap: 18px;
  align-items: flex-start;
}
.contact-icon {
  font-size: 1.2rem;
  width: 40px;
  height: 40px;
  background: rgba(245,237,224,0.06);
  border: 1px solid rgba(245,237,224,0.12);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.ci-label {
  font-size: 0.68rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: rgba(245,237,224,0.45);
  margin-bottom: 2px;
}
.ci-val {
  font-size: 0.9rem;
  color: rgba(245,237,224,0.8);
  font-weight: 300;
}

/* ─── FOOTER ─── */
.footer {
  background: #1a0f05;
  padding: 28px 40px;
  border-top: 1px solid rgba(245,237,224,0.06);
}
.footer-inner {
  max-width: 1100px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
}
.footer-name {
  font-family: var(--font-display);
  font-size: 1.1rem;
  color: var(--parchment);
  opacity: 0.8;
}
.footer-copy {
  font-size: 0.78rem;
  color: rgba(245,237,224,0.35);
  letter-spacing: 0.5px;
}
.footer-back {
  font-size: 0.75rem;
  letter-spacing: 1.5px;
  color: var(--gold-light);
  cursor: pointer;
  text-transform: uppercase;
  transition: opacity 0.2s;
}
.footer-back:hover { opacity: 0.7; }

/* ─── ANIMATIONS ─── */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(30px); }
  to { opacity: 1; transform: translateY(0); }
}
@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}
@keyframes pulse {
  0%, 100% { opacity: 0.4; transform: scaleY(0.8); }
  50% { opacity: 1; transform: scaleY(1); }
}
@keyframes rotateSlow {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

/* ─── RESPONSIVE ─── */
@media (max-width: 900px) {
  .about-grid,
  .contact-grid { grid-template-columns: 1fr; }
  .about-visual { order: -1; }
  .about-card { max-width: 400px; }
  .skills-grid,
  .projects-grid { grid-template-columns: repeat(2, 1fr); }
}
@media (max-width: 640px) {
  .section { padding: 72px 20px; }
  .navbar { padding: 16px 20px; }
  .navbar.scrolled { padding: 12px 20px; }
  .nav-links { display: none; }
  .hamburger { display: block; }
  .skills-grid,
  .projects-grid { grid-template-columns: 1fr; }
  .about-stats { flex-direction: column; gap: 20px; }
  .timeline-card { flex-direction: column; gap: 12px; }
  .footer-inner { flex-direction: column; text-align: center; }
  .hero-cta { flex-direction: column; align-items: center; }
}
</style>