---
title: Library
permalink: /library/
---

# Library

Publications, talks, reports, and patents from AI teams across Manulife.

## Browse by Type

- [Publications](/library/publications/) — peer-reviewed papers and preprints
- [Talks](/library/talks/) — conference presentations and invited talks
- [Reports](/library/reports/) — technical reports and whitepapers
- [Patents](/library/patents/) — granted and pending patents

---

## All Items

{% assign all_items = site.library | sort: "year" | reverse %}
<ul class="library-list">
{% for item in all_items %}
  <li class="library-item">
    <span class="library-year">{{ item.year }}</span>
    <a href="{{ item.external_url }}" target="_blank" rel="noopener">{{ item.title }}</a>
    <span class="library-type">{{ item.type }}</span>
    {% if item.venue %}<span class="library-venue">{{ item.venue }}</span>{% endif %}
  </li>
{% endfor %}
</ul>
