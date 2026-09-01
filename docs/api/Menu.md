---
title: Menu
---

# Feather Menu

`feather-menu` is a standalone Lua-defined NUI menu system for RedM. It has no Feather Core dependency.

## Setup

1. Put `feather-menu` in your server's resources directory.
2. Add `ensure feather-menu` to `server.cfg`.
3. Ensure it before resources that create menus.

## API

```lua
exports['feather-menu']:initiate() -> FeatherMenu

FeatherMenu:RegisterMenu(menuId, config, callbacks?) -> Menu
FeatherMenu:Notify(options, callback?)

Menu:RegisterPage(pageId) -> Page
Menu:Open(options?)
Menu:Close(options?)
Menu:UnRegister()

Page:RegisterElement(type, data, callback?) -> Element
Page:UnRegister()

Element:update(data)
Element:UnRegister()
```

## Example

```lua
local FeatherMenu = exports['feather-menu']:initiate()

local menu = FeatherMenu:RegisterMenu('my_menu', {
  top = '50%',
  left = '50%',
  draggable = true,
  canclose = true
}, {})

local page = menu:RegisterPage('main')
page:RegisterElement('button', {
  label = 'Continue',
  slot = 'content'
}, function()
  menu:Close()
end)

menu:Open({ startupPage = page })
```

Available element types are `header`, `subheader`, `line`, `bottomline`, `button`, `input`, `textarea`, `slider`, `arrows`, `toggle`, `checkbox`, `dropdown`, `gridslider`, `imagebox`, `imageboxcontainer`, `html`, `pagearrows`, and `textdisplay`.

Opening a menu closes the active menu by default. Set `overrideMenu = false` in the open options when opening should fail instead.
