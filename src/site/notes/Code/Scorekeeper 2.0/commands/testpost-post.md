---
{"dg-publish":true,"permalink":"/code/scorekeeper-2-0/commands/testpost-post/","dgPassFrontmatter":true}
---


#### *testpost|post*
#### **command usage:**
`%register [lb name]` 
→ `[lb name]` - (optional) short 8- character, simple name
*examples* 

#### **data To store:**


#### **processes:**

***variables:***

***controlled data:***


***other data values:***


```js
const fs = require('fs');
const chalk = require('chalk'); // Import the chalk library

let path = "/Volumes/[C] Windows 11.hidden/Users/home/Desktop/boo/resources/test-scripts/scores.json";

// Load the JSON file
let rawData = fs.readFileSync(path);
let scores = JSON.parse(rawData);


// Find the players with the highest score
let maxScore = -Infinity;
let winners = [];
for (let name in scores) {
  if (scores[name].total > maxScore) {
    maxScore = scores[name].total;
    winners = [name];
  } else if (scores[name].total === maxScore) {
    winners.push(name);
  }
}

if (winners.length === 1) {
  console.log(`The winner is: ${chalk.bold(winners[0])} with a score of ${chalk.green(maxScore)}`);
} else {
  console.log(`${chalk.bold('There is a tie between:')} ${winners.map(name => chalk.bold(name)).join(', ')} with a score of ${chalk.green(maxScore)}`);
}

// Create a code block
console.log(`\`\`\`markdown
${chalk.bold('Player Name')}  |  ${chalk.bold('Red')}  |  ${chalk.bold('Blue')}  |  ${chalk.bold('Total')}
------------------  |  -----  |  -----  |  -----`);

// Loop through the scores and print them in the code block
for (let name in scores) {
  console.log(`${chalk.bold(name)}  |  ${chalk.red(scores[name].red)}  |  ${chalk.blue(scores[name].blue)}  |  ${chalk.green(scores[name].total)}`);
}
console.log('```');

```
will result in : 
The winner is: **pookie** with a score of **46**
or if there is a tie..

**There is a tie between:** **smirly**, **mamba** with a score of **46**

markdown
**Player Name**  |  **Red**  |  **Blue**  |  **Total**
------------------  |  -----  |  -----  |  -----
**smirly**  |  **20**  |  **26**  |  **46**
**pookie**  |  **14**  |  **9**  |  **23**
**mamba**  |  **22**  |  **20**  |  **42**



```js
const fs = require('fs'); // We will use the fs module to read the JSON file
const chalk = require('chalk'); // We will use the chalk library to style the output text

let path = "/Volumes/[C] Windows 11.hidden/Users/home/Desktop/boo/resources/test-scripts/scores.json";

// Load the JSON file
let rawData = fs.readFileSync(path);
let scores = JSON.parse(rawData);


// Find the players with the highest score
let maxScore = -Infinity;
let winners = [];
for (let name in scores) {
  if (scores[name].total > maxScore) {
    maxScore = scores[name].total;
    winners = [name];
  } else if (scores[name].total === maxScore) {
    winners.push(name);
  }
}

// Print the names and scores of the winners in fancy ANSI and codeblock markdown
console.log(`${chalk.yellow.bold.underline('\nWinners:')}`);
winners.forEach(winner => {
  console.log(`\`\`\`md
${chalk.cyan.bold(winner)}: ${chalk.red(scores[winner].red)} + ${chalk.blue(scores[winner].blue)} = ${chalk.magenta.bold(scores[winner].total)}
\`\`\``);
});

```

#### **triggers actions:**

#### **output:**