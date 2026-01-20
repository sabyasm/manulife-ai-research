---
title: Publications
permalink: /library/publications/
---

# Publications

Peer-reviewed papers and preprints from Manulife AI teams.

{% assign publications = site.library | where: "type", "publication" | sort: "year" | reverse %}
<ul class="library-list">
{% for item in publications %}
  <li class="library-item">
    <span class="library-year">{{ item.year }}</span>
    <a href="{{ item.external_url }}" target="_blank" rel="noopener">{{ item.title }}</a>
    {% if item.venue %}<span class="library-venue">{{ item.venue }}</span>{% endif %}
  </li>
{% endfor %}
</ul>

{% if publications.size == 0 %}
No publications yet.
{% endif %}
