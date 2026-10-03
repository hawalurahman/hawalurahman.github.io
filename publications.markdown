---
layout: page
title: Publications
permalink: /publications/
---

{% assign sorted_pubs = site.data.publications | sort: "year" | reverse %}

{% for pub in sorted_pubs %}
<div style="margin-bottom: 20px;">
  <p style="margin: 0 0 5px 0;">
    <strong>{{ pub.title }}</strong>
  </p>
  <p style="margin: 0 0 5px 0; color: #555; font-size: 0.95rem;">
    {% comment %} Automatically style name wherever it appears in the author list {% endcomment %}
    {% assign styled_authors = pub.authors | replace: "Halim Wildan Awalurahman", '<span style="text-decoration: underline;">Halim Wildan Awalurahman</span>' %}
    
    {{ styled_authors }} ({{ pub.year }}). <em>{{ pub.venue }}</em>{% if pub.volume %}, vol. {{ pub.volume }}{% endif %}{% if pub.pages %}, pp. {{ pub.pages }}{% endif %}.
    {% if pub.url %}
      <a href="{{ pub.url }}" target="_blank">[Paper]</a>
    {% endif %}
  </p>
</div>
{% endfor %}