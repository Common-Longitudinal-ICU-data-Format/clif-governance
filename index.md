---
layout: default
title: Dashboard
---

<div class="dashboard-header">
  <h1>🏥 CLIF Governance Dashboard</h1>
  <p>Parliamentary tracker for the CLIF Consortium Steering Committee</p>
</div>

<div class="dashboard-grid">
  <div class="stat-card">
    <h3>Steering Committee</h3>
    <div class="value">{{ site.data.committee.voting_members | size }}</div>
    <div class="subtext">voting members</div>
  </div>
  
  <div class="stat-card">
    <h3>Meetings Recorded</h3>
    <div class="value">{{ site.meetings | size }}</div>
    <div class="subtext">since tracking began</div>
  </div>
  
  <div class="stat-card">
    <h3>Motions Tracked</h3>
    <div class="value">{{ site.data.motions.motions | size }}</div>
    <div class="subtext">total motions</div>
  </div>
</div>

<div class="card">
  <h2>📅 Upcoming Meeting</h2>
  <p><strong>Weekly Steering Committee Call</strong></p>
  <p>Thursdays, 2:00 - 3:00 PM CT via Zoom</p>
  <p style="margin-top: 1rem;">
    <a href="{{ '/meetings/' | relative_url }}">View all meetings →</a>
  </p>
</div>

<div class="card">
  <h2>📋 Recent Meetings</h2>
  {% assign sorted_meetings = site.meetings | sort: 'date' | reverse %}
  <ul class="meeting-list">
    {% for meeting in sorted_meetings limit: 5 %}
    <li>
      <a href="{{ meeting.url | relative_url }}">{{ meeting.title }}</a>
      <span class="date">{{ meeting.date | date: "%b %d, %Y" }}</span>
    </li>
    {% else %}
    <li>No meetings recorded yet. <a href="https://github.com/Common-Longitudinal-ICU-data-Format/clif-governance">Add one via PR!</a></li>
    {% endfor %}
  </ul>
</div>

<div class="card">
  <h2>🗳️ Active Motions</h2>
  {% assign active_motions = site.data.motions.motions | where_exp: "m", "m.status != 'passed' and m.status != 'failed'" %}
  {% if active_motions.size > 0 %}
  <ul>
    {% for motion in active_motions %}
    <li>
      <strong>#{{ motion.id }}</strong>: {{ motion.title }}
      <span class="motion-status status-{{ motion.status }}">{{ motion.status }}</span>
    </li>
    {% endfor %}
  </ul>
  {% else %}
  <p>No active motions. All caught up! ✅</p>
  {% endif %}
</div>

<div class="card">
  <h2>📖 How It Works</h2>
  <ol>
    <li><strong>Before meeting:</strong> Create agenda via PR to <code>_meetings/YYYY-MM-DD.md</code></li>
    <li><strong>During meeting:</strong> Record attendance, motions, and votes</li>
    <li><strong>After meeting:</strong> Merge PR → Site rebuilds automatically</li>
    <li><strong>Passed motions:</strong> GitHub Action creates issues in CLIF repo</li>
  </ol>
  <p style="margin-top: 1rem;">
    <a href="https://github.com/Common-Longitudinal-ICU-data-Format/clif-governance" target="_blank">View on GitHub →</a>
  </p>
</div>
