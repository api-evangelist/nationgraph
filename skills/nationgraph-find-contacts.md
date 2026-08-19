---
name: Find verified government decision-maker contacts
description: >-
  Search NationGraph Contacts for verified government decision-makers by role and
  institution, returning emails and direct phone numbers for outreach.
api: openapi/_original/nationgraph-openapi-original.json
auth: HTTP Bearer (Authorization: Bearer <token>)
operations:
  - search_contacts_api_v3_contacts_search_post
  - get_contacts_api_v3_contacts_get
---

# Find verified government decision-maker contacts

Base URL `https://api.nationgraph.com`; send `Authorization: Bearer <token>`.

1. **Search contacts.** `POST /api/v3/contacts/search`
   (`search_contacts_api_v3_contacts_search_post`) with role / institution /
   territory criteria in the body.
2. **List / page contacts.** `GET /api/v3/contacts`
   (`get_contacts_api_v3_contacts_get`) with `limit`/`offset` and `sort` to page
   through matched decision-makers (verified emails + phone numbers).

Handle 422 validation errors by reading each `detail[].loc`/`msg`. Respect the
public sector's contactability and compliance constraints before outreach.
