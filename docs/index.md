---
title: ""
template: "home.html"
hide:
  - navigation
  - toc
---

<style>
  /* =================================================================== */
  /* 1. THEME-AWARE STYLES & ANIMATIONS                                */
  /* =================================================================== */
  :root {
    --primary-color: #7C3AED;
    --accent-color: #EC4899;
    --cream-color: #FDE68A;
    --card-bg-color: var(--md-code-bg-color);
    --card-border-color: var(--md-default-fg-color--lightest);
    --button-text-color: #ffffff;
    --button-bg-color: var(--primary-color);
    --button-hover-bg-color: var(--accent-color);
  }
  [data-md-color-scheme="slate"] {
    --primary-color: #7C3AED;
    --accent-color: #EC4899;
    --cream-color: #FDE68A;
    --card-bg-color:rgb(0, 0, 0);
    --card-border-color:rgb(28, 28, 28);
    --button-text-color: #ffffff;
    --button-bg-color: var(--primary-color);
    --button-hover-bg-color: var(--accent-color);
  }

  .gradient-text {
    background: linear-gradient(90deg, #7C3AED, #EC4899, #F59E0B, #FDE68A, #7C3AED);
    background-size: 200% auto;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    color: transparent !important;
    animation: gradient-animation 5s linear infinite;
  }
  .gradient-text-secondary {
    background: linear-gradient(90deg, #10B981, #3B82F6, #8B5CF6, #EC4899, #10B981);
    background-size: 200% auto;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    color: transparent !important;
    animation: gradient-animation 4s linear infinite;
  }
  @keyframes gradient-animation { to { background-position: 200% center; } }
  @keyframes fadeInUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes pulse { 0%, 100% { transform: scale(1); } 50% { transform: scale(1.05); } }
  @keyframes float { 0%, 100% { transform: translateY(0px); } 50% { transform: translateY(-10px); } }

  /* =================================================================== */
  /* 2. LAYOUT & HERO SECTION                                          */
  /* =================================================================== */
  .modern-scroll-indicator {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .scroll-arrow-down {
    font-size: 2rem;
    color: #7C3AED;
    animation: scrollDown 2s ease-in-out infinite;
    cursor: pointer;
    transition: all 0.3s ease;
    display: inline-block;
    position: relative;
  }
  
  .scroll-arrow-down:hover {
    transform: scale(1.2);
    color: #EC4899;
  }
  
  @keyframes scrollDown {
    0%, 100% {
      transform: translateY(0);
      opacity: 0.7;
    }
    50% {
      transform: translateY(10px);
      opacity: 1;
    }
  }
  .page-section { 
    padding: 2.2rem 1rem;
    max-width: 100%;
    margin: 0.7rem 0 0.7rem 0;
    animation: fadeInUp 0.8s ease-out;
  }
  .page-section h2 { 
    text-align: center; 
    font-size: 2.8rem; 
    font-weight: 700; 
    margin-bottom: 2.5rem;
    animation: fadeInUp 1s ease-out;
  }
  .page-section h3 { 
    font-size: 1.8rem; 
    font-weight: 600; 
    margin-bottom: 1rem;
    animation: fadeInUp 1.2s ease-out;
  }

  .hero-section {
    padding: 0.2rem 1rem 1.2rem;
    text-align: center;
    max-width: 100%;
    background: linear-gradient(135deg, rgba(124, 58, 237, 0.05), rgba(236, 72, 153, 0.05));
    border-radius: 0;
  }
  .hero-heading {
    font-size: 4.5rem;
    font-weight: 900;
    letter-spacing: -2px;
    margin-bottom: 1rem;
    margin-top: 0;
    animation: pulse 3s ease-in-out infinite;
  }
  .hero-subtitle { 
    font-size: 1.8rem; 
    font-weight: 300; 
    color: var(--md-default-fg-color--light); 
    margin-bottom: 2rem;
    animation: fadeInUp 1.4s ease-out;
  }
  .hero-image-container {
    margin-bottom: 3rem;
    animation: float 6s ease-in-out infinite;
    transform: scale(1.02);
    transition: transform 0.3s ease-out;
  }
  .hero-image-container img {
    max-width: 100%;
    width: 1000px;
    border-radius: 12px;
    box-shadow: 0 20px 50px rgba(0,0,0,0.2);
  }
  
  /* Hero Image */
  .hero-image-animated {
    text-align: center;
    margin: 3rem 0;
    position: relative;
  }
  
  .hero-image-animated img {
    max-width: 100%;
    width: 1000px;
    border-radius: 16px;
    box-shadow: 0 25px 60px rgba(124, 58, 237, 0.15);
  }
  

  
  @keyframes pulse {
    0%, 100% {
      transform: scale(1);
    }
    50% {
      transform: scale(1.05);
    }
  }

  /* =================================================================== */
  /* 3. CARDS, GRIDS, AND STYLED BLOCKS                                */
  /* =================================================================== */
  .feature-grid { 
    display: grid; 
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); 
    gap: 1.5rem; 
    max-width: 1200px;
    margin: 0 auto;
  }
  .feature-card {
    background-color: var(--card-bg-color);
    padding: 2rem;
    border-radius: 15px;
    border: 1px solid var(--card-border-color);
    height: 100%;
    transition: all 0.3s ease;
    animation: fadeInUp 1s ease-out;
  }
  .feature-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0,0,0,0.15);
    border-color: var(--primary-color);
  }
  .feature-card .icon { 
    font-size: 2.5rem; 
    margin-bottom: 1rem; 
    color: var(--primary-color);
    animation: pulse 2s ease-in-out infinite;
  }
  .feature-card h3 { 
    font-size: 1.4rem; 
    margin-bottom: 0.5rem;
    color: var(--md-default-fg-color);
  }

  .styled-block {
    padding: 2.5rem;
    border-radius: 15px;
    margin: 0.7rem 0;
    border: 1px solid rgba(var(--md-primary-fg-color-rgb), 0.2);
    background: linear-gradient(135deg, rgba(var(--md-primary-fg-color-rgb), 0.05), rgba(var(--md-accent-fg-color-rgb), 0.05));
    text-align: center;
    animation: fadeInUp 1s ease-out;
  }
  .spec-pills {
    display: flex; 
    justify-content: center; 
    gap: 1rem; 
    flex-wrap: wrap; 
    margin: 1.5rem 0;
  }
  .spec-pill {
    background-color: rgba(var(--md-primary-fg-color-rgb), 0.1);
    color: var(--primary-color);
    padding: 0.5rem 1rem;
    border-radius: 20px;
    font-weight: 500;
    transition: all 0.3s ease;
  }
  .spec-pill:hover {
    background-color: var(--primary-color);
    color: white;
    transform: scale(1.05);
  }

  /* =================================================================== */
  /* 4. GRADIENT TABS FOR TIERS                                        */
  /* =================================================================== */
  .md-tabs__link--active {
    background: linear-gradient(90deg, var(--primary-color), var(--accent-color));
    color: white !important;
    border-radius: 5px 5px 0 0;
  }
  .md-tabs__item--active .md-tabs__link {
    color: white;
  }

  /* =================================================================== */
  /* 5. BUTTON STYLES - FIXED FOR DARK MODE                           */
  /* =================================================================== */
  .hero-links {
    display: flex;
    justify-content: center;
    gap: 1rem;
    flex-wrap: wrap;
    margin: 2rem 0;
  }
  
  .md-button {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 1rem 2.2rem;
    border-radius: 12px;
    text-decoration: none;
    font-weight: 700;
    font-size: 1.15rem;
    letter-spacing: 0.02em;
    transition: all 0.2s cubic-bezier(.4,1,.7,1);
    border: 2px solid transparent;
    min-width: 160px;
    color: #3b3b3b !important;
    background: linear-gradient(90deg, #ede9fe, #fbcfe8, #fef3c7, #fdf6e3, #ede9fe);
    background-size: 200% auto;
    box-shadow: 0 4px 24px 0 rgba(124,58,237,0.10);
    position: relative;
    z-index: 1;
  }
  .md-button--primary {
    background: linear-gradient(90deg, #ede9fe, #fbcfe8, #fef3c7, #fdf6e3, #ede9fe) !important;
    color: #3b3b3b !important;
    border: 2px solid #fbcfe8;
  }
  .md-button:hover, .md-button:focus {
    filter: brightness(1.08) saturate(1.2);
    box-shadow: 0 8px 32px 0 rgba(124,58,237,0.18);
    color: #222 !important;
    text-decoration: none;
    outline: none;
  }
  
  .md-button--primary:hover {
    background: linear-gradient(135deg, var(--accent-color), var(--primary-color));
    color: white !important;
  }

  /* =================================================================== */
  /* 6. WHY SUPEROPTIX SECTION                                         */
  /* =================================================================== */
  .why-section {
    background: linear-gradient(135deg, rgba(124, 58, 237, 0.08), rgba(236, 72, 153, 0.08));
    padding: 4rem 1rem;
    margin: 0.7rem 0;
    border-radius: 0;
  }
  
  .challenge-solution-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    max-width: 1200px;
    margin: 0 auto;
  }
  
  .challenge-card, .solution-card {
    background: var(--card-bg-color);
    padding: 2.5rem;
    border-radius: 15px;
    border: 1px solid var(--card-border-color);
    transition: all 0.3s ease;
    animation: fadeInUp 1s ease-out;
  }
  
  .challenge-card:hover, .solution-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 40px rgba(0,0,0,0.1);
  }
  
  .challenge-card h3 {
    color: #EF4444;
    font-size: 2rem;
    margin-bottom: 1rem;
  }
  
  .solution-card h3 {
    color: #10B981;
    font-size: 2rem;
    margin-bottom: 1rem;
  }

  /* =================================================================== */
  /* 7. FINAL CTA & MISC                                               */
  /* =================================================================== */
  .cta-section { 
    text-align: center; 
    padding: 4rem 1rem; 
    background: linear-gradient(135deg, var(--card-bg-color), rgba(124, 58, 237, 0.05));
    border-radius: 15px; 
    margin: 0.7rem 0;
    animation: fadeInUp 1s ease-out;
  }
  .final-word { 
    text-align: center; 
    margin-top: 3rem; 
    color: var(--md-default-fg-color--light);
    font-style: italic;
    animation: fadeInUp 1.2s ease-out;
  }

  /* =================================================================== */
  /* 8. RESPONSIVE DESIGN                                              */
  /* =================================================================== */
  @media (max-width: 768px) {
    .hero-heading { font-size: 3rem; }
    .hero-subtitle { font-size: 1.4rem; }
    .page-section h2 { font-size: 2.2rem; }
    .challenge-solution-grid { grid-template-columns: 1fr; }
    .hero-links { flex-direction: column; align-items: center; }
    .md-button { width: 100%; max-width: 300px; }
  }

  .marriage-section {
    margin: 3rem 0 2rem 0;
    text-align: center;
  }
  .marriage-heading {
    font-size: 2.5rem;
    font-weight: 900;
    margin-bottom: 2.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
  }
  .marriage-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
    gap: 2rem;
    max-width: 950px;
    margin: 0 auto;
  }
  .marriage-card {
    background: linear-gradient(135deg, #fff 80%, #f3e8ff 100%);
    border-radius: 22px;
    border: 2.5px solid;
    border-image: linear-gradient(90deg, #ec4899, #a78bfa, #f59e0b) 1;
    box-shadow: 0 4px 32px 0 rgba(124,58,237,0.10);
    padding: 2.5rem 1.5rem 2.2rem 1.5rem;
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 220px;
  }
  .marriage-emoji {
    font-size: 2.7rem;
    margin-bottom: 1.1rem;
  }
  .marriage-title {
    font-size: 1.25rem;
    font-weight: 700;
    margin-bottom: 0.7rem;
  }
  .marriage-desc {
    font-size: 1.08rem;
    color: #444;
  }

  /* DSPy/Agentic Special Cards (Dark) */
  .gradient-card-dark {
    background: #232336;
    border-radius: 22px;
    border: 2.5px solid;
    border-image: linear-gradient(90deg, #ec4899, #a78bfa, #f59e0b) 1;
    box-shadow: 0 4px 32px 0 rgba(124,58,237,0.10);
    padding: 2.5rem 2rem 2.2rem 2rem;
    margin: 1.5rem 0;
    position: relative;
    z-index: 2;
    text-align: left;
    color: #e5e5f7;
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
  }
  .gradient-card-dark h2 {
    font-size: 2.1rem;
    font-weight: 800;
    margin-bottom: 1.2rem;
    display: flex;
    align-items: center;
    gap: 0.7rem;
    letter-spacing: -1px;
    color: #fff;
  }
  .gradient-card-dark .big-emoji {
    font-size: 2.5rem;
    margin-right: 0.5rem;
    flex-shrink: 0;
  }
  .gradient-card-dark p {
    font-size: 1.15rem;
    margin-bottom: 0.5rem;
    color: #c7bfff;
  }
  .gradient-card-dark strong {
    color: #a78bfa;
    font-weight: 700;
  }
  .gradient-card-dark em {
    color: #ec4899;
    font-style: normal;
    font-weight: 600;
  }
  .gradient-card-dark ul {
    margin: 1rem 0 0 1.2rem;
    font-size: 1.08rem;
    color: #e5e5f7;
  }
  /* Purple-only gradient for step headings */
  .gradient-text-purple {
    background: linear-gradient(90deg, #7C3AED, #a78bfa);
    background-size: 200% auto;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    color: transparent;
    animation: gradient-animation 5s linear infinite;
  }
  /* Static gradient for non-animated gradient text */
  .gradient-static {
    animation: none !important;
  }
</style>

<!-- =================================================================== -->
<!-- HERO SECTION                                                        -->
<!-- =================================================================== -->
<div class="hero-section enhanced-hero-bg">
  <h1 class="hero-heading gradient-animated">👑 SUPEROPTIX AI</h1>
  <p class="hero-tagline gradient-soft">Full Stack Agentic AI Framework</p>
  <div class="hero-free-tiers">
    <span class="free-tiers-badge">🎉 Oracle & Genies are FREE to try!</span>
    <div class="tier-system-link">
      <a href="guides/tiers" class="tier-link">📊 View All Tiers →</a>
    </div>
  </div>
  <div class="hero-subtitle-inline">
    🧪 Evaluation-First ⚡ Optimization-Core 🕸️ Multi-Agent Orchestration
  </div>
  <p class="hero-desc gradient-text-secondary">Powered by DSPy. Refined by Superagentic AI.</p>
  <div class="hero-links">
    <a class="md-button md-button--primary" href="quick-start"><span style="margin-right:0.5em;">🚀</span>Quick Start</a>
    <a class="md-button" href="introduction"><span style="margin-right:0.5em;">📖</span>Learn More</a>
    <a class="md-button" href="guides/"><span style="margin-right:0.5em;">📚</span>Guides</a>
  </div>
  <div class="modern-scroll-indicator">
    <div class="scroll-arrow-down">↓</div>
  </div>
</div>

<style>
  .enhanced-hero-bg {
    background: radial-gradient(ellipse at 50% 30%, rgba(124,58,237,0.10) 0%, rgba(236,72,153,0.08) 40%, rgba(255,255,255,0.01) 100%);
    box-shadow: 0 2px 32px 0 rgba(124,58,237,0.04);
    padding-top: 2.5rem;
    padding-bottom: 2.5rem;
  }
  [data-md-color-scheme="slate"] .enhanced-hero-bg {
    background: radial-gradient(ellipse at 50% 30%, rgba(30,58,138,0.15) 0%, rgba(88,28,135,0.12) 30%, rgba(153,27,27,0.08) 60%, rgba(8,8,12,0.99) 100%);
  }
  .gradient-animated {
    background: linear-gradient(90deg, #7C3AED, #EC4899, #F59E0B, #FDE68A, #7C3AED);
    background-size: 200% auto;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    color: transparent !important;
    animation: gradient-animation 5s linear infinite;
    font-size: 4.5rem;
    font-weight: 900;
    letter-spacing: -2px;
    margin-bottom: 0.5rem;
    margin-top: 0;
    text-align: center;
  }
  .gradient-soft {
    background: linear-gradient(90deg, #60a5fa, #a78bfa, #818cf8, #a78bfa, #60a5fa);
    background-size: 200% auto;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    color: transparent !important;
    font-size: 2rem;
    font-weight: 700;
    text-align: center;
    margin-bottom: 1.2rem;
    text-shadow: 0 2px 8px rgba(124,58,237,0.08);
  }
  .hero-free-tiers {
    text-align: center;
    margin-bottom: 1.5rem;
  }
  .free-tiers-badge {
    display: inline-block;
    background: linear-gradient(90deg, #10B981, #3B82F6, #8B5CF6);
    color: white;
    padding: 0.5rem 1.2rem;
    border-radius: 25px;
    font-weight: 600;
    font-size: 1rem;
    box-shadow: 0 4px 15px rgba(16, 185, 129, 0.3);
    animation: pulse 2s ease-in-out infinite;
  }
  .tier-system-link {
    margin-top: 0.8rem;
  }
  .tier-link {
    color: var(--primary-color);
    text-decoration: none;
    font-weight: 500;
    font-size: 0.95rem;
    transition: all 0.3s ease;
    border-bottom: 1px solid transparent;
  }
  .tier-link:hover {
    color: var(--accent-color);
    border-bottom-color: var(--accent-color);
    text-decoration: none;
  }
  .hero-subtitle-inline {
    font-size: 1.4rem;
    font-weight: 300;
    color: var(--md-default-fg-color--light);
    text-align: center;
    margin-bottom: 2rem;
    line-height: 1.2;
  }
  .hero-subtitle-compact {
    font-size: 1.7rem;
    font-weight: 500;
    color: var(--md-default-fg-color--light);
    margin-bottom: 1.2rem;
    line-height: 1.2;
    text-align: center;
    max-width: 900px;
    margin-left: auto;
    margin-right: auto;
  }
  .hero-desc {
    font-size: 1.15rem;
    font-weight: 500;
    margin-bottom: 2.2rem;
    text-align: center;
  }
  .hero-links {
    display: flex;
    justify-content: center;
    gap: 1.2rem;
    flex-wrap: wrap;
    margin: 2rem 0 1.5rem 0;
  }
  .md-button {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 1rem 2.2rem;
    border-radius: 12px;
    border: 2px solid transparent;
    font-weight: 700;
    font-size: 1.15rem;
    letter-spacing: 0.02em;
    transition: all 0.2s cubic-bezier(.4,1,.7,1);
    min-width: 160px;
    color: #3b3b3b !important;
    background: linear-gradient(90deg, #ede9fe, #fbcfe8, #fef3c7, #fdf6e3, #ede9fe);
    background-size: 200% auto;
    box-shadow: 0 4px 24px 0 rgba(124,58,237,0.10);
    position: relative;
    z-index: 1;
    margin-bottom: 0.5rem;
  }
  .md-button--primary {
    background: linear-gradient(90deg, #fbc2eb, #a6c1ee, #fbc2eb) !important;
    color: #3b3b3b !important;
    border: 2px solid #fbcfe8;
    box-shadow: 0 6px 32px 0 rgba(124,58,237,0.13);
  }
  .md-button:hover, .md-button:focus {
    filter: brightness(1.08) saturate(1.2);
    box-shadow: 0 8px 32px 0 rgba(124,58,237,0.18);
    color: #222 !important;
    text-decoration: none;
    outline: none;
    transform: scale(1.04);
  }
  .md-button span {
    font-size: 1.2em;
    margin-right: 0.5em;
  }
  @media (max-width: 768px) {
    .gradient-animated { font-size: 2.3rem; }
    .gradient-soft { font-size: 1.2rem; }
    .hero-subtitle-compact { font-size: 1.1rem; }
    .hero-links { flex-direction: column; align-items: center; }
    .md-button { width: 100%; max-width: 300px; }
  }
</style>

<!-- Hero Image Section -->
<div class="hero-image-animated">
  <img src="superoptix_hero.png" alt="SuperOptiX Hero" />
</div>

<!-- =================================================================== -->
<!-- WHAT IS SUPEROPTIX?                                                 -->
<!-- =================================================================== -->
<div class="page-section">
  <h2>🔍 What is <span class="gradient-text">SuperOptiX</span>?</h2>
  <div style="font-size: 1.2rem; text-align: center; max-width: 800px; margin: 0 auto;">
    <p>SuperOptiX is a <strong>Full-Stack Agentic AI Framework</strong> designed to help developers and teams build optimized, production-grade AI agents from day one. It brings together declarative agent specification, automatic optimization, built-in evaluation, and multi-agent orchestration—all grounded in the principles of test-driven development and context engineering.</p>
    <p>Unlike most frameworks that bolt on evals and monitoring as an afterthought, SuperOptiX makes <strong>evaluation, optimization, and guardrails core to the development lifecycle</strong>. Whether you're deploying a single agent or a coordinated system of agents, SuperOptiX gives you the power to go from prototype to production—faster, safer, and smarter.</p>
    <p style="font-weight: 600;">🎯 Declarative by Design. ⚡ Optimized by Default. 🎼 Orchestration-Ready.</p>
    <p>With its native DSL (SuperSpec), DSPy-based optimization layer, structured agent tiers (Oracles, Genies, Protocols, Superagents, Sovereigns), and full-stack abstractions, SuperOptiX empowers you to build reliable, adaptive, and intelligent agentic systems—without reinventing the wheel.</p>
  </div>
</div>

<!-- =================================================================== -->
<!-- CORE FEATURES                                                       -->
<!-- =================================================================== -->
<div class="page-section">
  <h2><span class="gradient-text">⚡ Core Features</span></h2>
  <div class="feature-grid">
    <div class="feature-card"><h3><span class="icon">🎯</span> Evaluation-First by Design</h3><p>Agents are defined and validated using BDD-style specs before orchestration. Every agent starts with behavior-driven goals.</p></div>
    <div class="feature-card"><h3><span class="icon">✅</span> BDD-Style Spec Runner</h3><p>Write agent specs in a human-readable DSL (SuperSpec), execute them as tests, and optimize your agents iteratively—just like TDD for AI.</p></div>
    <div class="feature-card"><h3><span class="icon">⚙️</span> DSPy-Powered Optimization Engine</h3><p>SuperOptiX builds on DSPy for declarative optimization of agents, prompts, chains, and protocols—with transparent tracing and tuning.</p></div>
    <div class="feature-card"><h3><span class="icon">🚀</span> Agentic DSPy Evolution</h3><p>Custom modules for multi-agent coordination, protocol support (MCP, A2A), and advanced agentic scenarios beyond standard DSPy.</p></div>
    <div class="feature-card"><h3><span class="icon">🧩</span> Modular Optimization Architecture</h3><p>DSPy as primary adapter with framework-agnostic design. Ready to integrate future optimization frameworks while maintaining user choice.</p></div>
    <div class="feature-card"><h3><span class="icon">✍️</span> Prompt & Context Optimization</h3><p>Automatically decompose, optimize, and test prompts and embedded context for better grounding, relevance, and goal alignment.</p></div>
    <div class="feature-card"><h3><span class="icon">⚡</span> Automated Agent Pipeline Generation</h3><p>Define your high-level spec, and SuperOptiX generates the entire agent optimization pipeline—including DSPy Signatures, Modules, Evaluation, and Optimization—from prompt tuning to memory wiring.</p></div>
    <div class="feature-card"><h3><span class="icon">📄</span> SuperSpec DSL</h3><p>A domain-specific language to declaratively define agents, roles, evaluation specs, tools, and coordination flows. Think Gherkin for agents.</p></div>
    <div class="feature-card"><h3><span class="icon">🧠</span> Inbuilt Memory System</h3><p>Modular memory layers (short-term, vector, long-term, ephemeral) that can be composed per agent, protocol, or tier.</p></div>
    <div class="feature-card"><h3><span class="icon">📈</span> Built-in Evals</h3><p>Native evaluation suite for functional, behavioral, and optimization-level tests. Run metrics, comparisons, and scenario-based scoring.</p></div>
    <div class="feature-card"><h3><span class="icon">📦</span> Context Engineering Layer</h3><p>Structured context frames, templating, prompt modularization, and evaluation-backed refactoring tools.</p></div>
    <div class="feature-card"><h3><span class="icon">🤖</span> Model & Inference Management</h3><p>Plug-and-play with OpenAI, Anthropic, HuggingFace, Ollama, Groq, or Apple MLX. Swap models dynamically, locally or via API.</p></div>
    <div class="feature-card"><h3><span class="icon">🏪</span> Marketplace for Prebuilt Agents & Tools</h3><p>Discover and deploy pre-optimized Genies, Protocols, memory templates, and tooling components. Build faster with reusable agents.</p></div>
    <div class="feature-card"><h3><span class="icon">📊</span> AgentOps Layer</h3><p>Observability, replay, versioning, and adaptive agent debugging. Perfect for production feedback and runtime evaluation.</p></div>
  </div>
</div>

<!-- =================================================================== -->
<!-- SUPEROPTIX AND DSPY                                                 -->
<!-- =================================================================== -->
<div class="page-section">
  <h2><span class="gradient-text">🧠 SuperOptiX & DSPy</span></h2>
  
  <div class="dspy-container">
    <!-- Hero Section -->
    <div class="dspy-hero">
      <h3 class="gradient-text">Agentic DSPy - Taking Optimization to the Next Level</h3>
      <p>
        <strong>SuperOptiX harnesses the full power of DSPy's optimization principles and elevates them to the agentic layer.</strong><br>
        We're not just a DSPy wrapper—we're <em>Agentic DSPy</em>.
      </p>
    </div>

    <p class="dspy-intro">
      DSPy is the <strong>most powerful optimization framework</strong> in the AI space and the <strong>only framework that systematically optimizes</strong> language model programs. SuperOptiX recognizes this strength and builds upon DSPy's revolutionary optimization-first approach, extending it specifically for agentic AI and multi-agent orchestration.
    </p>

    <!-- Why DSPy Section -->
    <div class="dspy-section">
      <h3>🎯 Why DSPy is Perfect for Agentic Systems</h3>
      <p>DSPy's <strong>iterative optimization principles</strong> align perfectly with <strong>Test-Driven Development (TDD)</strong> and <strong>Behavior-Driven Development (BDD)</strong> methodologies. It's as if DSPy was designed specifically for building reliable, testable agentic systems:</p>
      
      <div class="comparison-table">
        <table>
          <thead>
            <tr>
              <th>DSPy Core Strength</th>
              <th>Agentic System Need</th>
              <th>SuperOptiX Innovation</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><strong>Optimization-First</strong></td>
              <td>Reliable agent behavior</td>
              <td>BDD-style agent specifications</td>
            </tr>
            <tr>
              <td><strong>Assertions & Evaluations</strong></td>
              <td>Agent validation</td>
              <td>Multi-tier evaluation framework</td>
            </tr>
            <tr>
              <td><strong>Signature Generation</strong></td>
              <td>Context engineering</td>
              <td>Advanced prompt optimization</td>
            </tr>
            <tr>
              <td><strong>Module Composition</strong></td>
              <td>Multi-agent coordination</td>
              <td>Orchestra-level optimization</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <!-- SuperOptiX Evolution Section -->
    <div class="dspy-section">
      <h3>🚀 SuperOptiX: The Agentic Evolution of DSPy</h3>
      
      <h4>Advanced Custom Modules for Agentic AI</h4>
      <p>SuperOptiX includes sophisticated modules designed specifically for agentic and multi-agent scenarios that extend beyond the standard DSPy offering:</p>
      
      <div class="feature-grid">
        <div class="feature-card">
          <div class="feature-icon">🤝</div>
          <h4 class="gradient-text">Multi-Agent Coordination Modules</h4>
          <p>Advanced orchestration patterns for complex multi-agent scenarios</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">🔗</div>
          <h4 class="gradient-text">Protocol Support Modules</h4>
          <p>MCP (Model Context Protocol) and A2A (Agent-to-Agent) integration</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">🧠</div>
          <h4 class="gradient-text">Memory-Optimized Modules</h4>
          <p>Context-aware memory management across agent interactions</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">🛡️</div>
          <h4 class="gradient-text">Guardrail Modules</h4>
          <p>Safety and compliance checks for production deployment</p>
        </div>
      </div>

      <h4>⚡ Automatic Pipeline Generation from Specifications</h4>
      <p>SuperOptiX uses DSPy's optimization engine to automatically generate entire agent pipelines from high-level specifications:</p>
      
      <div class="pipeline-container">
        <div class="pipeline-steps">
          <div class="pipeline-step">
            <div class="step-number">1</div>
            <div class="step-content">
              <strong class="gradient-text">Auto-generates DSPy Signatures</strong> based on agent role and context
            </div>
          </div>
          <div class="pipeline-step">
            <div class="step-number">2</div>
            <div class="step-content">
              <strong class="gradient-text">Creates optimized DSPy Modules</strong> for multi-step reasoning
            </div>
          </div>
          <div class="pipeline-step">
            <div class="step-number">3</div>
            <div class="step-content">
              <strong class="gradient-text">Builds complete evaluation pipelines</strong> with behavioral tests
            </div>
          </div>
          <div class="pipeline-step">
            <div class="step-number">4</div>
            <div class="step-content">
              <strong class="gradient-text">Generates optimization workflows</strong> tailored to agent requirements
            </div>
          </div>
        </div>
      </div>

      <h4>🧩 Modular Optimization Architecture</h4>
      <p>SuperOptiX takes a <strong>modular approach</strong> to optimization and evaluation:</p>
      
      <div class="architecture-grid">
        <div class="arch-item">
          <div class="arch-icon">🔧</div>
          <div class="arch-content">
            <strong class="gradient-text">DSPy as Primary Adapter</strong>
            Leverages DSPy's proven optimization capabilities
          </div>
        </div>
        <div class="arch-item">
          <div class="arch-icon">🌐</div>
          <div class="arch-content">
            <strong class="gradient-text">Framework Agnostic</strong>
            Ready to integrate other optimization frameworks as they emerge
          </div>
        </div>
        <div class="arch-item">
          <div class="arch-icon">⚙️</div>
          <div class="arch-content">
            <strong class="gradient-text">Custom Optimization Layer</strong>
            Users can implement specialized optimization strategies
          </div>
        </div>
        <div class="arch-item">
          <div class="arch-icon">🎯</div>
          <div class="arch-content">
            <strong class="gradient-text">Choice and Flexibility</strong>
            Multiple optimization paths for different use cases
          </div>
        </div>
      </div>
    </div>

    <!-- Perfect Marriage Section -->
    <div class="dspy-section">
      <h3>💫 The Perfect Marriage: DSPy + Agentic AI</h3>
      <p>DSPy's emphasis on <strong>systematic optimization</strong>, <strong>evaluation-driven development</strong>, and <strong>composable modules</strong> makes it the ideal foundation for building robust agentic systems. SuperOptiX extends this foundation with:</p>
      
      <div class="feature-grid">
        <div class="feature-card">
          <div class="feature-icon">📝</div>
          <h4 class="gradient-text">Application-Layer Abstractions</h4>
          <p>SuperSpec DSL for declarative agent building</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">✅</div>
          <h4 class="gradient-text">BDD Testing Framework</h4>
          <p>Behavior-driven specifications for agent validation</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">🏛️</div>
          <h4 class="gradient-text">Multi-Tier Architecture</h4>
          <p>Progressive complexity from Oracles to Sovereigns</p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">🛠️</div>
          <h4 class="gradient-text">Production-Ready Features</h4>
          <p>Memory management, observability, and deployment tools</p>
        </div>
      </div>
    </div>

    <div class="dspy-conclusion">
      <p>SuperOptiX transforms DSPy from a research framework into a production-ready agentic AI platform.</p>
    </div>
  </div>
</div>

<style>
/* DSPy Section Styles - Dark Mode Compatible */
.dspy-container {
  max-width: 1200px;
  margin: 0 auto;
}

.dspy-hero {
  background: linear-gradient(135deg, rgba(124, 58, 237, 0.08), rgba(236, 72, 153, 0.08));
  border-radius: 16px;
  padding: 3rem 2rem;
  margin: 2rem 0;
  text-align: center;
  border: 1px solid rgba(124, 58, 237, 0.15);
}

.dspy-hero h3 {
  font-size: 2rem;
  margin-bottom: 1.5rem;
}

.dspy-hero p {
  font-size: 1.2rem;
  line-height: 1.6;
  max-width: 800px;
  margin: 0 auto;
  color: var(--md-default-fg-color);
}

.dspy-intro {
  text-align: center;
  font-size: 1.2rem;
  max-width: 900px;
  margin: 2rem auto;
  line-height: 1.7;
  color: var(--md-default-fg-color);
}

.dspy-section {
  background: var(--card-bg-color);
  border-radius: 12px;
  padding: 2rem;
  margin: 0.7rem 0;
  border: 1px solid var(--card-border-color);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
}

.dspy-section h3 {
  font-size: 1.6rem;
  color: var(--primary-color);
  margin-bottom: 1.5rem;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.dspy-section h4 {
  font-size: 1.2rem;
  color: var(--accent-color);
  margin: 1.5rem 0 1rem 0;
}

/* Comparison Table */
.comparison-table {
  margin: 2rem 0;
}

.comparison-table table {
  width: 100%;
  border-collapse: collapse;
  background: var(--card-bg-color);
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.comparison-table th {
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
  color: white;
  padding: 1rem;
  text-align: center;
  font-weight: 600;
}

.comparison-table td {
  padding: 1rem;
  text-align: center;
  border-bottom: 1px solid var(--card-border-color);
  color: var(--md-default-fg-color);
}

.comparison-table tr:nth-child(even) {
  background: rgba(var(--md-primary-fg-color-rgb), 0.03);
}

.comparison-table tr:hover {
  background: rgba(var(--primary-color-rgb), 0.05);
}

/* Feature Grid */
.feature-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  margin: 2rem 0;
}

.feature-card {
  background: linear-gradient(135deg, rgba(124, 58, 237, 0.05), rgba(236, 72, 153, 0.05));
  padding: 2rem;
  border-radius: 12px;
  border: 1px solid rgba(124, 58, 237, 0.15);
  text-align: center;
  transition: all 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 25px rgba(124, 58, 237, 0.15);
  border-color: var(--primary-color);
}

.feature-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
  display: block;
}

.feature-card h4 {
  color: var(--primary-color);
  font-size: 1.2rem;
  margin-bottom: 0.8rem;
}

.feature-card p {
  color: var(--md-default-fg-color);
  line-height: 1.5;
}

/* Pipeline Steps */
.pipeline-container {
  background: rgba(var(--primary-color-rgb), 0.03);
  border-radius: 12px;
  padding: 2rem;
  margin: 2rem 0;
}

.pipeline-steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
}

.pipeline-step {
  background: var(--card-bg-color);
  padding: 1.5rem;
  border-radius: 8px;
  border-left: 4px solid var(--primary-color);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}

.step-number {
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
  color: white;
  width: 2.5rem;
  height: 2.5rem;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 1rem;
  margin-bottom: 1rem;
}

.step-content {
  font-weight: 500;
  color: var(--md-default-fg-color);
}

/* Architecture Grid */
.architecture-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
  margin: 2rem 0;
}

.arch-item {
  background: rgba(var(--accent-color-rgb), 0.05);
  padding: 1.5rem;
  border-radius: 8px;
  border-left: 3px solid var(--accent-color);
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.arch-icon {
  font-size: 2rem;
  color: var(--accent-color);
  flex-shrink: 0;
}

.arch-content {
  flex: 1;
}

.arch-content strong {
  display: block;
  margin-bottom: 0.5rem;
  color: var(--accent-color);
}

.arch-content {
  color: var(--md-default-fg-color);
}

/* Conclusion */
.dspy-conclusion {
  text-align: center;
  background: linear-gradient(135deg, rgba(124, 58, 237, 0.08), rgba(236, 72, 153, 0.08));
  border-radius: 12px;
  padding: 2.5rem;
  margin: 3rem 0;
  border: 1px solid rgba(124, 58, 237, 0.15);
}

.dspy-conclusion p {
  font-size: 1.3rem;
  font-weight: 600;
  color: var(--md-default-fg-color);
  margin: 0;
}

/* Responsive Design */
@media (max-width: 768px) {
  .feature-grid {
    grid-template-columns: 1fr;
  }
  
  .pipeline-steps {
    grid-template-columns: 1fr;
  }
  
  .architecture-grid {
    grid-template-columns: 1fr;
  }
  
  .pipeline-step {
    flex-direction: column;
    text-align: center;
  }
  
  .arch-item {
    flex-direction: column;
    text-align: center;
  }
}
</style>



<!-- =================================================================== -->
<!-- SUPERSPEC CTA                                                       -->
<!-- =================================================================== -->
<div class="page-section">
  <div class="styled-block">
    <h2 class="gradient-text">💎 SuperSpec - The Heart of Agent Building</h2>
    <p style="font-size: 1.2rem; max-width: 700px; margin: 1rem auto;">
      <strong>SuperSpec is our declarative DSL that makes agent building as simple as writing a specification.</strong><br>Think of it as "Kubernetes for AI agents" - you describe what you want, and SuperOptiX builds the entire pipeline.
    </p>
    <div class="spec-pills">
      <div class="spec-pill">📝 Declarative Agent Specs</div>
      <div class="spec-pill">✅ BDD-Style Testing</div>
      <div class="spec-pill">⚙️ Auto-Optimization</div>
      <div class="spec-pill">⚡ Pipeline Generation</div>
    </div>
    <div class="hero-links" style="margin-top: 2rem;">
      <a href="guides/superspec" class="md-button md-button--primary">💎 Explore SuperSpec</a>
      <a href="reference/api/superspec" class="md-button">📗 DSL Reference</a>
    </div>
  </div>
</div>

<!-- =================================================================== -->
<!-- WHY SUPEROPTIX SECTION                                              -->
<!-- =================================================================== -->
<div class="why-section">
  <div class="page-section">
    <h2>🤔 Why <span class="gradient-text">SuperOptiX</span>?</h2>
    <div class="challenge-solution-grid">
      <div class="challenge-card">
        <h3>🚨 The Challenge</h3>
        <p>Building production-grade AI agents remains a significant challenge. Most available frameworks are designed for demos, not deployment, and rely on hardcoded prompts with no built-in optimization. This leads to fragile systems and reinvention of common components.</p>
        <p>As a result, <strong>over 95% of AI projects never make it to production</strong>—not due to lack of ambition, but due to lack of the right tooling, standards, and engineering discipline.</p>
        <ul>
          <li>❌ Fragile, hardcoded prompts</li>
          <li>❌ No systematic optimization</li>
          <li>❌ Lack of evaluation frameworks</li>
          <li>❌ Production deployment challenges</li>
        </ul>
      </div>
      <div class="solution-card">
        <h3>✨ Our Solution</h3>
        <p>SuperOptiX AI is the first evolution‑first, behavior‑driven framework that combines:</p>
        <ul>
          <li><strong>✅ Built‑in Evaluation (BDD first)</strong>: Write behavior‑driven specs that serve as executable tests.</li>
          <li><strong>✅ Optimization at the Core</strong>: Data‑driven performance tuning, powered by DSPy.</li>
          <li><strong>✅ Orchestration‑Ready Pipelines</strong>: Kubernetes‑style DSL and multi‑agent coordination.</li>
          <li><strong>✅ Production‑Grade Monitoring</strong>: Guardrails, observability, and safe‑by‑design architecture.</li>
        </ul>
        <p>All within a single, end‑to‑end solution—no stitching together siloed tools.</p>
      </div>
    </div>
  </div>
</div>

<!-- =================================================================== -->
<!-- FREE TIERS CTA                                                      -->
<!-- =================================================================== -->
<div class="page-section" markdown="1">
!!! success "🆓 Start Free Today!"
    **Oracle & Genie tiers are completely FREE to try!** No credit card required.
    
    - 🧙‍♂️ **Oracle Tier**: Simple Q&A and automation - **FREE**
    - 🧞‍♂️ **Genie Tier**: Multi-step reasoning with tools & RAG - **FREE**
    - 🎭 **Protocol Tier+**: Advanced enterprise features - Commercial
    
    **[Get Started Now](quick-start)** | **[View All Tiers](guides/tiers)** | **[Install SuperOptiX](setup)**
</div>

<!-- =================================================================== -->
<!-- NEW TO SUPEROPTIX?                                                  -->
<!-- =================================================================== -->
<div class="page-section" markdown="1">
!!! tip "🎉 New to SuperOptiX?"
    **Start with our [Quick Start Guide](quick-start)** - designed to be your "wow moment" with SuperOptiX!
    
    **Need to set up first?** Check out [Installation](setup) and [LLM Setup](llm-setup) to get everything configured.
    
    Or jump directly to [Create First Genies Agent](tutorials/genies-agent) to get hands-on experience.
</div>

<!-- =================================================================== -->
<!-- WHAT MAKES SUPEROPTIX SPECIAL?                                      -->
<!-- =================================================================== -->
<div class="page-section" markdown="1">
  <h2>🌟 What Makes <span class="gradient-text">SuperOptiX Special?</span></h2>
  <p style="text-align: center; max-width: 800px; margin: 0 auto 2rem auto;">SuperOptiX isn't just another agent framework — it's the <strong>world's first optimization-first, orchestration-ready, evaluation-built Agentic AI framework</strong>. Here's what sets us apart:</p>

  <h3>⚡ Optimization-First Philosophy</h3>
  <p>Traditional AI frameworks treat optimization as an afterthought. SuperOptiX puts it at the core:</p>

| Traditional Approach | SuperOptiX Approach |
|:---|:---|
| ❌ Build → Hope it works | ✅ **Specify → Evaluate → Optimize → Deploy** |
| ❌ Manual prompt tuning | ✅ **Automated DSPy optimization** |
| ❌ No systematic testing | ✅ **BDD-driven evaluation** |
| ❌ Production surprises | ✅ **Safe-by-design validation** |

  <br>

  <h3>🏆 The SuperOptiX Differentiator</h3>

| Feature | SuperOptiX | Other Frameworks |
|:---|:---:|:---:|
| **Agent Optimization** | ✅ Built-in DSPy optimization | ❌ (DSPy exception) |
| **Agent Creation & Orchestration** | ✅ Complete framework | ✅ (basic) |
| **InBuilt Model Management** | ✅ MLX/HF/Ollama/LM Studio | ❌ |
| **BDD/TDD Spec Runner** | ✅ Professional evaluation | ❌ |
| **Local Inference + Memory + RAG** | ✅ Integrated solution | ✅ (external) |
| **DSL for Agent Specs (SuperSpec)** | ✅ Kubernetes-style | ❌ |
| **Tracing & Observability** | ✅ Built-in monitoring | ✅ |

</div>

<!-- =================================================================== -->
<!-- PROGRESSIVE TIER SYSTEM                                             -->
<!-- =================================================================== -->
<div class="page-section" markdown="1">
  <h2><span class="gradient-text">🏗️ Progressive Tier System</span></h2>
  
  !!! info "💼 Commercial Package with Free Tiers"
      **SuperOptiX is a commercial package**, but we offer **Oracle and Genie tiers completely free to try**! This allows you to experience the power of SuperOptiX before considering our commercial tiers (Protocol, Superagent, and Sovereign) for advanced enterprise features.
  
  <p style="text-align: center; max-width: 800px; margin: 0 auto 2rem auto;">Scale from simple to enterprise complexity with our 5-tier architecture inspired by Nick Bostrom's Superintelligence and Sam Altman's AGI stages:</p>

=== "🧙‍♂️ Oracles (Free to Try)"
    **Simple, fast question answering system** that involves interaction with LLMs and responding to your queries. There is no connection to external data and quality of output directly depends on the quality of the LLMs used.
    
    - **Status**: ✅ Available (Free to Try)
    - **What**: Simple, single-purpose agents
    - **Use Case**: Basic automation, simple Q&A
    - **Example**: FAQ bot, data formatter
    - **Complexity**: Low
    - **Cost**: 🆓 Free
    
    **Key Features:**
    - Single-step reasoning
    - Template-based responses
    - Built-in optimization and validations
    
    **Includes:**
    - Any LLM Support, Model Management, Few Shot Optimization, Simple Evals, BDD Spec Runner, Simple Sequential Multi Agent Orchestra, Static Pipelines Code with SuperOptiX DSPy Mixin, Demo Purpose Outputs, Basic tracing and observability

=== "🧞‍♂️ Genies (Free to Try)"
    **Multi-step reasoning agents** that involve interaction with LLMs and external systems like knowledge and tools. This system uses reasoning and action (ReAct) to perform controlled actions on your behalf.
    
    - **Status**: ✅ Available (Free to Try)
    - **What**: Multi-step reasoning agents
    - **Use Case**: Customer service, content creation
    - **Example**: Support agent, content writer
    - **Complexity**: Medium
    - **Cost**: 🆓 Free
    
    **Key Features:**
    - Multi-step reasoning with ReAct
    - Dynamic tool selection and usage
    - Memory integration and learning through RAG
    
    **Includes:**
    - Function calling LLM Support, Custom Function calling DSPy tools, RAG with favorite vectorDB Support, Model Management with MLX, HF, Ollama and LM Studio, Few Shot and Labeled Few Shot Optimization, Simple Evals, Basic DSPy Memory Support, BDD Spec Runner basic metrics, Sequential Multi Agent Orchestra, Static Pipelines Code with SuperOptiX DSPy Mixin, Demo Purpose Outputs with usage tracking, Basic Tool Tracing Observability and Tool call, Multi-Agent Orchestra with demo outputs

=== "🎭 Protocols (Commercial)"
    **Highly advanced tier** with support of industry-evolving protocols like MCP and A2A, covering all features from Oracles and Genies. This layer uses advanced industry protocols to make agents better and communicate with LLMs and each other.
    
    - **Status**: 🔒 Commercial (Contact Us)
    - **What**: Complex workflow agents
    - **Use Case**: Business processes, decision making
    - **Example**: Sales qualification, risk assessment
    - **Complexity**: High
    - **Cost**: 💼 Commercial
    
    **Key Features:**
    - Advanced agents with MCP & A2A protocols
    - Integrate with external APIs, systems, workflows
    
    **Includes:**
    - Everything from Oracles and Genies, Custom Function calling DSPy tools, Agentic RAG with popular vectorDB Support, AgentVectorDB Integration, Advanced Model Management with vLLM, SGLang, TGI servers for Production deployment, Advanced DSPy and Custom Optimizers, Layered Memory Support, Automated Basic Synthetic Data Generation, BDD Spec Runner with advanced metrics and validations, Parallel Multi Agent Orchestra, Controlled DSPy Pipelines (No Mixin), Production Worthy Agent Output format suitable for multi-agent system, Advanced Tracing Observability and Tool, Integration with third party tools like MLflow, Basic Planner → Executor Multi Agent Orchestra, Basic Kubernetes Style Orchestra

=== "🤖 Superagents (Commercial)"
    **Multi-agent systems with coordination** where a lead agent called Superagent may spawn automated subagents to perform tasks and work with other superagents. This involves higher levels of orchestration managed by AgentLines.
    
    - **Status**: 🔒 Commercial (Work in Progress)
    - **What**: Multi-agent systems with coordination
    - **Use Case**: Complex business workflows
    - **Example**: E-commerce platform, research team
    - **Complexity**: Expert
    - **Cost**: 💼 Commercial
    
    **Key Features:**
    - Superagents orchestrating other agents
    - AgentLines for scalable multi-agent governance
    
    **Tentative Features:**
    - Everything from Oracles, Genies and Protocols, Agentic DSPy Pipeline for Superagent, Advanced Model Management with vLLM, SGLang, TGI servers for Production deployment, Integration with high level GPU infra and MLOps tools for deployment, Combination of LLM and Fine Tuned SLMs, Context Management with VectorDBs and Advanced Memory, Agentic BDD Spec Runner within orchestra and AgentLines, Human in the loop interaction based on defined criteria, Integration with third party DevOps, MLOps Cloud providers

=== "👑 Sovereigns (Commercial)"
    **Autonomous AI systems** suitable for large-scale AI operations and enterprise workflows. These are the highest level of AI autonomy with advanced multi-agent orchestration and strategic planning.
    
    - **Status**: 🔒 Commercial (Coming Soon)
    - **What**: Autonomous AI
    - **Use Case**: Large-scale AI operations
    - **Example**: AI-powered company, research lab
    - **Complexity**: Enterprise
    - **Cost**: 💼 Commercial
    
    **Key Features:**
    - Advanced multi-agent orchestration
    - Strategic planning and execution
    
    **Tentative Features:**
    - Automatic discovery of agents based on task or goal, Ephemeral Agents making decisions and handling tasks, Integration with agent marketplace for choosing agents for tasks, Multiple LLM and Fine Tuned SLMs, Context Management with VectorDBs and Advanced Memory, Agentic BDD Spec Runner within orchestra and AgentLines, Integration with Multiple third party DevOps, MLOps Cloud providers

</div>

<!-- =================================================================== -->
<!-- KEY CAPABILITIES                                                    -->
<!-- =================================================================== -->
<div class="page-section">
  <h2><span class="gradient-text">🔧 Key Capabilities</span></h2>
  <div class="feature-grid" style="grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); text-align: center;">
    <div class="feature-card">✅ BDD Testing</div>
    <div class="feature-card">✅ Performance Optimization</div>
    <div class="feature-card">✅ Multi-Agent Orchestration</div>
    <div class="feature-card">✅ Production Operations</div>
    <div class="feature-card">✅ Memory Systems</div>
    <div class="feature-card">✅ RAG Integration</div>
    <div class="feature-card">✅ Model Management</div>
    <div class="feature-card">✅ Local & Cloud Inference</div>
  </div>
</div>

<!-- =================================================================== -->
<!-- FINAL CTA                                                           -->
<!-- =================================================================== -->
<div class="cta-section">
  <h2 class="gradient-text">🚀 Ready to Build the Future of AI?</h2>
  <p style="font-size: 1.2rem; margin-bottom: 1rem;">
    Join the SuperOptiX movement to create intelligent, optimized, and reliable AI agents.
  </p>
  <p style="font-size: 1rem; margin-bottom: 2rem; color: var(--text-secondary);">
    🆓 <strong>Start FREE today</strong> with Oracle & Genie tiers - no credit card required!
  </p>
  <div class="hero-links">
    <a href="quick-start" class="md-button md-button--primary">🚀 Start Free</a>
    <a href="tutorials/genies-agent" class="md-button">🤖 Create First Agent</a>
    <a href="guides/tiers" class="md-button">🎭 View Tiers</a>
  </div>
</div>

<p class="final-word"><em>👑 SuperOptiX: The King of Agent Frameworks - Where optimization meets intelligence.</em></p>
