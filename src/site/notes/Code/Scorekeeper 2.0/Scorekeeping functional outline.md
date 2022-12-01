---
{"dg-publish":true,"dg-home":true,"permalink":"/code/scorekeeper-2-0/scorekeeping-functional-outline/","tags":"gardenEntry","dgPassFrontmatter":true}
---



#### *Concepts*
- define required files
- variable assignment 
- processes
- code functions
- data structure

## Definitions
**RK** - rebel kill(s)
**KC** - kill(s) count
**SK** - scorekeeper 
**SS** - screenshot
**RK(d|w|m)** rebel kills for day | week | month
**KC(d|w|m)** kills count for day | week | month
**var** - variable 
**arg** - argument

## The Scores

We have 2 submission channels for members to submit screenshots to count towards their recorded scores. 

We then have *daily*, *weekly*, and *monthly* winners announced for each of the two categories. 

### Point system
**Rebel kills**
rebKills: 1,
bonus: .5

**Kills count**
reds: number,
blues: number

### Process flow (ideal)
1. member will register with the bot berfore having access to post, which will initiate their record/profile
2. user submits valid screen shot
3. sk(scorekeeper) tallies the kills on each screen shot for blues, and reds & tallies the rebel kills and number of bonus kills
4. sk submits using a command with bot:
	- short name
	- scores received
5. bot first determines if player has already been entered in for the day log
	- adds a new entry if they are not present
	- combine logged kills and new kills for sum if already present
6. bot logs the points for day set in global var which updates the score for current week, month, total accordingly
	- for rk bot takes raw bonus count and divides by 2
7. ***there are 3 paths(?) that should be possible with the data stored :***
	1. sk will be able to check logs and adjust accordingly
	2. sk will test and post the winners resulting from submissions at the end of each period
	3. members will be able to view their stats or another's at anytime

```ad-idea
bring up the idea of not counting bonuses for RK or not counting kills seperately for KC. ask smirly and members.
```

### Functionality
`rir:FileCode`


````ad-summary
title: JSON Files

So far json files planned for
```dirtree
- /data
	- ..json
- settings.json
- /scorekeeping
	- logs.json
```
````

````ad-codenote
title: Requirements

```ad-snip
title: NPM Modules

~~~js
const _ = require("lodash");
const fs = require("fs-extra");
const jp = require("jsonpath");
~~~
```
````

