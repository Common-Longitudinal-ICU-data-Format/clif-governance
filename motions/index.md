---
layout: default
title: Motions
---

<h1>🗳️ Motion Registry</h1>
<p>Complete record of all motions brought before the Steering Committee.</p>

<div class="dashboard-grid" style="margin-top: 2rem;">
  {% assign all_motions = site.data.motions.motions %}
  {% assign passed = all_motions | where: "status", "passed" %}
  {% assign failed = all_motions | where: "status", "failed" %}
  {% assign active = all_motions | where_exp: "m", "m.status != 'passed' and m.status != 'failed'" %}
  
  <div class="stat-card">
    <h3>Passed</h3>
    <div class="value" style="color: var(--success);">{{ passed | size }}</div>
  </div>
  
  <div class="stat-card">
    <h3>Failed</h3>
    <div class="value" style="color: var(--danger);">{{ failed | size }}</div>
  </div>
  
  <div class="stat-card">
    <h3>Active</h3>
    <div class="value" style="color: var(--warning);">{{ active | size }}</div>
  </div>
</div>

{% if active.size > 0 %}
<div class="card">
  <h2>🔄 Active Motions</h2>
  {% for motion in active %}
  <div class="motion-card">
    <div class="motion-header">
      <span class="motion-id">#{{ motion.id }}</span>
      <span class="motion-type">{{ motion.type | replace: "_", " " | capitalize }}</span>
      <span class="motion-status status-{{ motion.status }}">{{ motion.status | capitalize }}</span>
    </div>
    <h3>{{ motion.title }}</h3>
    <p class="motion-meta">
      Proposed by <strong>{{ motion.proposed_by }}</strong>
      {% if motion.seconded_by %} | Seconded by <strong>{{ motion.seconded_by }}</strong>{% endif %}
      | {{ motion.proposed_date }}
    </p>
    {% if motion.description %}
    <p class="motion-description">{{ motion.description }}</p>
    {% endif %}
  </div>
  {% endfor %}
</div>
{% endif %}

<div class="card">
  <h2>📜 All Motions</h2>
  {% if all_motions.size > 0 %}
  <table style="width: 100%; border-collapse: collapse;">
    <thead>
      <tr style="text-align: left; border-bottom: 2px solid var(--gray-200);">
        <th style="padding: 0.75rem;">ID</th>
        <th style="padding: 0.75rem;">Title</th>
        <th style="padding: 0.75rem;">Type</th>
        <th style="padding: 0.75rem;">Status</th>
        <th style="padding: 0.75rem;">Date</th>
      </tr>
    </thead>
    <tbody>
      {% for motion in all_motions %}
      <tr style="border-bottom: 1px solid var(--gray-100);">
        <td style="padding: 0.75rem; font-family: monospace;">#{{ motion.id }}</td>
        <td style="padding: 0.75rem;">{{ motion.title }}</td>
        <td style="padding: 0.75rem;">{{ motion.type | replace: "_", " " | capitalize }}</td>
        <td style="padding: 0.75rem;">
          <span class="motion-status status-{{ motion.status }}">{{ motion.status | capitalize }}</span>
        </td>
        <td style="padding: 0.75rem;">{{ motion.proposed_date }}</td>
      </tr>
      {% endfor %}
    </tbody>
  </table>
  {% else %}
  <p>No motions recorded yet. Motions will appear here as they are proposed in meetings.</p>
  {% endif %}
</div>

<div class="card">
  <h2>📊 Motion Types & Thresholds</h2>
  <table style="width: 100%; border-collapse: collapse;">
    <thead>
      <tr style="text-align: left; border-bottom: 2px solid var(--gray-200);">
        <th style="padding: 0.75rem;">Type</th>
        <th style="padding: 0.75rem;">Threshold</th>
        <th style="padding: 0.75rem;">Description</th>
      </tr>
    </thead>
    <tbody>
      <tr style="border-bottom: 1px solid var(--gray-100);">
        <td style="padding: 0.75rem;">Standard</td>
        <td style="padding: 0.75rem;">Simple Majority (>50%)</td>
        <td style="padding: 0.75rem;">General decisions, policy updates</td>
      </tr>
      <tr style="border-bottom: 1px solid var(--gray-100);">
        <td style="padding: 0.75rem;">mCIDE Update</td>
        <td style="padding: 0.75rem;">Simple Majority (>50%)</td>
        <td style="padding: 0.75rem;">Adding/modifying controlled vocabularies</td>
      </tr>
      <tr style="border-bottom: 1px solid var(--gray-100);">
        <td style="padding: 0.75rem;">Schema Change</td>
        <td style="padding: 0.75rem;">Two-Thirds (≥67%)</td>
        <td style="padding: 0.75rem;">Breaking changes to existing tables</td>
      </tr>
      <tr>
        <td style="padding: 0.75rem;">New Table</td>
        <td style="padding: 0.75rem;">Two-Thirds (≥67%)</td>
        <td style="padding: 0.75rem;">Adding new tables to CLIF schema</td>
      </tr>
    </tbody>
  </table>
</div>
