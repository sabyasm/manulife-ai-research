---
title: Reports
permalink: /library/reports/
---

# Reports

Technical reports and whitepapers from Manulife AI teams.

{% assign reports = site.library | where: "type", "report" | sort: "year" | reverse %}
<ul class="library-list">
{% for item in reports %}
  <li class="library-item">
    <span class="library-year">{{ item.year }}</span>
    <a href="{{ item.external_url }}" target="_blank" rel="noopener">{{ item.title }}</a>
    {% if item.venue %}<span class="library-venue">{{ item.venue }}</span>{% endif %}
  </li>
{% endfor %}
</ul>

{% if reports.size == 0 %}
No reports yet.
{% endif %}
