# CLIF Governance

Parliamentary tracker for the CLIF Consortium Steering Committee.

**🌐 Live site:** [common-longitudinal-icu-data-format.github.io/clif-governance](https://common-longitudinal-icu-data-format.github.io/clif-governance)

## Features

- 📋 **Agenda Management** — Set weekly meeting agendas via PR
- ✅ **Quorum Tracking** — Automatic quorum calculation based on attendance
- 🗳️ **Motion Registry** — Track all motions with vote records
- 📜 **Historical Archive** — Full searchable meeting history
- 🔗 **GitHub Integration** — Passed motions auto-create issues in CLIF repo

## How It Works

### Before the Meeting

1. Create a new file: `_meetings/YYYY-MM-DD.md`
2. Add agenda items, set the date
3. Submit a PR

### During the Meeting

1. Record attendance (who's on Zoom)
2. Add any motions that come up
3. Record votes

### After the Meeting

1. Add meeting minutes
2. Merge the PR
3. Site rebuilds automatically
4. Passed motions create GitHub issues

## File Structure

```
clif-governance/
├── _data/
│   ├── committee.yml      # Steering committee roster
│   └── motions.yml        # Motion registry
├── _meetings/             # Meeting records (YYYY-MM-DD.md)
├── _layouts/              # Page templates
├── assets/css/            # Styling
├── committee.md           # Committee page
├── meetings/index.md      # Meetings archive
├── motions/index.md       # Motion registry
└── index.md               # Dashboard
```

## Adding a Meeting

Create `_meetings/2026-03-13.md`:

```yaml
---
title: "Steering Committee - March 13, 2026"
date: 2026-03-13
attendance:
  present:
    - "Will Parker"
    - "Nick Ingraham"
    - "Catherine Gao"
  absent:
    - "Pat Lyons"
agenda:
  - title: "Review action items"
    presenter: "Will Parker"
    duration: "5 min"
  - title: "CLIF 3.0 discussion"
    presenter: "Kaveri Chhikara"
    duration: "20 min"
motions: []
---

## Minutes

Meeting notes here...
```

## Recording a Motion

Add to the meeting file's `motions` array:

```yaml
motions:
  - id: "2026-002"
    title: "Add position_details column to position table"
    type: "schema_change"
    proposed_by: "Catherine Gao"
    seconded_by: "Nick Ingraham"
    description: "Add optional column for detailed positioning information"
    status: "passed"
    votes:
      yes: ["Will Parker", "Nick Ingraham", "Catherine Gao", "Kaveri Chhikara"]
      no: []
      abstain: ["Vaishvik Chaudhari"]
```

## Motion Types & Thresholds

| Type | Threshold | Use For |
|------|-----------|---------|
| `standard` | >50% | General decisions |
| `mcide_update` | >50% | Vocabulary changes |
| `schema_change` | ≥67% | Breaking table changes |
| `new_table` | ≥67% | Adding new tables |
| `policy` | >50% | Policy decisions |

## Local Development

```bash
# Install dependencies
bundle install

# Run locally
bundle exec jekyll serve

# View at http://localhost:4000/clif-governance/
```

## Contributing

1. Fork the repo
2. Create a branch (`git checkout -b meeting/2026-03-13`)
3. Add your meeting file
4. Submit a PR

---

Built with ❤️ for the CLIF Consortium
