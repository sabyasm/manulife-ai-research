---
title: Partnership
permalink: /partnership/
---

# Partnership

We partner with leading academic institutions and industry organizations to advance AI research relevant to insurance and financial services.

{% assign grouped = site.data.partnership | group_by: "type" %}

{% for group in grouped %}
## {{ group.name | capitalize }} Partnerships

<ul class="collab-list">
{% for collab in group.items %}
  <li class="collab-item">
    <strong>{{ collab.partner }}</strong>
    <span class="collab-years">{{ collab.years }}</span>
    <p>{{ collab.area }}</p>
    {% if collab.links %}
    <ul class="collab-links">
      {% for link in collab.links %}
      <li><a href="{{ link.url }}" target="_blank" rel="noopener">{{ link.label }}</a></li>
      {% endfor %}
    </ul>
    {% endif %}
    {% assign domain = site.domains | where: "slug", collab.domain | first %}
    {% if domain %}
    <div class="oss-meta">Related domain: <a href="{{ domain.url | relative_url }}">{{ domain.title }}</a></div>
    {% endif %}
  </li>
{% endfor %}
</ul>
{% endfor %}