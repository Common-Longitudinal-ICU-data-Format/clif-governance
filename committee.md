---
layout: default
title: Committee
---

<h1>👥 Steering Committee</h1>
<p>The CLIF Consortium Steering Committee is responsible for governance decisions.</p>

<div class="card" style="margin-top: 2rem;">
  <h2>Quorum Requirements</h2>
  <p>
    <strong>Quorum:</strong> More than 50% of voting members must be present ({{ site.data.committee.voting_members | size | divided_by: 2 | plus: 1 }} of {{ site.data.committee.voting_members | size }} members)
  </p>
  <p style="margin-top: 0.5rem;">
    <strong>Attendance:</strong> Determined by Zoom login at weekly meeting
  </p>
</div>

<h2 style="margin-top: 2rem;">Voting Members</h2>
<div class="committee-grid">
  {% for member in site.data.committee.voting_members %}
  <div class="member-card">
    <h3>{{ member.name }}</h3>
    <div class="role">{{ member.role }}</div>
    <div class="institution">{{ member.institution }}</div>
    {% if member.email %}
    <div style="margin-top: 0.5rem; font-size: 0.875rem;">
      <a href="mailto:{{ member.email }}">{{ member.email }}</a>
    </div>
    {% endif %}
  </div>
  {% endfor %}
</div>

<div class="card" style="margin-top: 2rem;">
  <h2>Voting Thresholds</h2>
  <table style="width: 100%; border-collapse: collapse;">
    <thead>
      <tr style="text-align: left; border-bottom: 2px solid var(--gray-200);">
        <th style="padding: 0.75rem;">Motion Type</th>
        <th style="padding: 0.75rem;">Required Threshold</th>
      </tr>
    </thead>
    <tbody>
      {% for threshold in site.data.committee.voting_thresholds %}
      <tr style="border-bottom: 1px solid var(--gray-100);">
        <td style="padding: 0.75rem;">{{ threshold[0] | replace: "_", " " | capitalize }}</td>
        <td style="padding: 0.75rem;">
          {% if threshold[1] == 0.5 %}
            Simple Majority (>50%)
          {% elsif threshold[1] == 0.67 %}
            Two-Thirds (≥67%)
          {% else %}
            {{ threshold[1] | times: 100 }}%
          {% endif %}
        </td>
      </tr>
      {% endfor %}
    </tbody>
  </table>
</div>
