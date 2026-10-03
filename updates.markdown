---
layout: page
title: Updates
permalink: /updates/
---

{% assign sorted_updates = site.data.updates | sort: "date" | reverse %}
{% assign grouped_updates = sorted_updates | group_by_exp: "item", "item.date | date: '%Y'" %}

{% for year_group in grouped_updates %}
  <h2>{{ year_group.name }}</h2>
  <ul>
    {% for update in year_group.items %}
      <li>
        <small style="color: #777;">{{ update.date | date: "%b %d" }}</small> — 
        {{ update.text | markdownify | remove: '<p>' | remove: '</p>' | strip }}
      </li>
    {% endfor %}
  </ul>
{% endfor %}