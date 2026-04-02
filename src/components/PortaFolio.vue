<template>
  <div class="portafolio">
    <header class="nav" :class="{ 'nav--open': menuOpen }">
      <div class="nav__inner">
        <a class="nav__brand" href="#inicio" @click="closeMenu">Portafolio</a>
        <button type="button" class="nav__toggle" :aria-expanded="menuOpen" aria-label="Abrir o cerrar menú"
          @click="menuOpen = !menuOpen">
          <span />
          <span />
          <span />
        </button>
        <nav class="nav__links" aria-label="Principal">
          <a href="#inicio" @click="closeMenu">Inicio</a>
          <a href="#sobre-mi" @click="closeMenu">Sobre mí</a>
          <a href="#habilidades" @click="closeMenu">Habilidades</a>
          <a href="#proyectos" @click="closeMenu">Proyectos</a>
          <a href="#contacto" @click="closeMenu">Contacto</a>
        </nav>
      </div>
    </header>

    <main>
      <section id="inicio" class="hero">
        <div class="hero__layout">
          <figure class="hero__figure">
            <img class="hero__photo" :src="profile.photoUrl" :alt="`Fotografía de ${profile.name}`" width="280"
              height="280" loading="eager" decoding="async">
          </figure>
          <div class="hero__content">
            <p class="hero__eyebrow">Hola, soy</p>
            <h1 class="hero__title">{{ profile.name }}</h1>
            <p class="hero__role">{{ profile.role }}</p>
            <p class="hero__lead">{{ profile.tagline }}</p>
            <div class="hero__actions">
              <a class="btn btn--primary" href="#proyectos">Ver proyectos</a>
              <a class="btn btn--ghost" href="#contacto">Contactar</a>
            </div>
          </div>
        </div>
      </section>

      <section id="sobre-mi" class="section section--alt">
        <div class="section__inner">
          <h2 class="section__title">Sobre mí</h2>
          <p class="section__text">{{ profile.about }}</p>
        </div>
      </section>

      <section id="habilidades" class="section">
        <div class="section__inner">
          <h2 class="section__title">Habilidades</h2>
          <div v-for="(categorySkills, categoryName) in skills" :key="categoryName" class="skills__group">
            <h3 class="skills__category">{{ categoryName }}</h3>
            <ul class="skills">
              <li v-for="skill in categorySkills" :key="skill.label" class="skills__item">
                <span class="skills__icons" aria-hidden="true">
                  <i v-if="skill.iconClass" :class="['skills__fa', skill.iconClass]"
                    :style="skill.color ? { color: skill.color } : undefined" />
                  <i v-if="skill.iconClass2" :class="['skills__fa', 'skills__fa--extra', skill.iconClass2]"
                    :style="skill.color2 ? { color: skill.color2 } : undefined" />
                </span>
                <span class="skills__label">{{ skill.label }}</span>
              </li>
            </ul>
          </div>
        </div>
      </section>

      <section id="proyectos" class="section section--alt">
        <div class="section__inner">
          <h2 class="section__title">Proyectos</h2>
          <div class="projects">
            <article v-for="project in projects" :key="project.title" class="project-card">
              <div class="project-card__accent" :aria-hidden="true" />
              <h3 class="project-card__title">{{ project.title }}</h3>
              <p class="project-card__desc">{{ project.description }}</p>
              <ul class="project-card__tags">
                <li v-for="tag in project.tags" :key="tag">{{ tag }}</li>
              </ul>
              <a v-if="project.url" class="project-card__link" :href="project.url" target="_blank"
                rel="noopener noreferrer">
                Ver más
              </a>
            </article>
          </div>
        </div>
      </section>

      <section id="contacto" class="section">
        <div class="section__inner section__inner--narrow">
          <h2 class="section__title">Contacto</h2>
          <p class="section__text">
            Puedes contactarme a través de mi correo electrónico o mis redes sociales.
          </p>
          <div class="contact">
            <a class="contact__link" :href="`mailto:${profile.email}`">
              {{ profile.email }}
            </a>
            <div class="contact__social">
              <a v-for="link in social" :key="link.label" class="contact__social-link" :href="link.href" target="_blank"
                rel="noopener noreferrer">
                <i :class="link.iconClass" aria-hidden="true" />
                <span>{{ link.label }}</span>
              </a>
            </div>
          </div>
        </div>
      </section>
    </main>

    <footer class="footer">
      <p>© {{ year }} {{ profile.name }}. Hecho con Vue 3.</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import data from '../data/portfolio.json'

const { profile, skills, projects, social } = data

const menuOpen = ref(false)
const year = new Date().getFullYear()

function closeMenu() {
  menuOpen.value = false
}
</script>

<style scoped>
.portafolio {
  --bg: #f1f5f9;
  --bg-elevated: #ffffff;
  --surface-muted: #f8fafc;
  --text: #0f172a;
  --text-muted: #64748b;
  --accent: #3b82f6;
  --accent-strong: #2563eb;
  --accent-soft: #dbeafe;
  --accent-slate: #e2e8f0;
  --accent-ice: #e0f2fe;
  --border: rgba(100, 116, 139, 0.25);
  --radius: 16px;
  --shadow-soft: 0 14px 40px rgba(15, 23, 42, 0.08),
    0 6px 20px rgba(37, 99, 235, 0.06);
  --font: 'Segoe UI', system-ui, -apple-system, sans-serif;
  min-height: 100vh;
  background: linear-gradient(160deg,
      #f8fafc 0%,
      #e2e8f0 28%,
      #e0f2fe 55%,
      #eff6ff 78%,
      #f1f5f9 100%) fixed;
  color: var(--text);
  font-family: var(--font);
}

.nav {
  position: sticky;
  top: 0;
  z-index: 20;
  width: 100%;
  background: #475569;
  border-bottom: 1px solid rgba(0, 0, 0, 0.15);
  box-shadow: 0 2px 12px rgba(15, 23, 42, 0.12);
}

.nav__inner {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
  max-width: 1100px;
  margin: 0 auto;
  padding: 0.875rem 1.25rem;
}

.nav__brand {
  font-weight: 700;
  font-size: 1.1rem;
  color: #fff;
  text-decoration: none;
  letter-spacing: -0.02em;
}

.nav__brand:hover {
  color: #e2e8f0;
}

.nav__toggle {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 5px;
  width: 2.5rem;
  height: 2.5rem;
  padding: 0;
  border: 1px solid rgba(255, 255, 255, 0.35);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.12);
  cursor: pointer;
}

.nav__toggle span {
  display: block;
  height: 2px;
  width: 1.25rem;
  margin: 0 auto;
  background: #fff;
  border-radius: 1px;
  transition: transform 0.2s, opacity 0.2s;
}

.nav__links {
  display: none;
  flex-direction: column;
  gap: 0.25rem;
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  padding: 0.75rem 1.25rem 1rem;
  background: #334155;
  border-bottom: 1px solid rgba(0, 0, 0, 0.2);
  box-shadow: 0 12px 24px rgba(15, 23, 42, 0.15);
}

.nav--open .nav__links {
  display: flex;
}

.nav--open .nav__toggle span:nth-child(1) {
  transform: translateY(7px) rotate(45deg);
}

.nav--open .nav__toggle span:nth-child(2) {
  opacity: 0;
}

.nav--open .nav__toggle span:nth-child(3) {
  transform: translateY(-7px) rotate(-45deg);
}

.nav__links a {
  color: #f8fafc;
  text-decoration: none;
  padding: 0.5rem 0;
  font-size: 0.95rem;
}

.nav__links a:hover {
  color: #fff;
  text-decoration: underline;
  text-underline-offset: 0.2em;
}

@media (min-width: 768px) {
  .nav__inner {
    padding: 0.875rem 2rem;
  }

  .nav__toggle {
    display: none;
  }

  .nav__links {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 1.5rem;
    position: static;
    padding: 0;
    background: transparent;
    border: none;
    box-shadow: none;
  }

  .nav__links a {
    padding: 0;
  }

  .nav__links a:hover {
    color: #e2e8f0;
  }
}

main {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 1.25rem;
}

@media (min-width: 768px) {
  main {
    padding: 0 2rem;
  }
}

.hero {
  padding: 2.5rem 0 3.5rem;
  display: flex;
  justify-content: center;
}

.hero__layout {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  text-align: center;
  width: 100%;
  max-width: 960px;
}

@media (min-width: 768px) {
  .hero__layout {
    flex-direction: row;
    align-items: center;
    justify-content: center;
    text-align: left;
    gap: 3rem;
  }
}

.hero__figure {
  margin: 0;
  flex-shrink: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

.hero__photo {
  display: block;
  width: clamp(200px, 74vw, 200px);
  height: clamp(200px, 74vw, 200px);
  object-fit: cover;
  object-position: center center;
  border-radius: 50%;
  border: 4px solid var(--bg-elevated);
  box-shadow: var(--shadow-soft), 0 0 0 3px rgba(37, 99, 235, 0.15);
}

.hero__content {
  max-width: 40rem;
}

.hero__eyebrow {
  margin: 0 0 0.5rem;
  font-size: 0.9rem;
  color: var(--accent-strong);
  font-weight: 600;
  letter-spacing: 0.04em;
  text-transform: uppercase;
}

.hero__title {
  margin: 0 0 0.35rem;
  font-size: clamp(2rem, 5vw, 2.75rem);
  font-weight: 800;
  letter-spacing: -0.03em;
  line-height: 1.15;
  background: linear-gradient(115deg, #0f172a 0%, #475569 40%, #2563eb 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.hero__role {
  margin: 0 0 1rem;
  font-size: 1.15rem;
  color: var(--text-muted);
}

.hero__lead {
  margin: 0 0 1.75rem;
  font-size: 1.05rem;
  line-height: 1.65;
  color: var(--text-muted);
}

.hero__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
}

@media (max-width: 767px) {
  .hero__actions {
    justify-content: center;
  }
}

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.65rem 1.25rem;
  border-radius: 999px;
  font-size: 0.95rem;
  font-weight: 600;
  text-decoration: none;
  border: 2px solid transparent;
  transition: background 0.2s, color 0.2s, border-color 0.2s;
}

.btn--primary {
  background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  color: #fff;
  box-shadow: 0 4px 18px rgba(37, 99, 235, 0.35);
}

.btn--primary:hover {
  filter: brightness(1.08);
}

.btn--ghost {
  background: transparent;
  color: var(--text);
  border-color: var(--border);
}

.btn--ghost:hover {
  border-color: var(--accent-strong);
  color: var(--accent-strong);
  background: rgba(239, 246, 255, 0.9);
}

.section {
  padding: 3.5rem 0;
}

.section--alt {
  background: var(--bg-elevated);
  margin: 0 -1.25rem;
  padding: 3.5rem 1.25rem;
  border-radius: var(--radius);
  border: 1px solid var(--border);
  box-shadow: var(--shadow-soft);
}

@media (min-width: 768px) {
  .section--alt {
    margin: 0;
    padding: 3.5rem 2rem;
  }
}

.section__inner {
  max-width: 720px;
}

.section__inner--narrow {
  max-width: 520px;
}

.section__title {
  margin: 0 0 1.25rem;
  font-size: 1.5rem;
  font-weight: 700;
  letter-spacing: -0.02em;
  color: #1e293b;
}

.section__text {
  margin: 0;
  color: var(--text-muted);
  line-height: 1.7;
  font-size: 1.02rem;
}

.skills__group {
  margin-bottom: 1.5rem;
}

.skills__group:last-child {
  margin-bottom: 0;
}

.skills__category {
  margin: 0 0 0.75rem;
  font-size: 0.85rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--accent-strong);
}

.skills {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.skills__item {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.45rem 0.9rem;
  border-radius: 999px;
  font-size: 0.9rem;
  font-weight: 500;
}

.skills__icons {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
}

.skills__fa {
  font-size: 1.15rem;
  line-height: 1;
}

/* contraste del logo JS amarillo sobre fondos claros del chip */
.skills__item .fa-js {
  filter: drop-shadow(0 0 0.5px rgba(0, 0, 0, 0.35));
}

.skills__fa--extra {
  font-size: 1rem;
}

.skills__label {
  line-height: 1.2;
}

.skills__item:nth-child(4n + 1) {
  background: var(--accent-slate);
  color: #334155;
}

.skills__item:nth-child(4n + 2) {
  background: var(--accent-soft);
  color: #1d4ed8;
}

.skills__item:nth-child(4n + 3) {
  background: #cbd5e1;
  color: #1e293b;
}

.skills__item:nth-child(4n + 4) {
  background: var(--accent-ice);
  color: #075985;
}

.projects {
  display: grid;
  gap: 1.25rem;
}

@media (min-width: 640px) {
  .projects {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 900px) {
  .projects {
    grid-template-columns: repeat(3, 1fr);
  }
}

.project-card {
  position: relative;
  padding: 1.35rem;
  background: var(--surface-muted);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  overflow: hidden;
}

.project-card__accent {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: linear-gradient(90deg,
      #64748b,
      #94a3b8,
      #3b82f6,
      #1d4ed8);
}

.project-card__title {
  margin: 0;
  font-size: 1.1rem;
  font-weight: 700;
}

.project-card__desc {
  margin: 0;
  flex: 1;
  font-size: 0.92rem;
  line-height: 1.55;
  color: var(--text-muted);
}

.project-card__tags {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  gap: 0.35rem;
}

.project-card__tags li {
  font-size: 0.75rem;
  padding: 0.2rem 0.5rem;
  background: var(--bg-elevated);
  border-radius: 6px;
  color: var(--text-muted);
}

.project-card__link {
  align-self: flex-start;
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--accent-strong);
  text-decoration: none;
}

.project-card__link:hover {
  text-decoration: underline;
}

.contact {
  margin-top: 1.5rem;
}

.contact__link {
  display: inline-block;
  color: var(--accent-strong);
  font-weight: 600;
  text-decoration: none;
  margin-bottom: 1rem;
}

.contact__link:hover {
  text-decoration: underline;
}

.contact__social {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.contact__social-link {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  color: var(--text-muted);
  text-decoration: none;
  font-size: 0.95rem;
}

.contact__social-link .fa-github {
  color: #111827;
}

.contact__social-link .fa-linkedin {
  color: #0a66c2;
}

.contact__social-link:hover {
  color: var(--accent-strong);
}

.footer {
  margin-top: 3rem;
  padding: 2rem 1.25rem 2.5rem;
  text-align: center;
  font-size: 0.85rem;
  color: var(--text-muted);
  border-top: 1px solid var(--border);
}

.footer p {
  margin: 0;
}
</style>
