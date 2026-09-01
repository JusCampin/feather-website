---
title: Feather Roles
---

# Feather Roles

Feather Roles provides Character-scoped staff authority. A player’s role follows the active UUID Character rather than automatically applying to every Character on the account.

## Installation

```cfg
ensure oxmysql
ensure feather-core
ensure feather-character
ensure feather-roles
```

Configure the permanent role keys and levels before first start. Higher levels have greater authority. Do not rename role keys after assignments exist. Grant the first owner from the server console:

```text
RoleAssign <serverId> owner
```

## Server API

```lua
exports['feather-roles']:GetCapabilities()
exports['feather-roles']:GetHealth()
exports['feather-roles']:AwaitReady(timeoutMs?)
exports['feather-roles']:GetCatalog()
exports['feather-roles']:GetCharacterRole(characterUuid)
exports['feather-roles']:GetActorRole(source)
exports['feather-roles']:GetHighestAccountRole(accountUuid)
exports['feather-roles']:GetHistory(filters?)
exports['feather-roles']:AssignCharacterRole(request)
```

```lua
local assigned = exports['feather-roles']:AssignCharacterRole({
  actorSource = source,
  targetCharacterId = targetCharacterUuid,
  roleKey = 'moderator',
  reason = 'Staff promotion',
  reasonCode = 'admin.staff.promote',
  idempotencyKey = requestId,
  correlationId = requestId
})
```

Every call returns a result envelope. Assignment is hierarchy-protected, policy-authorized, locked, audited, and idempotent.
