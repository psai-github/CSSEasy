---
layout: base
title: Step2 
search_exclude: true
description: Basic CMds
hide: true
permalink: /Step2LXD
---

<link rel="stylesheet" href="{{site.baseurl}}/assets/css/lxdproject.css">

<style>
.video-container {
  position: relative;
  width: 100%;
  max-width: 600px;
  margin: 0 auto 25px auto;
  padding-bottom: 56.25%; /* 16:9 ratio */
  height: 0;
  overflow: hidden;
  border-radius: 16px;
  box-shadow: 0 8px 25px rgba(255, 255, 255, 0.1);
}
.video-container iframe {
  position: absolute;
  top: 0; left: 0;
  width: 100%;
  height: 100%;
  border-radius: 16px;
}
</style>

<div class="bubble">
  <h1>Setting Up a Repo The Right Way - Step 2</h1>
</div>

<div class="video-container">
  <iframe src="https://www.youtube.com/embed/nroMSrVCrJM" loading="lazy" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

<div class="bubble">
  <p>
    Repo means Your Github Repositry and This is the best way to set it up. <code>./scripts/venv.sh</code> command installs Venv on your repo.<code>source venv/bin/activate</code> Opens the Repo in a Venv python envirment   
  </p>
</div>

<a href="{{ site.baseurl }}/LXDHome" class="back-link">⬅ Back to Homepage</a>
