---
layout: page
title: Projects
permalink: /projects/
description: A showcase of my research projects and technical work in Natural Language Processing
nav: true
nav_order: 2
horizontal: false
---

<style>
.projects-hero {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 60px 0;
  margin: -40px -15px 40px -15px;
  text-align: center;
  border-radius: 0 0 20px 20px;
}

.projects-hero h1 {
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 1rem;
}

.projects-hero p {
  font-size: 1.2rem;
  opacity: 0.9;
  max-width: 600px;
  margin: 0 auto;
}

.project-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 30px;
  margin-top: 40px;
}

.project-card {
  background: white;
  border-radius: 16px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.project-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 20px 64px rgba(0, 0, 0, 0.15);
}

.project-image {
  height: 200px;
  background: linear-gradient(45deg, #f093fb 0%, #f5576c 100%);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 3rem;
  position: relative;
  overflow: hidden;
}

.project-image.nlp { background: linear-gradient(45deg, #667eea 0%, #764ba2 100%); }
.project-image.ml { background: linear-gradient(45deg, #f093fb 0%, #f5576c 100%); }
.project-image.ai { background: linear-gradient(45deg, #4facfe 0%, #00f2fe 100%); }
.project-image.data { background: linear-gradient(45deg, #43e97b 0%, #38f9d7 100%); }
.project-image.web { background: linear-gradient(45deg, #fa709a 0%, #fee140 100%); }

.project-content {
  padding: 24px;
}

.project-title {
  font-size: 1.4rem;
  font-weight: 600;
  color: #2d3748;
  margin-bottom: 12px;
  line-height: 1.3;
}

.project-description {
  color: #4a5568;
  line-height: 1.6;
  margin-bottom: 16px;
  font-size: 0.95rem;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
  margin-bottom: 16px;
}

.tech-tag {
  background: #e2e8f0;
  color: #4a5568;
  padding: 4px 10px;
  border-radius: 12px;
  font-size: 0.8rem;
  font-weight: 500;
}

.project-links {
  display: flex;
  gap: 12px;
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 8px 16px;
  border-radius: 8px;
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 500;
  transition: all 0.2s;
}

.project-link.primary {
  background: #667eea;
  color: white;
}

.project-link.primary:hover {
  background: #5a6fd8;
  color: white;
}

.project-link.secondary {
  background: #f7fafc;
  color: #4a5568;
  border: 1px solid #e2e8f0;
}

.project-link.secondary:hover {
  background: #edf2f7;
  color: #2d3748;
}

@media (max-width: 768px) {
  .projects-hero {
    padding: 40px 0;
    margin: -20px -15px 30px -15px;
  }
  
  .projects-hero h1 {
    font-size: 2rem;
  }
  
  .project-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }
}

/* Dark theme support */
@media (prefers-color-scheme: dark) {
  .project-card {
    background: #2d3748;
    border-color: #4a5568;
  }
  
  .project-title {
    color: #f7fafc;
  }
  
  .project-description {
    color: #e2e8f0;
  }
  
  .tech-tag {
    background: #4a5568;
    color: #e2e8f0;
  }
  
  .project-link.secondary {
    background: #4a5568;
    color: #e2e8f0;
    border-color: #718096;
  }
}
</style>

<div class="projects-hero">
  <h1>Research Projects</h1>
  <p>Exploring the frontiers of Natural Language Processing and Machine Learning through innovative research and practical applications</p>
</div>

<div class="project-grid">
  {%- assign sorted_projects = site.projects | sort: "importance" -%}
  {%- for project in sorted_projects -%}
  <div class="project-card">
    <div class="project-image nlp">
      <i class="fas fa-brain"></i>
    </div>
    <div class="project-content">
      <h3 class="project-title">{{ project.title }}</h3>
      <p class="project-description">{{ project.description }}</p>
      
      <div class="project-tech">
        <span class="tech-tag">NLP</span>
        <span class="tech-tag">Python</span>
        <span class="tech-tag">Machine Learning</span>
      </div>
      
      <div class="project-links">
        <a href="{{ project.url | relative_url }}" class="project-link primary">
          <i class="fas fa-eye"></i>
          View Details
        </a>
        {% if project.github %}
        <a href="{{ project.github }}" class="project-link secondary" target="_blank">
          <i class="fab fa-github"></i>
          Code
        </a>
        {% endif %}
      </div>
    </div>
  </div>
  {%- endfor -%}
</div>
