---
layout: default
title: Shuban Blog
---


<html>

<style>
body {
      background-color: #171515;
      color: #ffffff;
  }

h2::before {  
  transform: scaleX(0);
  transform-origin: bottom right;
}

h2:hover::before {
  transform: scaleX(1);
  transform-origin: bottom left;
}

h2::before {
  content: " ";
  display: block;
  position: absolute;
  top: 0; right: 0; bottom: 0; left: 0;
  inset: 0 0 0 0;
  background: rgb(0, 0, 0);
  z-index: -1;
  transition: transform .3s ease;
}

h2 {
  position: relative;
  color: #39FF14;
  font-size: 1.5rem;
  font-family: Monospace;
}

p {
  font-family: Monospace;
}

html {
  block-size: 100%;
  inline-size: 100%;
}

body {
  min-block-size: 100%;
  min-inline-size: 100%;
  margin: 0;
  box-sizing: border-box;
  display: grid;
  place-content: center;
  font-family: system-ui, sans-serif;
}

.block-container {
    padding-top: 1rem;
    padding-bottom: 0rem;
    padding-left: 5rem;
    padding-right: 0rem;
}

/* @media (orientation: landscape) {
  body {
    grid-auto-flow: column;
  }
} */
</style>


<body>

<h2>About Me</h2>

<p>Hi, I am Shuban Pal. Some of my interests include cybersecurity, computer science, and math. I am fluent in Python, Go, and C. Some of my hobbies are playing video games, coding, and robotics. Here is a cool village I built in minecraft<br></p>
<img src="https://raw.githubusercontent.com/shuban-789/Markdown-images/main/minecraft.png" width="450">


<h2>Check out my Github!</h2>

<p>One of my coolest projects: <br>

Orion (RSH) Server <br></p>
<a href="https://github.com/shuban-789/Orion" target="_blank"><img src="https://github-readme-stats.vercel.app/api/pin/?username=shuban-789&repo=Orion&theme=chartreuse-dark" width="450"></a>
<br>
<h1>  My Skillbase:</h1>

<h2>Programming Languages:</h2>
<img src="https://skillicons.dev/icons?i=py,c,go" width="240">
<h2>Tools:</h2>
<img src="https://skillicons.dev/icons?i=vscode,linux,bash,aws,blender,docker" width="540">
<h2>Backend Software:</h2>
<img src="https://skillicons.dev/icons?i=mongodb,postgres,nginx" width="240">
<br>
<h2>  Currently trying to learn:</h2>

<img src="https://skillicons.dev/icons?i=gitlab,pytorch,tensorflow,firebase,unity" width="450">
