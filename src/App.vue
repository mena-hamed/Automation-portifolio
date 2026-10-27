<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'
import {
  ArrowDownRight,
  ArrowUpRight,
  ArrowRight,
  Menu,
  X,
  Workflow,
  Bot,
  GitBranch,
  Zap,
  Mail,
  Linkedin,
  Github,
  MoveUpRight,
  Sparkles,
  Code2,
  Database,
  CalendarDays,
  MessageSquare,
  CheckCircle2,
  Terminal,
  Play,
  RefreshCw,
  Cpu,
  Layers,
  ExternalLink,
  Copy,
  Check,
  Radio,
  Sliders,
  Share2
} from 'lucide-vue-next'

// Navigation & Layout
const menuOpen = ref(false)
const activeSection = ref('home')
const scrollProgress = ref(0)
const year = new Date().getFullYear()

const nav = [
  { label: 'About', href: '#about' },
  { label: 'Experience', href: '#experience' },
  { label: 'Skills', href: '#skills' },
  { label: 'Services', href: '#services' },
  { label: 'Projects', href: '#projects' },
  { label: 'Contact', href: '#contact' },
]

// Typewriter Effect for Hero
const fullLine1 = "Hi, I am Menna Hamed"
const typedLine1 = ref("")
const isLine1Done = ref(false)

const roles = [
  "An AI Automation Specialist",
  "n8n Workflow Architect",
  "Multi-Agent Systems Engineer",
  "Autonomous Solutions Developer",
]
const roleIndex = ref(0)
const typedRole = ref("")
const isDeletingRole = ref(false)
let roleTimer = null
let line1Timer = null

const typeLine1 = () => {
  let charIdx = 0
  const typeChar = () => {
    if (charIdx < fullLine1.length) {
      typedLine1.value += fullLine1.charAt(charIdx)
      charIdx++
      line1Timer = setTimeout(typeChar, 65)
    } else {
      isLine1Done.value = true
      setTimeout(startRoleCycle, 400)
    }
  }
  typeChar()
}

const startRoleCycle = () => {
  const currentFullRole = roles[roleIndex.value]

  if (!isDeletingRole.value) {
    if (typedRole.value.length < currentFullRole.length) {
      typedRole.value = currentFullRole.slice(0, typedRole.value.length + 1)
      roleTimer = setTimeout(startRoleCycle, 55)
    } else {
      // Hold the completed sentence so the viewer can read it comfortably
      roleTimer = setTimeout(() => {
        isDeletingRole.value = true
        startRoleCycle()
      }, 2400)
    }
  } else {
    if (typedRole.value.length > 0) {
      typedRole.value = currentFullRole.slice(0, typedRole.value.length - 1)
      roleTimer = setTimeout(startRoleCycle, 28)
    } else {
      isDeletingRole.value = false
      roleIndex.value = (roleIndex.value + 1) % roles.length
      roleTimer = setTimeout(startRoleCycle, 350)
    }
  }
}

// Hero Interactive Showcase
const heroTab = ref('engine') // 'engine' | 'profile'
const isSimulating = ref(false)
const activeNodeIndex = ref(-1)

const workflowLogs = ref([
  { time: '02:30:12', level: 'OK', text: 'n8n Workflow Engine initialized' },
  { time: '02:30:14', level: 'INFO', text: 'Multi-agent router listening on /webhook/v1' },
  { time: '02:30:15', level: 'ACTIVE', text: 'All nodes synchronized & ready' },
])

const simulateWorkflow = () => {
  if (isSimulating.value) return
  isSimulating.value = true
  activeNodeIndex.value = 0

  const now = () => {
    const d = new Date()
    return `${String(d.getHours()).padStart(2, '0')}:${String(d.getMinutes()).padStart(2, '0')}:${String(d.getSeconds()).padStart(2, '0')}`
  }

  workflowLogs.value.unshift({
    time: now(),
    level: 'TRIGGER',
    text: '⚡ Inbound webhook trigger received: payload.json',
  })

  setTimeout(() => {
    activeNodeIndex.value = 1
    workflowLogs.value.unshift({
      time: now(),
      level: 'AI AGENT',
      text: '🤖 LLM Intent Classification completed (latency: 180ms)',
    })
  }, 700)

  setTimeout(() => {
    activeNodeIndex.value = 2
    workflowLogs.value.unshift({
      time: now(),
      level: 'RAG',
      text: '🔍 Vector search query matched 3 contextual documents',
    })
  }, 1400)

  setTimeout(() => {
    activeNodeIndex.value = 3
    workflowLogs.value.unshift({
      time: now(),
      level: 'ROUTER',
      text: '🔀 Decision branch dispatched to Google Workspace & APIs',
    })
  }, 2100)

  setTimeout(() => {
    activeNodeIndex.value = 4
    workflowLogs.value.unshift({
      time: now(),
      level: 'DONE',
      text: '✓ Execution finished successfully (Total: 840ms)',
    })
    isSimulating.value = false
    setTimeout(() => {
      activeNodeIndex.value = -1
    }, 1200)
  }, 2800)
}

// Projects Data
const projects = [
  {
    number: '01',
    type: 'MULTI-AGENT SYSTEM',
    badge: 'n8n Architecture',
    title: 'Personal/Business AI Assistant',
    description: 'A three-agent autonomous n8n assistant that categorizes inbound requests, decides between business vs personal context, and triggers the appropriate tool integrations.',
    tags: ['n8n', 'AI Agents', 'Google Workspace', 'Routing'],
    link: '#contact',
    thumb: 'agent',
    stats: '3 Specialized Sub-Agents'
  },
  {
    number: '02',
    type: 'N8N AUTOMATION · LINKEDIN',
    badge: 'Content Agent',
    title: 'Automatic LinkedIn Poster',
    description: 'An AI automation pipeline that curates research resources, formulates engaging industry posts via RAG, and automatically publishes directly through the LinkedIn API.',
    tags: ['LinkedIn API', 'RAG System', 'AI Automation', 'Scheduling'],
    link: '#contact',
    thumb: 'linkedin',
    stats: '100% Hands-Free Publishing'
  },
  {
    number: '03',
    type: 'AI-POWERED ASSISTANT',
    badge: 'Knowledge Retrieval',
    title: 'HR System',
    description: 'A complete clock-in, clock-out and leave request system in addition to a cv classification for requested candidates.',
    tags: ['Weebhook', 'Vector Search', 'Ollama / Gemini'],
    link: '#contact',
    thumb: 'knowledge',
    stats: 'Complete Hr System'
  },
]

// Services
const services = [
  {
    icon: Workflow,
    n: '01',
    title: 'Autonomous Workflow Automation',
    desc: 'Connecting apps, cutting manual repetitive overhead, and building self-healing workflows that keep business running in the background 24/7.',
    highlights: ['n8n Self-Hosted & Cloud', 'Webhook Triggers', 'Custom Logic & Transforms']
  },
  {
    icon: Bot,
    n: '02',
    title: 'AI Multi-Agent Systems',
    desc: 'Designing router-driven autonomous agents that classify intent, retrieve knowledge with RAG, call specialized tools, and complete multi-step tasks.',
    highlights: ['Intent Routing', 'Tool Calling', 'Persistent Memory & State']
  },
  {
    icon: GitBranch,
    n: '03',
    title: 'Seamless Integrations & Custom APIs',
    desc: 'Unifying fragmented platforms: Google Workspace, LinkedIn API, Notion, databases, vector stores, and custom REST webhooks into cohesive pipelines.',
    highlights: ['RESTful Webhooks', 'Authentication & OAuth', 'Data Normalization']
  },
  {
    icon: Sparkles,
    n: '04',
    title: 'Process Optimization & Systems Design',
    desc: 'Mapping complex manual bottlenecks, removing friction points, and converting time-consuming operational tasks into elegant, reliable automations.',
    highlights: ['Process Audits', 'Error Handling & Alerts', 'Measurable Efficiency Gains']
  },
]

// Skill Groups
const skillGroups = [
  {
    title: 'WORKFLOW & AUTOMATION',
    subtitle: 'Core Engine',
    icon: Workflow,
    items: ['n8n', 'Workflow Architecture', 'Webhooks & Polling', 'Cron Triggers', 'Error Handlers', 'Sub-Workflows']
  },
  {
    title: 'AI SYSTEMS & MULTI-AGENT',
    subtitle: 'Intelligence Layer',
    icon: Bot,
    items: ['Multi-Agent Systems', 'LLM Routing', 'Prompt Engineering', 'RAG Fundamentals', 'Vector Search', 'Tool Calling']
  },
  {
    title: 'DEVELOPMENT & LOGIC',
    subtitle: 'Technical Foundation',
    icon: Code2,
    items: ['Python', 'JavaScript', 'REST APIs', 'JSON Transformations', 'Vue.js', 'Git & GitHub']
  },
  {
    title: 'INTEGRATIONS & ECOSYSTEM',
    subtitle: 'Connected Tools',
    icon: Database,
    items: ['Google Workspace', 'LinkedIn API', 'OpenRouter / Gemini', 'Vector Stores', 'Notion API', 'Telegram Bots']
  },
]

// Email Copy
const emailCopied = ref(false)
const copyEmail = () => {
  navigator.clipboard.writeText('mennahamedmakram05@gmail.com')
  emailCopied.value = true
  setTimeout(() => {
    emailCopied.value = false
  }, 2500)
}

// Spotlight Mouse Effect on Cards
const handleCardMouseMove = (e) => {
  const card = e.currentTarget
  const rect = card.getBoundingClientRect()
  const x = e.clientX - rect.left
  const y = e.clientY - rect.top
  card.style.setProperty('--mouse-x', `${x}px`)
  card.style.setProperty('--mouse-y', `${y}px`)
}

// Particle Canvas Animation
const canvasRef = ref(null)
let animationFrameId = null

const initCanvas = () => {
  const canvas = canvasRef.value
  if (!canvas) return
  const ctx = canvas.getContext('2d')

  let width = (canvas.width = window.innerWidth)
  let height = (canvas.height = window.innerHeight)

  const handleResize = () => {
    if (!canvas) return
    width = canvas.width = window.innerWidth
    height = canvas.height = window.innerHeight
  }
  window.addEventListener('resize', handleResize)

  const particles = []
  const count = Math.min(Math.floor(width / 28), 45)

  for (let i = 0; i < count; i++) {
    particles.push({
      x: Math.random() * width,
      y: Math.random() * height,
      vx: (Math.random() - 0.5) * 0.45,
      vy: (Math.random() - 0.5) * 0.45,
      radius: Math.random() * 1.5 + 0.8,
      alpha: Math.random() * 0.5 + 0.2,
    })
  }

  let mouse = { x: -1000, y: -1000 }
  const handleMouseMove = (e) => {
    mouse.x = e.clientX
    mouse.y = e.clientY
  }
  window.addEventListener('mousemove', handleMouseMove)

  const render = () => {
    ctx.clearRect(0, 0, width, height)

    // Draw connecting lines between nearby particles
    for (let i = 0; i < particles.length; i++) {
      const p1 = particles[i]
      p1.x += p1.vx
      p1.y += p1.vy

      if (p1.x < 0) p1.x = width
      else if (p1.x > width) p1.x = 0
      if (p1.y < 0) p1.y = height
      else if (p1.y > height) p1.y = 0

      // Mouse subtle attraction
      const dxMouse = mouse.x - p1.x
      const dyMouse = mouse.y - p1.y
      const distMouse = Math.sqrt(dxMouse * dxMouse + dyMouse * dyMouse)
      if (distMouse < 120) {
        p1.x += (dxMouse / distMouse) * 0.4
        p1.y += (dyMouse / distMouse) * 0.4
      }

      ctx.beginPath()
      ctx.arc(p1.x, p1.y, p1.radius, 0, Math.PI * 2)
      ctx.fillStyle = `rgba(197, 250, 107, ${p1.alpha})`
      ctx.fill()

      for (let j = i + 1; j < particles.length; j++) {
        const p2 = particles[j]
        const dx = p1.x - p2.x
        const dy = p1.y - p2.y
        const dist = Math.sqrt(dx * dx + dy * dy)

        if (dist < 110) {
          ctx.beginPath()
          ctx.moveTo(p1.x, p1.y)
          ctx.lineTo(p2.x, p2.y)
          const lineAlpha = (1 - dist / 110) * 0.16
          ctx.strokeStyle = `rgba(197, 250, 107, ${lineAlpha})`
          ctx.lineWidth = 0.8
          ctx.stroke()
        }
      }
    }

    animationFrameId = requestAnimationFrame(render)
  }

  render()

  return () => {
    window.removeEventListener('resize', handleResize)
    window.removeEventListener('mousemove', handleMouseMove)
    cancelAnimationFrame(animationFrameId)
  }
}

// Scroll Progress Tracker & Intersection Observer
let cleanupCanvas = null
let observer = null

const handleScroll = () => {
  const scrollTop = window.scrollY || document.documentElement.scrollTop
  const docHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight
  scrollProgress.value = docHeight > 0 ? (scrollTop / docHeight) * 100 : 0
}

onMounted(() => {
  typeLine1()
  cleanupCanvas = initCanvas()

  window.addEventListener('scroll', handleScroll, { passive: true })

  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          activeSection.value = entry.target.id
        }
      })
    },
    { rootMargin: '-30% 0px -50% 0px' }
  )

  document.querySelectorAll('section[id]').forEach((sec) => observer.observe(sec))
})

onUnmounted(() => {
  clearTimeout(line1Timer)
  clearTimeout(roleTimer)
  if (cleanupCanvas) cleanupCanvas()
  window.removeEventListener('scroll', handleScroll)
  observer?.disconnect()
})

const closeMenu = () => {
  menuOpen.value = false
}
</script>

<template>
  <div class="site-shell">
    <!-- Scroll Progress Indicator -->
    <div class="scroll-progress-bar" :style="{ width: `${scrollProgress}%` }"></div>

    <!-- Interactive Neural Canvas -->
    <canvas ref="canvasRef" class="ambient-canvas"></canvas>

    <!-- Glowing Ambient Mesh Background Orbs -->
    <div class="ambient-glow glow-1"></div>
    <div class="ambient-glow glow-2"></div>
    <div class="ambient-glow glow-3"></div>

    <!-- High-Tech Grain Texture -->
    <div class="grain"></div>

    <!-- Navigation Header -->
    <header class="topbar">
      <a class="brand" href="#home" @click="closeMenu">
        <span class="brand-mark">
          <Workflow :size="18" />
        </span>
        <span class="brand-text">
          MENNA<span class="brand-dot">.</span>
        </span>
        <span class="brand-status-tag">
          <span class="status-pulse-dot"></span>
          AI AUTOMATION
        </span>
      </a>

      <nav class="desktop-nav">
        <a
          v-for="item in nav"
          :key="item.href"
          :href="item.href"
          :class="{ active: activeSection === item.href.slice(1) }"
        >
          {{ item.label }}
        </a>
      </nav>

      <div class="topbar-actions">
        <a class="nav-cta" href="#contact">
          <span>LET'S CONNECT</span>
          <ArrowUpRight :size="14" />
        </a>

        <button
          class="menu-toggle"
          aria-label="Toggle navigation"
          @click="menuOpen = !menuOpen"
        >
          <X v-if="menuOpen" :size="20" />
          <Menu v-else :size="20" />
        </button>
      </div>
    </header>

    <!-- Mobile Drawer Menu -->
    <transition name="drawer-fade">
      <div v-if="menuOpen" class="mobile-menu">
        <a
          v-for="item in nav"
          :key="item.href"
          :href="item.href"
          @click="closeMenu"
        >
          {{ item.label }}
        </a>
        <a href="#contact" class="mobile-cta" @click="closeMenu">
          <span>Let's Connect</span>
          <ArrowUpRight :size="15" />
        </a>
      </div>
    </transition>

    <main>
      <!-- HERO SECTION -->
      <section id="home" class="hero section-wrap">
        <div class="hero-content">
          <!-- Live Status Beacon Badge -->
          <div class="hero-status-pill">
            <span class="live-dot-beacon"></span>
            <span class="status-pill-text">AVAILABLE FOR NEW PROJECTS & COLLABORATIONS</span>
            <span class="status-pill-sub">DEPI AI TRAINEE</span>
          </div>

          <!-- DYNAMIC TYPEWRITER HEADLINE -->
          <div class="hero-headline-block">
            <!-- Line 1: Big Name with typing effect -->
            <h1 class="hero-line-1">
              {{ typedLine1 }}<span v-if="!isLine1Done" class="typewriter-cursor">|</span>
            </h1>

            <!-- Line 2: The dynamic transition line on lower row -->
            <div class="hero-line-2-wrapper">
              <span class="hero-role-typed">
                {{ typedRole }}<span v-if="isLine1Done" class="typewriter-cursor active">|</span>
              </span>
            </div>
          </div>

          <!-- Elevator Pitch -->
          <p class="hero-intro">
            I engineer smart, autonomous multi-agent pipelines and <span class="text-highlight">n8n automations</span> that turn manual bottlenecks into effortless, self-running systems.
          </p>

          <!-- Core Tech Capability Chips -->
          <div class="hero-capsules">
            <span class="hero-chip"><Workflow :size="13" /> n8n Workflows</span>
            <span class="hero-chip"><Bot :size="13" /> Multi-Agent Systems</span>
            <span class="hero-chip"><Sparkles :size="13" /> RAG & Embeddings</span>
            <span class="hero-chip"><GitBranch :size="13" /> API Integrations</span>
          </div>

          <!-- Action Buttons -->
          <div class="hero-actions">
            <a class="button button-primary" href="#projects">
              <span>Explore My Work</span>
              <ArrowUpRight :size="16" />
            </a>
            <a class="button button-glass" href="#about">
              <span>Systems Architecture</span>
              <ArrowDownRight :size="16" />
            </a>
          </div>

          <!-- Quick Metrics Banner -->
          <div class="hero-metrics">
            <div class="metric-item">
              <span class="metric-num">3+</span>
              <span class="metric-label">MULTI-AGENT BUILDS</span>
            </div>
            <div class="metric-divider"></div>
            <div class="metric-item">
              <span class="metric-num">100%</span>
              <span class="metric-label">AUTOMATED LOGIC</span>
            </div>
            <div class="metric-divider"></div>
            <div class="metric-item">
              <span class="metric-num">&lt; 1.5s</span>
              <span class="metric-label">LATENCY ORCHESTRATION</span>
            </div>
          </div>
        </div>

        <!-- HERO RIGHT SHOWCASE: INTERACTIVE ENGINE & PROFILE -->
        <div class="hero-showcase">
          <div class="showcase-card">
            <!-- Showcase Header Tabs -->
            <div class="showcase-tabs">
              <button
                class="tab-btn"
                :class="{ active: heroTab === 'engine' }"
                @click="heroTab = 'engine'"
              >
                <Zap :size="14" />
                <span>Live n8n Engine</span>
                <span class="tab-indicator-dot"></span>
              </button>
              <button
                class="tab-btn"
                :class="{ active: heroTab === 'profile' }"
                @click="heroTab = 'profile'"
              >
                <Bot :size="14" />
                <span>Engineer Card</span>
              </button>
            </div>

            <!-- TAB 1: LIVE INTERACTIVE N8N ENGINE -->
            <div v-show="heroTab === 'engine'" class="showcase-engine">
              <div class="engine-topline">
                <span class="engine-title">
                  <Workflow :size="14" />
                  <span>AUTONOMOUS_MULTI_AGENT_PIPELINE.n8n</span>
                </span>
                <button
                  class="simulate-btn"
                  :disabled="isSimulating"
                  @click="simulateWorkflow"
                >
                  <Play v-if="!isSimulating" :size="12" />
                  <RefreshCw v-else :size="12" class="spin-icon" />
                  <span>{{ isSimulating ? 'EXECUTING...' : 'TRIGGER SIMULATION' }}</span>
                </button>
              </div>

              <!-- Interactive Workflow Canvas Visual -->
              <div class="workflow-canvas">
                <!-- Glowing SVG Wires -->
                <svg class="canvas-wires" viewBox="0 0 460 220" preserveAspectRatio="none">
                  <path
                    class="canvas-wire wire-bg"
                    d="M 60 70 C 130 70, 130 110, 200 110 S 270 70, 340 70 H 400"
                  />
                  <path
                    class="canvas-wire wire-active"
                    :class="{ flowing: isSimulating }"
                    d="M 60 70 C 130 70, 130 110, 200 110 S 270 70, 340 70 H 400"
                  />
                  <path
                    class="canvas-wire wire-branch"
                    d="M 200 110 C 240 110, 240 170, 320 170 H 400"
                  />
                </svg>

                <!-- Flow Nodes -->
                <div
                  class="flow-node node-1"
                  :class="{ active: activeNodeIndex === 0, lit: activeNodeIndex >= 0 }"
                >
                  <div class="node-icon-box trigger-bg"><Zap :size="15" /></div>
                  <div class="node-info">
                    <span class="node-type">TRIGGER</span>
                    <strong class="node-name">Webhook</strong>
                  </div>
                  <span class="node-status-glow"></span>
                </div>

                <div
                  class="flow-node node-2"
                  :class="{ active: activeNodeIndex === 1, lit: activeNodeIndex >= 1 }"
                >
                  <div class="node-icon-box agent-bg"><Bot :size="15" /></div>
                  <div class="node-info">
                    <span class="node-type">AI AGENT</span>
                    <strong class="node-name">Gemini Intent</strong>
                  </div>
                  <span class="node-status-glow"></span>
                </div>

                <div
                  class="flow-node node-3"
                  :class="{ active: activeNodeIndex === 2, lit: activeNodeIndex >= 2 }"
                >
                  <div class="node-icon-box rag-bg"><Sparkles :size="15" /></div>
                  <div class="node-info">
                    <span class="node-type">KNOWLEDGE</span>
                    <strong class="node-name">Vector RAG</strong>
                  </div>
                  <span class="node-status-glow"></span>
                </div>

                <div
                  class="flow-node node-4"
                  :class="{ active: activeNodeIndex === 3, lit: activeNodeIndex >= 3 }"
                >
                  <div class="node-icon-box router-bg"><GitBranch :size="15" /></div>
                  <div class="node-info">
                    <span class="node-type">INTEGRATION</span>
                    <strong class="node-name">Workspace API</strong>
                  </div>
                  <span class="node-status-glow"></span>
                </div>

                <div
                  class="flow-node node-5"
                  :class="{ active: activeNodeIndex === 4, lit: activeNodeIndex >= 4 }"
                >
                  <div class="node-icon-box done-bg"><CheckCircle2 :size="15" /></div>
                  <div class="node-info">
                    <span class="node-type">COMPLETED</span>
                    <strong class="node-name">Success (200)</strong>
                  </div>
                  <span class="node-status-glow"></span>
                </div>
              </div>

              <!-- Live Execution Terminal Log Feed -->
              <div class="engine-terminal">
                <div class="terminal-bar">
                  <div class="terminal-dots">
                    <span></span><span></span><span></span>
                  </div>
                  <span class="terminal-title">LIVE TELEMETRY STREAM</span>
                  <span class="terminal-status">
                    <span class="live-dot-small"></span> RUNTIME READY
                  </span>
                </div>
                <div class="terminal-logs">
                  <div
                    v-for="(log, idx) in workflowLogs"
                    :key="idx"
                    class="log-row"
                  >
                    <span class="log-time">[{{ log.time }}]</span>
                    <span class="log-badge" :class="log.level.toLowerCase().replace(/\s+/g, '-')">{{ log.level }}</span>
                    <span class="log-msg">{{ log.text }}</span>
                  </div>
                </div>
              </div>
            </div>

            <!-- TAB 2: ENGINEER PROFILE CARD -->
            <div v-show="heroTab === 'profile'" class="showcase-profile">
              <div class="profile-card-inner">
                <div class="profile-image-frame">
                  <img
                    src="/images/menna-portrait.jpeg"
                    alt="Menna Hamed - AI Automation Specialist"
                    class="profile-img"
                  />
                  <div class="profile-hud-overlay">
                    <span class="hud-corner top-left"></span>
                    <span class="hud-corner top-right"></span>
                    <span class="hud-corner bottom-left"></span>
                    <span class="hud-corner bottom-right"></span>
                    <span class="hud-badge">AI / AUTOMATION</span>
                  </div>
                </div>

                <div class="profile-details">
                  <div class="profile-header">
                    <h3>Menna Hamed</h3>
                    <span class="profile-role">AI Automation Specialist</span>
                  </div>
                  <p class="profile-bio">
                    Senior Computer Science student at Alexandria National University specializing in autonomous workflows, router-driven multi-agent frameworks, and end-to-end n8n architecture.
                  </p>
                  <div class="profile-tags">
                    <span>Alexandria National Univ</span>
                    <span>DEPI AI Trainee</span>
                    <span>NTI NLP Alum</span>
                    <span>GPA 3.3</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- ABOUT SECTION -->
      <section id="about" class="about section-wrap section-block">
        <div class="section-kicker">
          <span class="kicker-num">01</span>
          <span class="kicker-divider">/</span>
          <span>A LITTLE ABOUT ME</span>
        </div>

        <div class="about-grid">
          <div class="about-heading-col">
            <h2>
              Systems thinker.<br />
              <span class="gradient-text">Automation builder.</span>
            </h2>
            <p class="about-quote-lead">
              "I turn repetitive, manual bottlenecks into intelligent workflows — giving teams and creators more room to focus on high-impact work."
            </p>

            <!-- Dynamic Architecture Concept Box -->
            <div class="architecture-box">
              <div class="arch-header">
                <span class="arch-label">CORE ARCHITECTURE PARADIGM</span>
                <span class="arch-code">n8n + LLM</span>
              </div>
              <div class="arch-flow">
                <div class="arch-step">
                  <span class="step-num">01</span>
                  <strong>Manual Chaos</strong>
                  <small>Scattered inputs</small>
                </div>
                <div class="arch-arrow">➔</div>
                <div class="arch-step highlight">
                  <span class="step-num">02</span>
                  <strong>AI Routing</strong>
                  <small>Intent & RAG</small>
                </div>
                <div class="arch-arrow">➔</div>
                <div class="arch-step highlight-alt">
                  <span class="step-num">03</span>
                  <strong>n8n Execution</strong>
                  <small>Autonomous delivery</small>
                </div>
              </div>
            </div>
          </div>

          <div class="about-content-col">
            <div class="availability-pill">
              <span class="status-dot"></span>
              <span>OPEN TO COLLABORATIONS & AI AUTOMATION PROJECTS</span>
            </div>

            <p class="about-lead">
              I'm <strong>Menna Hamed</strong>, a Senior Computer Science student at Alexandria National University deeply passionate about the intersection of <em>AI agents, workflow orchestration, and practical business automation</em>.
            </p>

            <p>
              I use <strong>n8n</strong> to design workflows that eliminate manual friction, route information precisely where it needs to go, and free people from tedious repetitive tasks. From autonomous multi-agent assistants and LinkedIn content pipelines to real-time API integrations, I specialize in engineering clean, dependable solutions that work reliably at scale.
            </p>

            <p>
              My philosophy is straightforward: understand the human problem first, then build an automated system that feels intuitive, fault-tolerant, and genuinely valuable — not just complex for complexity's sake.
            </p>

            <!-- Stat Counters -->
            <div class="about-stats-grid">
              <div class="stat-box" @mousemove="handleCardMouseMove">
                <div class="stat-top">
                  <Workflow :size="18" />
                  <span class="stat-num">AI + n8n</span>
                </div>
                <span class="stat-title">CORE DISCIPLINE</span>
                <p>Autonomous agents & workflow automation</p>
              </div>

              <div class="stat-box" @mousemove="handleCardMouseMove">
                <div class="stat-top">
                  <Bot :size="18" />
                  <span class="stat-num">End-to-End</span>
                </div>
                <span class="stat-title">SYSTEMS THINKING</span>
                <p>From initial trigger to final execution</p>
              </div>

              <div class="stat-box" @mousemove="handleCardMouseMove">
                <div class="stat-top">
                  <Sparkles :size="18" />
                  <span class="stat-num">Human-First</span>
                </div>
                <span class="stat-title">PRACTICAL IMPACT</span>
                <p>Engineered for real-world reliability</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      <!-- EXPERIENCE & EDUCATION SECTION -->
      <section id="experience" class="experience section-wrap section-block">
        <div class="section-kicker">
          <span class="kicker-num">02</span>
          <span class="kicker-divider">/</span>
          <span>THE FOUNDATION</span>
        </div>

        <div class="section-heading-row">
          <h2>
            Where I learned<br />
            <span class="gradient-text">to build & automate.</span>
          </h2>
          <p>
            A strong Computer Science foundation combined with intensive practical training in AI workflow orchestration, multi-agent pipelines, and autonomous integrations.
          </p>
        </div>

        <div class="timeline-layout">
          <!-- Timeline Column -->
          <div class="timeline-column">
            <div class="subsection-label">
              <span class="label-symbol">↗</span>
              <span>EXPERIENCE & EDUCATION</span>
            </div>

            <!-- Item 1: DEPI -->
            <div class="timeline-item active-timeline" @mousemove="handleCardMouseMove">
              <div class="timeline-meta">
                <span class="timeline-badge current">CURRENT</span>
                <span class="timeline-date">2026 — PRESENT</span>
              </div>
              <div class="timeline-content">
                <div class="timeline-title-row">
                  <h3>AI Automation With n8n Trainee</h3>
                  <span class="timeline-org">Digital Egypt Pioneers Initiative (DEPI) · Remote</span>
                </div>
                <p class="timeline-desc">
                  Specialized in building end-to-end AI automation systems and autonomous workflow solutions using n8n, LLM routing, and API integrations.
                </p>
                <div class="timeline-tags">
                  <span>Multi-Agent Architectures</span>
                  <span>n8n Workflows</span>
                  <span>OpenRouter / Gemini</span>
                  <span>Vector Databases (RAG)</span>
                  <span>Google Workspace Automation</span>
                </div>
              </div>
            </div>

            <!-- Item 2: NTI -->
            <div class="timeline-item" @mousemove="handleCardMouseMove">
              <div class="timeline-meta">
                <span class="timeline-badge intern">COMPLETED</span>
                <span class="timeline-date">PREVIOUS</span>
              </div>
              <div class="timeline-content">
                <div class="timeline-title-row">
                  <h3>NLP Intern</h3>
                  <span class="timeline-org">National Telecommunication Institute (NTI)</span>
                </div>
                <p class="timeline-desc">
                  Focused on Natural Language Processing pipelines, text preprocessing, tokenization, semantic embeddings, and understanding transformer model architectures.
                </p>
                <div class="timeline-tags">
                  <span>NLP Pipelines</span>
                  <span>Text Classification</span>
                  <span>Python</span>
                  <span>Model Evaluation</span>
                </div>
              </div>
            </div>

            <!-- Item 3: Degree -->
            <div class="timeline-item" @mousemove="handleCardMouseMove">
              <div class="timeline-meta">
                <span class="timeline-badge edu">DEGREE</span>
                <span class="timeline-date">2023 — 2027</span>
              </div>
              <div class="timeline-content">
                <div class="timeline-title-row">
                  <h3>B.Sc. in Computer Science</h3>
                  <span class="timeline-org">Alexandria National University</span>
                </div>
                <p class="timeline-desc">
                  Senior student maintaining a <strong>GPA of 3.3</strong>. Core coursework in Data Structures, Algorithms, Software Engineering, Database Systems, and Artificial Intelligence.
                </p>
                <div class="timeline-tags">
                  <span>GPA: 3.3 / 4.0</span>
                  <span>Expected: 2027</span>
                  <span>Software Engineering</span>
                  <span>Data Structures</span>
                </div>
              </div>
            </div>
          </div>

          <!-- Certifications & Philosophy Column -->
          <div class="cert-column">
            <div class="subsection-label">
              <span class="label-symbol">✳</span>
              <span>SPECIALIZED DOMAINS</span>
            </div>

            <div class="cert-card" @mousemove="handleCardMouseMove">
              <div class="cert-icon-box">
                <Workflow :size="20" />
              </div>
              <div class="cert-info">
                <span class="cert-kicker">AUTONOMOUS ORCHESTRATION</span>
                <h4>n8n Workflow Engineering</h4>
                <p>Designing multi-step, webhook-driven, and event-based autonomous processes.</p>
              </div>
            </div>

            <div class="cert-card" @mousemove="handleCardMouseMove">
              <div class="cert-icon-box bot-accent">
                <Bot :size="20" />
              </div>
              <div class="cert-info">
                <span class="cert-kicker">INTELLIGENCE & ROUTING</span>
                <h4>Multi-Agent AI Systems</h4>
                <p>Router-driven LLMs, prompt chaining, function calling, and structured outputs.</p>
              </div>
            </div>

            <div class="cert-card" @mousemove="handleCardMouseMove">
              <div class="cert-icon-box rag-accent">
                <Database :size="20" />
              </div>
              <div class="cert-info">
                <span class="cert-kicker">KNOWLEDGE RETRIEVAL</span>
                <h4>RAG & Context Injection</h4>
                <p>Vector databases, semantic search, and document grounded AI query systems.</p>
              </div>
            </div>

            <div class="cert-quote-box">
              <Sparkles :size="18" />
              <span>"Continuous iteration: Build fast, automate smart, eliminate busywork."</span>
            </div>
          </div>
        </div>
      </section>

      <!-- SKILLS SECTION -->
      <section id="skills" class="skills section-wrap section-block">
        <div class="section-kicker">
          <span class="kicker-num">03</span>
          <span class="kicker-divider">/</span>
          <span>MY TOOLKIT</span>
        </div>

        <div class="section-heading-row">
          <h2>
            The right tools<br />
            <span class="gradient-text">for intelligent workflows.</span>
          </h2>
          <p>
            My toolkit spans workflow orchestration, AI-powered decision making, and the technical building blocks that connect disparate software ecosystems.
          </p>
        </div>

        <div class="skills-grid">
          <div
            v-for="(group, index) in skillGroups"
            :key="group.title"
            class="skill-card"
            @mousemove="handleCardMouseMove"
          >
            <div class="skill-card-header">
              <div class="skill-card-icon">
                <component :is="group.icon" :size="18" />
              </div>
              <span class="skill-index">0{{ index + 1 }}</span>
            </div>

            <div class="skill-card-body">
              <span class="skill-subtitle">{{ group.subtitle }}</span>
              <h3>{{ group.title }}</h3>
              <div class="skill-pills">
                <span v-for="skill in group.items" :key="skill" class="skill-pill">
                  {{ skill }}
                </span>
              </div>
            </div>
          </div>
        </div>

        <div class="skill-bottom-banner">
          <span class="tiny-cross">✳</span>
          <span class="banner-text">ALWAYS LEARNING, ALWAYS ITERATING</span>
          <span class="banner-line"></span>
          <span class="banner-sub">HAVE A NEW API OR TOOL? LET'S CONNECT IT.</span>
        </div>
      </section>

      <!-- SERVICES SECTION -->
      <section id="services" class="services section-wrap section-block">
        <div class="section-kicker">
          <span class="kicker-num">04</span>
          <span class="kicker-divider">/</span>
          <span>WHAT I CAN BUILD FOR YOU</span>
        </div>

        <div class="section-heading-row">
          <h2>
            Make your systems<br />
            <span class="gradient-text">work on autopilot.</span>
          </h2>
          <p>
            Eliminate repetitive tasks, bridge disconnected software, and deploy autonomous AI assistants customized to your exact operations.
          </p>
        </div>

        <div class="service-list">
          <article
            v-for="service in services"
            :key="service.n"
            class="service-row"
            @mousemove="handleCardMouseMove"
          >
            <span class="service-number">{{ service.n }}</span>
            <div class="service-icon">
              <component :is="service.icon" :size="20" />
            </div>
            <div class="service-copy">
              <h3>{{ service.title }}</h3>
              <p>{{ service.desc }}</p>
              <div class="service-highlights">
                <span v-for="h in service.highlights" :key="h">✓ {{ h }}</span>
              </div>
            </div>
            <div class="service-action">
              <a href="#contact" class="service-link-circle" aria-label="Inquire about service">
                <ArrowUpRight :size="18" />
              </a>
            </div>
          </article>
        </div>
      </section>

      <!-- PROJECTS SECTION -->
      <section id="projects" class="projects section-wrap section-block">
        <div class="section-kicker">
          <span class="kicker-num">05</span>
          <span class="kicker-divider">/</span>
          <span>SELECTED AUTOMATIONS</span>
        </div>

        <div class="section-heading-row">
          <h2>
            Ideas turned into<br />
            <span class="gradient-text">intelligent workflows.</span>
          </h2>
          <p>
            Real-world builds showcasing AI agents, automated publication pipelines, and retrieval-augmented systems.
          </p>
        </div>

        <div class="project-grid">
          <article
            v-for="project in projects"
            :key="project.number"
            class="project-card"
            @mousemove="handleCardMouseMove"
          >
            <div class="project-thumb-box">
              <div class="thumb-topline">
                <span class="thumb-tag">{{ project.badge }}</span>
                <span class="thumb-num">PROJECT / {{ project.number }}</span>
              </div>

              <!-- Visual Representation of Each Project -->
              <div v-if="project.thumb === 'agent'" class="thumb-visual visual-agent">
                <div class="agent-preview-nodes">
                  <div class="p-node"><Bot :size="16" /><span>AI Router</span></div>
                  <div class="p-wire"></div>
                  <div class="p-node"><Mail :size="16" /><span>Gmail</span></div>
                  <div class="p-wire"></div>
                  <div class="p-node"><Database :size="16" /><span>Drive</span></div>
                </div>
                <div class="pulse-indicator">
                  <span class="pulse-dot"></span> 3 Sub-Agents Active
                </div>
              </div>

              <div v-else-if="project.thumb === 'linkedin'" class="thumb-visual visual-linkedin">
                <div class="linkedin-preview-card">
                  <div class="lp-header">
                    <Linkedin :size="16" />
                    <span>Auto Post Generator</span>
                    <span class="lp-status">SCHEDULED</span>
                  </div>
                  <div class="lp-lines">
                    <span></span><span></span><span></span>
                  </div>
                  <div class="lp-footer">
                    <Sparkles :size="13" /> RAG Powered Source Grounding
                  </div>
                </div>
              </div>

              <div v-else class="thumb-visual visual-rag">
                <div class="rag-preview-card">
                  <div class="rag-search-box">
                    <Database :size="15" />
                    <span>Vector Similarity Search</span>
                  </div>
                  <div class="rag-results">
                    <div class="rag-chunk"><span>Doc #1:</span> Semantic match (97%)</div>
                    <div class="rag-chunk"><span>Doc #2:</span> Context retrieved (91%)</div>
                  </div>
                </div>
              </div>
            </div>

            <div class="project-info">
              <div class="project-meta">
                <span class="project-type">{{ project.type }}</span>
                <span class="project-stat-pill">{{ project.stats }}</span>
              </div>

              <h3 class="project-title">{{ project.title }}</h3>
              <p class="project-description">{{ project.description }}</p>

              <div class="project-tags">
                <span v-for="tag in project.tags" :key="tag">{{ tag }}</span>
              </div>

              <a class="project-link" :href="project.link">
                <span>Explore Details</span>
                <ArrowUpRight :size="15" />
              </a>
            </div>
          </article>
        </div>

        <div class="project-footnote">
          <span class="tiny-cross">✳</span>
          <span>Project repos, demos, and live workflow templates will be linked next!</span>
        </div>
      </section>

      <!-- CONTACT SECTION -->
      <section id="contact" class="contact section-wrap section-block">
        <div class="contact-card" @mousemove="handleCardMouseMove">
          <div class="contact-grid-bg"></div>

          <div class="contact-content">
            <div class="section-kicker">
              <span class="kicker-num">06</span>
              <span class="kicker-divider">/</span>
              <span>YOUR NEXT WORKFLOW STARTS HERE</span>
            </div>

            <h2>
              Have a process that needs<br />
              <span class="gradient-text">a little AI magic?</span>
            </h2>

            <p>
              Tell me what's repetitive, manual, or slowing your team down. Let's design and deploy an autonomous automation tailored to your exact workflow.
            </p>

            <div class="contact-action-row">
              <a class="button button-primary" href="mailto:menna.hamed.cs@gmail.com">
                <Mail :size="16" />
                <span>Let's Build Something Useful</span>
                <ArrowUpRight :size="16" />
              </a>

              <button class="copy-email-btn" @click="copyEmail">
                <Check v-if="emailCopied" :size="15" />
                <Copy v-else :size="15" />
                <span>{{ emailCopied ? 'Copied to Clipboard!' : 'Copy Email' }}</span>
              </button>
            </div>
          </div>

          <div class="contact-side">
            <!-- Animated Planetary Orbit Core -->
            <div class="contact-orbit">
              <div class="contact-orbit-inner">
                <Workflow :size="32" />
              </div>
              <span class="orbit-satellite sat-1"><Bot :size="13" /></span>
              <span class="orbit-satellite sat-2"><Zap :size="13" /></span>
              <span class="orbit-satellite sat-3"><Database :size="13" /></span>
            </div>

            <!-- Direct Social & Network Links -->
            <div class="contact-links">
              <a href="mailto:mennahamedmakram05@gmail.com">
                <Mail :size="16" />
                <span>EMAIL</span>
                <span class="link-label">mennahamedmakram05@gmail.com</span>
                <ArrowUpRight :size="14" />
              </a>
              <a href="https://www.linkedin.com/in/menna-hamed-/" target="_blank" rel="noreferrer">
                <Linkedin :size="16" />
                <span>LINKEDIN</span>
                <span class="link-label">Menna Hamed</span>
                <ArrowUpRight :size="14" />
              </a>
              <a href="https://github.com/mena-hamed" target="_blank" rel="noreferrer">
                <Github :size="16" />
                <span>GITHUB</span>
                <span class="link-label">menna-hamed</span>
                <ArrowUpRight :size="14" />
              </a>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- FOOTER -->
    <footer class="footer section-wrap">
      <a class="brand" href="#home">
        <span class="brand-mark">
          <Workflow :size="16" />
        </span>
        <span class="brand-text">MENNA<span class="brand-dot">.</span></span>
      </a>

      <span class="footer-note">ENGINEERED FOR EFFICIENCY · BUILT TO AUTOMATE</span>

      <a class="back-top" href="#home">
        <span>BACK TO TOP</span>
        <ArrowUpRight :size="14" />
      </a>

      <span class="copyright">© {{ year }} MENNA HAMED · ALL RIGHTS RESERVED</span>
    </footer>
  </div>
</template>
