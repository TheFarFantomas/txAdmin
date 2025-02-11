# In-Game Menu

txAdmin v4.0.0 introduced an in-game menu equipped with common admin functionality, 
an online player browser, and a slightly trimmed down version of the web panel.

You can find a short preview video [here](https://www.youtube.com/watch?v=jWKg0VQK0sc)

## Accessing the Menu

You can access the menu in-game by using the command `/tx` or `/txadmin`, alternatively
you can also use a keybind by going to `Game Settings > Key Bindings > FiveM` and 
setting the `(txAdmin) Menu: Open Main Page` option.

### Permissions
Anybody who you would like to give permissions to open the menu in-game, must have a txAdmin
account with either their Discord or Cfx.re identifiers tied to it.

***If you do not have any of these identifiers attached, you will not be able to access the menu***

You can further control the menu options accessible to admins by changing their permissions
in the admin manager as shown below.

![img](https://i.imgur.com/LP7Ij8M.png)

## Convars
The txAdmin menu has a variety of different convars that can alter the default behavior of the menu.  
Convars configured in the settings page should not be set manually.

**txAdmin-menuEnabled** (settings page only)
- Description: Whether the menu is enabled or not. Changing it requires server restart.
- Default: `true`

**txAdmin-menuAlignRight** (settings page only)
- Description: Whether to align the menu to the right of the screen instead of the left.
- Default: `false`

**txAdmin-menuPageKey** (settings page only)
- Description: Will change the key used for changing pages in the menu. This value must be the exact browser key code for your preferred key. You can use [this](https://keycode.info/) website and the `event.code` section to find it.
- Default: `Tab`

**txAdmin-menuDebug**
- Description: Will toggle debug printing on the server and client.
- Default: `false`
- Usage: `+setr txAdmin-menuDebug true`

**txAdmin-menuPlayerIdDistance**
- Description: The distance in which Player IDs become visible, if toggled on.
- Default: 150
- Usage: `+setr txAdmin-menuPlayerIdDistance 100`

**txAdmin-menuDrunkDuration**
- Description: How many seconds the drunk effect (troll action) should last.
- Default: 30
- Usage: `+setr txAdmin-menuDrunkDuration 120`

**txAdmin-menuPtfxDisable**
- Description: Determine whether to not play particles effects whenever an admin's player mode is changed.
- Default: `false`
- Usage: `+set txAdmin-menuPtfxDisable true`

**txAdmin-menuAnnounceNotiPos**
- Description: Determines the location of the txAdmin announcement notification. This **must** use one of the following valid 
positions, `top-center`, `top-left`, `top-right`, `bottom-center`, `bottom-left`, `bottom-right`.
- Default: `top-center`
- Usage: `+set txAdmin-menuAnnounceNotiPos top-right`

**txAdmin-changePlateText**

- Description: If the boost is used, it will automatically change the registration number of car to Tx Boost.
- Default: `true`

## Commands
**tx | txadmin**
- Description: Will toggle the in-game menu. This command has an optional argument of a player id that will quickly open up the target player's info modal.
- Usage: `/tx (playerID)`, `/txadmin (playerID)`
- Required Perm: `Must be an admin registered in the Admin Manager`

**txAdmin-debug**
- Description: Will toggle on debug mode without requiring a restart. (Can be used from console)
- Usage: `/txAdmin-debug [0 | 1]`
- Required Perm: `control.server`

**txAdmin-reauth**
- Description: Will retrigger the reauthentication process.
- Usage: `/txAdmin-reauth`
- Required Perm: `none`

## Troubleshooting menu access

- If you type `/tx` and nothing happens, your menu is probably disabled.  
- If you see a red message like [this](https://i.imgur.com/G83uTNC.png) and you are registered on txAdmin, you can type `/txAdmin-reauth` in the chat to retry the authentication.  
- If you can't authenticate and the reason id `Invalid Request: source`, this means the source IP of the HTTP request being made by fxserver to txAdmin is not a "localhost" one, which might occur if your host has multiple IPs. To disable this protection, edit your `config.json` file and add `webServer.disableNuiSourceCheck` with value `true` then restart txAdmin.

## Development
You can find development instructions regarding the menu [here.](https://github.com/tabarra/txAdmin/blob/master/docs/development.md#menu-development)

## FAQ
- **Q**: Why don't the 'Heal' options revive a player when using ESX/QBCore/etc?
- **A**: Many frameworks independently handle a "dead" state for a player, meaning
  the menu is unable to reset this state in an resource agnostic form directly. To establish compatibility 
  with any framework, txAdmin will emit an [txAdmin:events:healedPlayer](https://github.com/tabarra/txAdmin/blob/master/docs/events.md#txadmineventshealedplayer-v48) 
  for developers to handle.