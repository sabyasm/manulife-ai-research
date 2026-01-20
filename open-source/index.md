---
title: Open Source
permalink: /open-source/
---

# Open Source

We contribute to the broader machine learning community through open source projects.

<div class="card-grid">
{% for project in site.data.open_source %}
  <div class="card oss-card">
    <h3><a href="{{ project.repo_url }}" target="_blank" rel="noopener">{{ project.name }}</a></h3>
    <span class="oss-status {{ project.status }}">{{ project.status }}</span>
    <p>{{ project.description }}</p>
    <div class="oss-meta">
      <strong>Team:</strong> {{ project.team_owner }}<br>
      <strong>License:</strong> {{ project.license }}<br>
      <strong>Last Release:</strong> {{ project.last_release }}
    </div>
  </div>
{% endfor %}
</div>
