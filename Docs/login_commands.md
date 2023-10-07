---
title: Login commands
layout: home
nav_order: 5
---

# Login commands

Login commands are executed on the Path of Titans server when a player logs in. This is particularly useful for allocating the user a specific role when first connecting but can be used to run any command.

## Setting up a login command

### 1. Form Path of Titans command

You can execute any path of titans command available via RCON. 

OverRaptor will replace certain parameters with actual values:

`{aid}` - Players alderon id

`{name}` - Players in game username

An example **command** might look like -

```
promote {aid} supercoolrole
```

### 2. Expected Successful/Failed command response
Players have to be in a certain state once connected for many commands to successfully execute. OverRaptor will keep trying to run the command until it produces a response containing the specified output.

For example:
The `promote` command will return `Player with id 000-000-000 does not exist.` when the user first connnects, even though the user is logged in to the server. Finally once the player is in the appropriate state the command returns `Role added for 000-000-000`. So we can simply keep executing the command until `Role added` is found in the response or until the player disconnects.

An example **expect-success-contains** might look like -
```
Role added for
```

### 3. Add command

Add command with only expected success response:
```
add-login-command [pot-server-name] [command] [expect-success-contains]
```
Add command with only expected failure response:
```
add-login-command [pot-server-name] [command] [expect-failed-contains]
```
Atleast one must be set, this means both success and fail responses can be set:
```
add-login-command [pot-server-name] [command] [expect-failed-contains] [expect-success-contains]
```