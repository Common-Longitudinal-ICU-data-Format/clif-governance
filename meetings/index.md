---
layout: default
title: Meetings
---

<h1>📅 Meeting Archive</h1>
<p>Complete record of CLIF Steering Committee meetings.</p>

<div class="card" style="margin-top: 2rem;">
  <h2>All Meetings</h2>
  {% assign sorted_meetings = site.meetings | sort: 'date' | reverse %}
  <ul class="meeting-list">
    {% for meeting in sorted_meetings %}
    <li>
      <div>
        <a href="{{ meeting.url | relative_url }}">{{ meeting.title }}</a>
        {% if meeting.motions %}
        <span style="color: var(--gray-500); font-size: 0.875rem; margin-left: 0.5rem;">
          ({{ meeting.motions | size }} motion{% if meeting.motions.size != 1 %}s{% endif %})
        </span>
        {% endif %}
      </div>
      <span class="date">{{ meeting.date | date: "%B %d, %Y" }}</span>
    </li>
    {% else %}
    <li>
      <p>No meetings recorded yet.</p>
      <p style="margin-top: 0.5rem;">
        <a href="https://github.com/Common-Longitudinal-ICU-data-Format/clif-governance/new/main/_meetings">
          ➕ Add the first meeting
        </a>
      </p>
    </li>
    {% endfor %}
  </ul>
</div>

<div class="card">
  <h2>📝 Adding a New Meeting</h2>
  <p>Create a new file: <code>_meetings/YYYY-MM-DD.md</code></p>
  <pre style="background: var(--gray-100); padding: 1rem; border-radius: 8px; overflow-x: auto; margin-top: 1rem;">
---
title: "Steering Committee - March 6, 2026"
date: 2026-03-06
attendance:
  present:
    - "Will Parker"
    - "Nick Ingraham"
    - "Catherine Gao"
  absent:
    - "Pat Lyons"
agenda:
  - title: "Review last week's action items"
    presenter: "Will Parker"
    duration: "5 min"
  - title: "CLIF 3.0 schema discussion"
    presenter: "Kaveri Chhikara"
    duration: "20 min"
motions: []
---

## Minutes

Meeting notes go here...
  </pre>
</div>
