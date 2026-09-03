---
title: Feather Admin
---

# Feather Admin

Feather Admin is the operator interface for moderation, reports, cases, player notes, staff roles, inventory administration, announcements, audit viewing, player management, and developer tools.

## Requirements and installation

This version of Admin still requires [Legacy: Menu v1](/api/resources/Menuv1) (`feather-menu`). Keep that dependency until Admin's menu integration is migrated. [Menu v2](/api/resources/Menuv2) is the official system for new Feather development; installing it does not replace Admin's existing v1 API calls.

```cfg
ensure oxmysql
ensure feather-core
ensure feather-toolkit
ensure feather-roles
ensure feather-inventory
ensure feather-menu
ensure feather-admin
```

Configure the menu command, reports, moderation limits, logging/webhook, hierarchy, and permission matrix in `configs/`. Grant the first Owner through Feather Roles before using Admin for routine role management.

## Public API

Admin is primarily an operator UI, not a general gameplay API. Its supported server export is:

```lua
exports['feather-admin']:checkConnectionBan(primaryIdentifier)
```

Connection-gate integrations should use the current Core gate and Admin moderation contracts rather than calling Admin network events. The `feather-admin:*` events are internal UI transport and are not a supported external mutation API.

## Production guidance

- Keep permissions least-privileged.
- Configure Discord webhook delivery only for Admin audit reporting; Core does not provide generic Discord helpers.
- Use Admin’s Inventory and Roles integrations rather than editing those databases.
- Run the supplied contract and persistence smoke tests in staging after upgrades.
