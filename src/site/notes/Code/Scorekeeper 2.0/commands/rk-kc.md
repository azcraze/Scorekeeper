---
{"dg-publish":true,"permalink":"/code/scorekeeper-2-0/commands/rk-kc/","dgPassFrontmatter":true}
---


#### *kc|rk <+|->*
#### **command usage:**
`%kc|rk [-] <lb name> <#> <#>`
→ `[-]` - if the first argument is a minus it will subtract the scores for the player sent
→ `<lb name>` - the player scores are being adjusted 
→ `<#>` - the 2 scores, separated by a space in order. Those orders are:
		rk - rebs, bonus
		kc - reds, blues
*examples* 
`%rk fishie 5 2`,  `%kc kedo 14 37`,  `%rk - hunty 5 7`, 
#### **data To store:**
command Parameters:
player, [scores]

serverVars:
dayStamp, 

userRecords.json:
dayStamp
#### **processes:**

***variables:***

***controlled data:***


***other data values:***


#### **scripts:**

```ad-note
title: javascript script for adding RK


~~~js
const _ = require("lodash");
const jp = require("jsonpath");
const fs = require("fs-extra");

//const skPath = "/Volumes/[C] Windows 11.hidden/Users/home/Desktop/fizzy/data/scorekeeping/952122158321139733/scorekeeping.json";
const skPath = `./data/scorekeeping/${serverVars("servID")}/scorekeeping.json`;
const jFile = fs.readJsonSync(skPath);

//input args
//let args = allArgs;
let args = tempVars("allArgs");
args = _.split(args, " ")
console.log(args);
let player = args.shift();
let pScores = [args[0], args[1]/2];
pScores = [+pScores[0], +pScores[1], (+pScores[0] + pScores[1])]


/////////////////////////////**
// some functions
//////////////////////////////

//general utility func
function clog(arg) {
    console.log(arg);
  }
  
function addScores(){
    let record = scores[ind][0];
    console.log(record);
    record[0] += pScores[0]
    record[1] += pScores[1]  
    record[2] += pScores[2]
    scores[ind][0] = record
    //console.log( "records is " + scores[ind][0] )
 }
 
 function pushNew(){
 players.push(player);
 scores.push([pScores, [0, 0, 0]]);
 }

  /////////////////////////////**
  // simple declarations
  //////////////////////////////
let obj;
let players;
let scores;
let ind;


////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////
//
//                 START DAY ENTRY SCRIPT
//
////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////

obj = Object.entries(jFile.day.logs);
obj = _.unzip(obj);
//console.log(obj);

players = obj[0];
scores = obj[1];
//console.log(scores);

ind = _.indexOf(players, player);
//console.log(ind);

(ind === -1) ? pushNew() : addScores()

obj = _.zipObject(players, scores)
jFile.day.logs = obj;


//console.log(jFile);

////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////
//
//                 START WEEK ENTRY SCRIPT
//
////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////


obj = Object.entries(jFile.week.logs);
obj = _.unzip(obj);
//console.log(obj);

players = obj[0];
scores = obj[1];
//console.log(scores);

ind = _.indexOf(players, player);
//console.log(ind);

(ind === -1) ? pushNew() : addScores()

obj = _.zipObject(players, scores)
jFile.week.logs = obj;


//console.log(jFile);


////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////
//
//                 START MONTH ENTRY SCRIPT
//
////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////

obj = Object.entries(jFile.month.logs);
obj = _.unzip(obj);
//console.log(obj);

players = obj[0];
scores = obj[1];
//console.log(scores);

ind = _.indexOf(players, player);
//console.log(ind);

(ind === -1) ? pushNew() : addScores()

obj = _.zipObject(players, scores)
jFile.month.logs = obj;

//console.log(jFile);

fs.writeFileSync(skPath, JSON.stringify(jFile, null, 2));
~~~

```


```ad-code
title: Javascript script for adding KC 

~~~js
const _ = require("lodash");
const jp = require("jsonpath");
const fs = require("fs-extra");

const skPath = `./data/scorekeeping/${serverVars("servID")}/scorekeeping.json`;
const jFile = fs.readJsonSync(skPath);

//input args
let args = tempVars("allArgs");
args = _.split(args, " ")
console.log(args);
let player = args.shift();
let pScores = [args[0], args[1]/2];
pScores = [+pScores[0], +pScores[1], (+pScores[0] + pScores[1])]

/////////////////////////////**
// some functions
//////////////////////////////

//general utility func
function clog(arg) {
    console.log(arg);
  }
  
function addScores(){
    let record = scores[ind][1];
   // console.log(record);
    record[0] += pScores[0]
    record[1] += pScores[1]  
    record[2] += pScores[2]
    scores[ind][1] = record
    //console.log( "records is " + scores[ind][0] )
 }
 
 function pushNew(){
 players.push(player);
 scores.push([[0, 0, 0], pScores]);
 }

  /////////////////////////////**
  // simple declarations
  //////////////////////////////
let obj;
let players;
let scores;
let ind;

////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////
//
//                 START DAY ENTRY SCRIPT
//
////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////

obj = Object.entries(jFile.day.logs);
obj = _.unzip(obj);
//console.log(obj);

players = obj[0];
scores = obj[1];
//console.log(scores);

ind = _.indexOf(players, player);
//console.log(ind);

(ind === -1) ? pushNew() : addScores()

obj = _.zipObject(players, scores)
jFile.day.logs = obj;


//console.log(jFile);


////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////
//
//                 START WEEK ENTRY SCRIPT
//
////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////


obj = Object.entries(jFile.week.logs);
obj = _.unzip(obj);
//console.log(obj);

players = obj[0];
scores = obj[1];
//console.log(scores);

ind = _.indexOf(players, player);
//console.log(ind);

(ind === -1) ? pushNew() : addScores()

obj = _.zipObject(players, scores)
jFile.week.logs = obj;

//console.log(jFile);


////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////
//
//                 START MONTH ENTRY SCRIPT
//
////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////

obj = Object.entries(jFile.month.logs);
obj = _.unzip(obj);
//console.log(obj);

players = obj[0];
scores = obj[1];
//console.log(scores);

ind = _.indexOf(players, player);
//console.log(ind);

(ind === -1) ? pushNew() : addScores()

obj = _.zipObject(players, scores)
jFile.month.logs = obj;


//console.log(jFile);

fs.writeFileSync(skPath, JSON.stringify(jFile, null, 2));
~~~

```
#### **triggers actions:**

#### **output:**