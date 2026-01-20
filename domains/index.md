---
title: Embedded Domains
permalink: /domains/
---

# Embedded Domains

AI research and applied research are embedded within business and technology functions. Each domain below represents a focus area with demonstrated evidence of research outputs and collaborations.

<div class="card-grid">
{% for domain in site.domains %}
  {% assign domain_library_count = site.library | where_exp: "item", "item.domains contains domain.slug" | size %}
  {% assign domain_collab_count = site.data.collaborations | where: "domain", domain.slug | size %}
  {% comment %} 
    Gating: only show domains with ≥2 library items OR ≥1 library item AND ≥1 collaboration 
  {% endcomment %}
  {% if domain_library_count >= 2 or domain_library_count >= 1 and domain_collab_count >= 1 %}
  <a href="{{ domain.url | relative_url }}" class="card card-link">
    <h3>{{ domain.title }}</h3>
    <p>{{ domain.blurb }}</p>
    <div class="oss-meta">
      {{ domain_library_count }} publication{% if domain_library_count != 1 %}s{% endif %}
      {% if domain_collab_count > 0 %} · {{ domain_collab_count }} collaboration{% if domain_collab_count != 1 %}s{% endif %}{% endif %}
    </div>
  </a>
  {% endif %}
{% endfor %}
</div>
