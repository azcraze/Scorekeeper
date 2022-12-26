---
{"dg-publish":true,"permalink":"/code/scorekeeper-2-0/commands/leaderboard/","dgPassFrontmatter":true}
---


#### *leaderboard*
#### **command usage:**
`%lb <period> [rk | kc]` 
→ `<period>`- (required) choose which board to show. (*day | week | month|total)*

*examples* 
`%lb rk week`
`%lb day`
`%b kc month`

#### **data To store:**
period

#### **processes:**

***variables:***

***controlled data:***


***other data values:***

#### **scripts:**


```ad-code
Type: **code** 

~~~js
const fs = require('fs');
const pretty = require("prettyjson");
const c = require('ansi-colors');

const options = {
	keysColor: "rainbow",
	dashColor: "magenta",
	stringColor: "grey",
	defaultIndentation: 2,
	numberColor: "white",
	inlineArrays: true,
	multilineStringColor: "rainbow",
	emptyArrayMsg: "[]"
};

function prettify(data) {
	return pretty.render(data, options);
}

function out(toLog) {
	console.log(prettify(toLog));
}

const path = "resources/test-scripts/scores.json";
const dayStamp = "12172022";

// Load the JSON file
const rawData = fs.readFileSync(path);
const scores = JSON.parse(rawData);

// Convert the scores object to an array of key-value pairs and sort it by sum
const scoresArray = Object.entries(scores[dayStamp]);
scoresArray.sort((a, b) => b[1].total - a[1].total);

// Build the leaderboard table
const leaderboard = `${c.bgMagenta("PLAYER    RED  BLU   TOTAL")}\n${c.blue("--------------------------")}\n`;
for (const [name, score] of scoresArray) {
  leaderboard += `${c.blue(name.padEnd(9))} ${score.red.toString().padEnd(5)} ${score.blue.toString().padEnd(5)}${score.total}\n`;
}

out(leaderboard);

this.storeValue(leaderboard, 1, "out1", cache);
Actions.callNextAction(cache);

~~~

```

#### **triggers actions:**


#### **output:**