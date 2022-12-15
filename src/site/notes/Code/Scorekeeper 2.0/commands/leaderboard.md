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

;;ad-note

```js
const _ = require("lodash");
const jp = require("jsonpath");
const fs = require("fs-extra");
const {
    repeat
} = require("lodash");
//var servID = 952122158321139733;
//const skPath = `./data/scorekeeping/${serverVars("servID")}/scorekeeping.json`;
const skPath =
    "/Volumes/[C] Windows 11.hidden/Users/home/Desktop/fizzy/data/scorekeeping/952122158321139733/scorekeeping.json";
const jFile = fs.readJsonSync(skPath);

//let period = tempVars("period");
let period = "day";

/////////////////////////////**
// some functions
//////////////////////////////

//general utility func
function clog(arg) {
    console.log(arg);
}

//chunk up object
const chunk = (arr, size) =>
    arr.reduce(
        (acc, e, i) => (
            i % size ? acc[acc.length - 1].push(e) : acc.push([e]), acc
        ),
        []
    );
//sort by specific key    
const sortBy = (arr, k) =>
    arr.concat().sort((a, b) => (a[k] > b[k] ? 1 : a[k] < b[k] ? -1 : 0));

//truncate to whole number
const trunc = (n) => ~~n;

/////////////////////////////**
// simple declarations
//////////////////////////////
let obj;
let ind;
let lb;
let LB;
let arr;

/////////////////////////////**
// create object from array structure
//////////////////////////////
function mapObj() {
    let i = 0;
    let len = arr.length;
    let result = [];

    do {
        let [a, red, blue, kills, rebs, bonus, points] = [
            arr[i][0],
            arr[i][1][0],
            arr[i][1][1],
            arr[i][1][2],
            arr[i][2][0],
            arr[i][2][1],
            arr[i][2][2],
        ];
        let data = {
            player: a,
            rk: {
                rebs: rebs,
                bonus: bonus,
                points: points,
            },
            kc: {
                red: red,
                blue: blue,
                kills: kills,
            },
        };
        result.push({
            ...data,
        });
        i = i + 1;
    } while (i < len);
    return sortBy(result, "rk" [2]);
}

/////////////////////////////**
// print RK leaderboard
//////////////////////////////

function genLb() {
    let i = 0;
    let len = lb.length;
    let result = ["`PLAYER   RK  +K  ⇢ TOTAL`", "---------------------------"];

    do {
        let [a, rebs, bonus, points] = [
            lb[i].player,
            lb[i].rk.rebs,
            lb[i].rk.bonus,
            lb[i].rk.points,
        ];
        a = a + _.repeat(".", 8 - a.length);
        rebs = _.repeat(".", 4 - rebs.length) + rebs;
        bonus = bonus + _.repeat(".", 5 - bonus.length);
        points = _.repeat(".", 4 - points.length) + trunc(points);
        let lbRow = `\`${a}\` • \`${rebs}\` • \`${bonus}\` ⇢ \`${points}\``;
        result.push(lbRow);
        i = i + 1;
    } while (i < len);
    return _.join(result, "\n");
}

////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////
//
//                 Leaderboard switch
//
////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////

switch (period) {
    case "day": {
        obj = Object.entries(jFile.day.logs);
        obj = obj.flat(2);
        arr = chunk(obj, 3);

        lb = mapObj();
        LB = genLb();
    }
    break;
case "week": {
    obj = Object.entries(jFile.week.logs);
    obj = obj.flat(2);
    arr = chunk(obj, 3);

    lb = mapObj();
    LB = genLb();
}
break;
case "month": {
    obj = Object.entries(jFile.month.logs);
    obj = obj.flat(2);
    arr = chunk(obj, 3);

    lb = mapObj();
    LB = genLb();
}
break;
//default: action to execute on match; break;
}

console.log(LB);
//this.storeValue(LB, 1, "lb", cache);
//Actions.callNextAction(cache);
```

#### **triggers actions:**


#### **output:**