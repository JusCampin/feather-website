---
title: Feather Notify
---

# Feather Notify

Feather Notify is the default RedM presentation provider for Core notifications.

## Installation and settings

```cfg
ensure feather-core
ensure feather-notify
```

`config.lua` limits message length and duration and supplies the default duration. Supported styles are `tooltip`, `advanced`, `location`, `right`, `left`, `top_banner`, `advanced_right`, `top`, `center`, `standard`, `bottom_right`, `mission_failed`, `dead_player`, and `warning`.

## Server usage

```lua
exports['feather-notify']:GetCapabilities() -> Result
exports['feather-core']:SendNotification(request) -> Result
```

```lua
exports['feather-core']:SendNotification({
  source = source,
  style = 'right',
  message = 'Saved successfully.',
  duration = 3000
})
```

## Client usage

```lua
exports['feather-notify']:ShowNotification(request) -> Result
```

Styles such as `top_banner`, `advanced`, `mission_failed`, and `warning` require a title. Advanced styles may also use `dictionary`, `icon`, `color`, `quality`, and audio fields.

Verification commands: `NotifyContractSmokeTest <source>`, `NotifyClientSmokeTest`, and `NotifyStyleSmokeTest`.
