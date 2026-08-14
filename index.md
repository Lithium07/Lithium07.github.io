---
layout: default
---
<div class="hero">
  <div class="avatar" role="img" aria-label="Jiahao Li"><span>JL</span></div>
  <div class="hero-body">
    <h1>Jiahao Li</h1>
    <p class="role">Principal Researcher</p>
    <p class="org">Microsoft Research Asia</p>
    <ul class="hero-links">
      <li><a href="mailto:jiahali@microsoft.com">Email</a></li>
      <li><a href="https://scholar.google.com/citations?user=AcOcw0AAAAAJ&hl=en" target="_blank" rel="noopener">Google Scholar</a></li>
      <li><a href="https://www.microsoft.com/en-us/research/people/jiahali/" target="_blank" rel="noopener">MSR Profile</a></li>
      <!-- 需要的话补上：GitHub / DBLP / X / LinkedIn / CV
      <li><a href="https://github.com/YOUR_ID" target="_blank" rel="noopener">GitHub</a></li>
      <li><a href="/assets/cv.pdf">CV</a></li>
      -->
    </ul>
  </div>
</div>

## About

I am a Principal Researcher in the Media Computing Group at Microsoft Research Asia. I received my B.S. in Computer Science and Technology from Harbin Institute of Technology in 2014, and my Ph.D. in Computer Application Technology from Peking University in 2019.

My early work focused on traditional video codecs, where several of my techniques were adopted into international standards including H.266/VVC and AOM AV1. I then turned to neural image and video codecs, aiming to push the frontier of compression research. My interests now extend further to visual generation, video understanding, agentic video systems, and long-horizon video memory and context.

I have contributed several technique transfers to Microsoft real-time communication product Teams.

## Research Interests

<ul class="chips">
  <li>Neural image & video compression</li>
  <li>Visual generation</li>
  <li>Video understanding</li>
  <li>Agentic video systems</li>
  <li>Long-horizon video memory & context</li>
</ul>

## Education

<ul class="timeline">
  <li>
    <div class="deg">Ph.D. in Computer Application Technology</div>
    <div class="where">Peking University</div>
    <div class="when">2019</div>
  </li>
  <li>
    <div class="deg">B.S. in Computer Science and Technology</div>
    <div class="where">Harbin Institute of Technology</div>
    <div class="when">2014</div>
  </li>
</ul>

<!-- 想加 Experience / Awards / Academic Service：复制上面 "## 标题" + <ul class="timeline"> 结构即可 -->

## Publications

<p class="pub-note">Here is my <a href="https://scholar.google.com/citations?user=AcOcw0AAAAAJ&hl=en" target="_blank" rel="noopener">Google Scholar</a>.</p>

{% capture publications %}{% include publications.md %}{% endcapture %}

<div class="pubs">
{{ publications | markdownify | replace: '<a href="http', '<a target="_blank" rel="noopener" href="http' }}
</div>

## Contact

<div class="callout">
  <p><strong>I am hiring research interns.</strong> If you are passionate about neural compression, visual generation, video understanding, or agentic visual systems, please send your CV to <a href="mailto:li.jiahao@microsoft.com">li.jiahao@microsoft.com</a>.</p>
</div>
