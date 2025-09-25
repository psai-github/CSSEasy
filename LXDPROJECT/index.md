---
layout: base
title: Homepage
search_exclude: true
description: LXD Project Homepage
hide: true
permalink: /LXDHome
---

<link rel="stylesheet" href="{{ '/assets/css/lxdproject.css' | relative_url }}">

<!-- Main Content -->
<div class="bubble">
  <h1>Your Guide to CSSE TRI 1 is here</h1>
  <p>Yes, we all have had problems understanding the class, but don’t worry — we have step-by-step video and photo guides on every setup tool and process done in class, before you make this very exact project.</p>
</div>

<div class="warning">
  ⚠️ This only starts after you have installed WSL, Ubuntu, and VSCode.
  <a href="{{site.baseurl}}/ToolsSetup">Click here to get the setup</a>
</div>

<div class="search-container">
  <input type="text" id="search" placeholder="Search activities by title, description, or tags...">
</div>

<div class="activities">
  <div class="activity" data-title="Learn HTML Basics" data-desc="Start with simple HTML structure." data-tags="html,web,beginner">
    <div class="step-bar">
      <span>Step</span> <span class="step-number"></span>
    </div>
    <div class="activity-title"><a href="{{site.baseurl}}/Step1LXD" target="_blank">Basic CMDS</a></div>
    <div class="activity-desc">Commands You will use everyday, MUST WATCH</div>
    <div class="tags-toggle">Show Tags ▾</div>
    <div class="tags"><span>html</span><span>basic</span><span>beginner</span><span>Step1</span><span>cd</span><span>ls</span></div>
  </div>

  <div class="activity" data-title="Style with CSS" data-desc="Make your website beautiful." data-tags="css,design,frontend">
    <div class="step-bar">
      <span>Step</span> <span class="step-number"></span>
    </div>
    <div class="activity-title"><a href="{{site.baseurl}}/Step2LXD" target="_blank">Setting Up Repo</a></div>
    <div class="activity-desc">Cloning and Setting up a Repo</div>
    <div class="tags-toggle">Show Tags ▾</div>
    <div class="tags"><span>Cloning</span><span>Venv</span><span>Setting Up</span><span>Repositry</span></div>
  </div>

  <div class="activity" data-title="JavaScript Basics" data-desc="Add interactivity to your site." data-tags="javascript,frontend,coding">
    <div class="step-bar">
      <span>Step</span> <span class="step-number"></span>
    </div>
    <div class="activity-title"><a href="{{site.baseurl}}/Step3LXD" target="_blank">Themes On Pages</a></div>
    <div class="activity-desc">Diffrent Website Themes on Pages</div>
    <div class="tags-toggle">Show Tags ▾</div>
    <div class="tags"><span>pages</span><span>themes</span><span>make</span></div>
  </div>
  
  <div class="activity" data-title="Jupyter Notebook Jokes" data-desc="Fun examples with Jupyter notebooks." data-tags="jupyter,notebook,fun">
    <div class="step-bar">
      <span>Step</span> <span class="step-number"></span>
    </div>
    <div class="activity-title"><a href="{{site.baseurl}}/Step4LXD" target="_blank">Jokes On Jupiter</a></div>
    <div class="activity-desc">Using Jupyter notebooks for playful examples.</div>
    <div class="tags-toggle">Show Tags ▾</div>
    <div class="tags"><span>jupyter</span><span>notebook</span><span>examples</span></div>
  </div>
</div>

<script>
  // Auto-number steps
  document.querySelectorAll(".step-number").forEach((el, idx) => {
    el.textContent = idx + 1;
  });

  // Search function (includes title, desc, tags)
  document.getElementById("search").addEventListener("input", function () {
    let query = this.value.toLowerCase();
    let activities = document.querySelectorAll(".activity");

    activities.forEach(activity => {
      let title = activity.dataset.title.toLowerCase();
      let desc = activity.dataset.desc.toLowerCase();
      let tags = activity.dataset.tags.toLowerCase();

      if (title.includes(query) || desc.includes(query) || tags.includes(query)) {
        activity.style.display = "";
      } else {
        activity.style.display = "none";
      }
    });
  });

  // Toggle tags visibility
  document.querySelectorAll(".tags-toggle").forEach(toggle => {
    toggle.addEventListener("click", function () {
      let tags = this.nextElementSibling;
      if (tags.style.display === "block") {
        tags.style.display = "none";
        this.textContent = "Show Tags ▾";
      } else {
        tags.style.display = "block";
        this.textContent = "Hide Tags ▴";
      }
    });
  });
</script>

<!-- Themed Buttons at the Bottom -->
<div class="bottom-buttons" style="display: flex; justify-content: center; gap: 1.5rem; margin-top: 2.5rem; margin-bottom: 2rem;">
  <a href="{{site.baseurl}}/tools/VarClass" class="themed-btn" style="background: #4f8cff; color: #fff; padding: 0.8em 2em; border-radius: 8px; font-size: 1.1em; text-decoration: none; box-shadow: 0 2px 8px rgba(79,140,255,0.12); transition: background 0.2s; font-weight: 600;">VarClasses</a>
  <a href="{{site.baseurl}}/tools/VarClass" class="themed-btn" style="background: #2ecc71; color: #fff; padding: 0.8em 2em; border-radius: 8px; font-size: 1.1em; text-decoration: none; box-shadow: 0 2px 8px rgba(46,204,113,0.12); transition: background 0.2s; font-weight: 600;">Iterations</a>
</div>
