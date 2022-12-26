---
{"dg-publish":true,"dg-home":true,"date updated":"1669934706649","permalink":"/code/scorekeeper-2-0/scorekeeping-functional-outline/","tags":"gardenEntry","dgPassFrontmatter":true}
---


#### *Concepts*

* define required files
* variable assignment
* processes
* code functions
* data structure

## Definitions

**RK** - rebel kill(s)\
**KC** - kill(s) count\
**SK** - scorekeeper\
**SS** - screenshot\
**RK(d|w|m)** rebel kills for day | week | month\
**KC(d|w|m)** kills count for day | week | month\
**var** - variable\
**arg** - argument

## The Scores

We have 2 submission channels for members to submit screenshots to count towards their recorded scores.\
We then have *daily*, *weekly*, and *monthly* winners announced for each of the two categories.

### Point System

**Rebel kills**\
rebKills: 1,\
bonus: .5

**Kills count**\
reds: number,\
blues: number

### Process Flow (ideal)

1. member will register with the bot berfore having access to post, which will initiate their record/profile
2. user submits valid screen shot
3. sk(scorekeeper) tallies the kills on each screen shot for blues, and reds & tallies the rebel kills and number of bonus kills
4. sk submits using a command with bot:
		* short name
		* scores received
5. bot first determines if player has already been entered in for the day log
		* adds a new entry if they are not present
		* combine logged kills and new kills for sum if already present
6. bot logs the points for day set in global var which updates the score for current week, month, total accordingly
		* for rk bot takes raw bonus count and divides by 2
7. ***there are 3 paths(?) that should be possible with the data stored :***
		1. sk will be able to check logs and adjust accordingly
		2. sk will test and post the winners resulting from submissions at the end of each period
		3. members will be able to view their stats or another's at anytime

```ad-idea
bring up the idea of not counting bonuses for RK or not counting kills seperately for KC. ask smirly and members.
```

### Functionality & Interactions

* Server initialization
* User registration
* Assigning scores role
* Initializing database profile
* Tracking current date
* Scorekeeping commands to enter scores
* Allows for changes to records
* Calculating end of period scores
* sorting and finding top results
* Handling ties
* Posting test embeds
* Posting winner posts
* Managing automatic role assignment and removal
* Command to view player stats
* Commands for current period leaderboards

### Commands

`%setup scorekeeper` - initialize server variables and data stores\
`%register` - register to get access to submission channels and scorekeeping\
`%skset` - group command for various settings and data setting

* `%skset newuser` - will take parameters (tbd)
* `%skset date` - manually adjust date or check current setting
* `%skset admin` - admin commands?
* `%skset logs` - log settings and commands

`%sk <+|->` - sk command to add or subtract daily scores for a player\
`%testpost (d|w|m)` - preview winner result embeds and check for corrections needed\
`%post (d|w|m)` - post winners\
`%scores` - check personal or other player stats
`%leaderboard` - get current tallied scores

## Technical Development Process


This section covers each of the commands and the following information about each command:
- who its intended for
- the command usage (parameters, args, etc)
		- optional args
		- required
- the data it will fetch & store from the database
- the processes it takes on or with the data stored (author input also)
- data values
	- new variables or db values
	- updated or changed variables or db values
	- appended (added to list) variables or db values
	- deleted, removed or reset variables or db values
- data that is changed or updated as secondary
- secondary processes that are triggered
- the result/output

#### *Note the following syntax rules:*
**They tell you how to use read the technical parts of this document:**
> `(this|this|or|this)` - (not optional) used to list subcommands who's processes are identical. think of the`|` as an 'OR' 
> `<required arg>` - acts as a place holder for information required to be sent with the command
> `[optional arg]` - acts as a place holder for information is optional depending on the desired action.
> `([group] [args])` - indicates that in order to use any of the args in the `( )` the author must submit values for all of the args in that group
> `...` - used to indicate args or group args that the author can optionally send more than one of

### Command documentation

 [[Code/Scorekeeper 2.0/commands/setup scorekeeper\|setup scorekeeper]]
 [[Code/Scorekeeper 2.0/commands/register\|register]]
 [[Code/Scorekeeper 2.0/commands/skset\|skset]] (group command)
 [[Code/Scorekeeper 2.0/commands/rk-kc\|rk-kc]] +|-
 [[Code/Scorekeeper 2.0/commands/testpost-post\|testpost-post]]
 [[Code/Scorekeeper 2.0/commands/leaderboard\|leaderboard]]
 [[Code/Scorekeeper 2.0/commands/scores\|scores]]






```ad-summary
title: Bot project directory
Most files and folders are here. Some i may have left out as redundantcies or unnecessary or for brevity

So far json files planned for
```dirtree

- actions
- data/
	- scorekeeping/
		- SERVERID1/
			- ksScores.json
			- rkScores.json
			- logs.json*
			- skVars.json
		- ...SERVERID2/
			- ...
		- playerRecords/
			- player1-records.json
			- player2-records,json
			- ...
		- commands.json
		- events.json
		- globals.json
		- globalVars.json
		- players.json
		- prefixes.json
		- servers.json
		- serverVars.json
		- settings.json
		- storedVariables.json
		- users.json
	- templates/
		- kcScores.json
		- rkScores.json
		- skVars.json
		- player-records.json
		- ...
- events/
- extentions/
- node__modules/
	- .../
	- ...
- resources/
	- functions/
		- ...
	- tests/
		- ...
	- scripts/
	- addPlayerKc.js
	- addPlayerRk.js
	- kc.js
	- rk.js
	- kcLb.js
	- rkLb.js
	- kcRemove.js
	- rkRemove.js
	- post.js
	- getSettings.js
- bot.js
- package.json
- project.discordbot


```



```ad-snip
title: Requirements

```ad-codenote
title: NPM Modules

~~~js
const _ = require("lodash");
const fs = require("fs-extra");
const jp = require("jsonpath");
~~~
```
