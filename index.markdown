---
layout: homepage
title: Home
---

<div class="hero-profile">
  <img src="{{ '/assets/img/IMG_0256.jpg' | relative_url }}" alt="Halim W. Awalurahman" class="profile_picture">
  <div class="hero-info">
    <h1>Halim W. Awalurahman</h1>
    <p class="subtitle">Doctoral Candidate in Computer Science<br>Faculty of Computer Science, Universitas Indonesia (Fasilkom UI)</p>
    <div class="hero-links">
      <a href="mailto:{{ site.email }}">Email</a> | 
      <a href="https://github.com/{{ site.github_username }}" target="_blank">GitHub</a> | 
      <a href="https://scholar.google.com/citations?user=kc6YyCoAAAAJ&hl=en" target="_blank">Google Scholar</a>
    </div>
  </div>
</div>

## About Me

Currently researching **Natural Language Processing (NLP)**, **Automatic Question Generation (AQG)**, and **Large Language Model (LLM) evaluation**.



## Recent Updates

<ul style="padding-left: 20px; margin-top: 5px;">
  {% assign sorted_updates = site.data.updates | sort: "date" | reverse %}
  {% for update in sorted_updates limit:3 %}
    <li style="margin-bottom: 6px;">
      <small style="color: #777;">{{ update.date | date: "%b %Y" }}</small> — 
      {{ update.text | markdownify | remove: '<p>' | remove: '</p>' | strip }}
    </li>
  {% endfor %}
</ul>
<p><a href="{{ '/updates' | relative_url }}">View all updates &rarr;</a></p>



## Latest Publications

{% assign sorted_pubs = site.data.publications | sort: "year" | reverse %}
{% for pub in sorted_pubs limit:3 %}
  {% assign styled_authors = pub.authors | replace: "Halim Wildan Awalurahman", '<span style="text-decoration: underline;">Halim Wildan Awalurahman</span>' %}
  - **{{ pub.title }}**  
    {{ styled_authors }} ({{ pub.year }}). <em>{{ pub.venue }}</em>{% if pub.url %} <a href="{{ pub.url }}" target="_blank">[Paper]</a>{% endif %}
{% endfor %}

<p><a href="{{ '/publications' | relative_url }}">View all publications &rarr;</a></p>