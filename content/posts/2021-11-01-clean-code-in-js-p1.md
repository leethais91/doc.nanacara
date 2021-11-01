---
title: "Clean code in JS (P1)"
slug:
description: "Write meaningful names for variables and functions"
date: 2021-11-01 10:52:30
author: ThaiLe
tags:
    - CleanCode
    - JS
cover:
fullscreen: false
---
Write meaningful names for variables and functions. It can take some time to find a good name but it will save you and your team even more time in the future. Where you visit your code only a few months later and have a hard time understanding what you did before.

## Basic rules

Variables, functions, parameters -> `cameCase`

Constants -> `SCREAMING_CASE`

```javascript
# Constants
const API_KEY = '34c851e7f5e99eddb689e42da05a9828'
const TAU = 2 * Math.PI
```

## Semantic Data Types

### Numbers, Strings, Objects

In most cases, numbers, strings, and individual objects are named with the most appropriate **singular noun**.

```javascript
const email = 'dev@gmail.com'
const age = 20
const profile = {
    username: 'dev',
    email: 'dev@gmail.com',
    experience: '3+ years make bad code',
}
```

### Booleans

The name for booleans are usually in the form yes-no question.

```javascript
const isEmpty = true
const canSupportIE = false;
const hasToken = false;

function isOdd(num) {
    return Boolean(num % 2)
}
```

Don’t use negation in Boolean names. Don’t use names that require a prefix like `not` that inverts the variable’s truth value.

```javascript
// Don't do like this
const notSuccessful = false;
const notValid = false;

// Refactoring by invert the meaning and remove the prefix
const isSuccess = true; // or const isError = false;
const isValid = true;
```

### Array & Collections

Array and other collection (such as Map, Set) are name with `plural` noun in `camelCase`.

```javascript
const sheeps = ['Willy', 'Barry', 'Moe']
const employees = ['Join', 'Mary', 'Adam']
const remainingJobs = ['BUILD', 'DEPLOY', 'CLEAN']
```

Can use **singular form** of these nouns can be used as variable names during iteration.

```javascript
employees.forEach(employee => rewardingBonus(employee))
// or
for (const employee of employees)
    rewardingBonus(employee)
```

Can use **collections nouns** for better readability.

```javascript
const flockOfSheeps = ['Willy', 'Barry', 'Moe']
flockOfSheeps.forEach(sheep => {
    console.log(sheep)
})
```

**Note:** [what is collections nouns](https://www.gingersoftware.com/content/grammar-rules/nouns/collective-nouns/)

## Functions

Usually named as a combination of two parts: `transitive verb` + `direct object`

In other words: `verb` + `noun`

_Here example about naming functions_

```javascript
function getSum(a, b) { return a + b }

const suggestDaddy(users) {
    return users.fifter(user => user.gender === 'male' && (user.hasCar() || user.hasHouseForRent() || user.job === 'developer'))
}
// Get list candidates for daddy from friend list
const suggarDaddies = suggestDaddy(friendsOnFacebook)
// Inbox direction message for each daddy
suggarDaddies.forReach(daddy => sendDM(daddy))
```
