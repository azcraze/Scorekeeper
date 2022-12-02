---
{"dg-publish":true,"permalink":"/code/scorekeeper-2-0/commands/setup-scorekeeper/","dgPassFrontmatter":true}
---


### *setup scorekeeper*
**command usage:**
`%setup scorekeeper <scores role id> ([rkd|rkw|rkm] [rk role])... ([kcd|kcw|kcm] [kc role])...` 
→ `[roles]` - setting roles for assigning to winners
*examples*   `%setup scorekeeper 876409193962274816 rkd 816814079213043714` 
**data to store:**
current date, year, month, week, day, doty, dotw, setup indicator
**processes:**
- check the `setup indicator` for a `true` value to determine whether certain processes will occur 
  if undefined: 
	- join month, day, and year values for the dayStamp *ex. 11292022*
	- create array (list) of all currently registered players with the scores role → store in `server variable` →  `registeredUsers` 
	- create the following JSON files (==keys to be decided later==)
		- scorekeeping.json
		- daylog.json
		- weeklog.json
		- monthlog.json
		- records.json
		- template-log.json
		- skvariables.json
	- 
  if true:
***variables:***

***stored data:***

***other data values:***

**triggers actions:**

**output:**


