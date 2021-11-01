---
title: "Clean code in JS (P2)"
slug:
description: "Use modern javascript to clean code"
date: 2021-11-01 11:22:58
author: ThaiLe
tags:
    - CleanCode
    - JS
cover:
fullscreen: false
---
Modern javascript helps you to make your website and app faster, cleaner.

> This guide is not intended to teach you JavaScript or ES6 syntax. I just show some keywords and personal tips via examples for you to know when you can apply them.

#### Destructuring objects and arrays

> Destructuring is a convenient way of creating new variables by extracting some values from data stored in objects or arrays.

[More detail here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

_Example with `Object`_

```javascript
const person = {
  id: "001",
  firstName: "Join",
  lastName: "Wick",
  age: 35,
}
```

_Without destructuring_

```javascript
const userID = person.id;
const lastName = person.lastName;
const sex = person.sex || "M";
```

_Refactor with destructuring_

```javascript
const { userID: id, lastName, sex = "M" } = person;
```

_Example with `Function`_

```javascript
function getFullName(person) {
  const firstName = person.firstName;
  const lastName = person.lastName;
  return firstName + ' ' + lastName;
}
getFullName(person); // "Join Wick"
```

_Refactor with destructuring_

```javascript
function getFullName({ firstName, lastName }) {
  return firstName + ' ' + lastName;
}

getFullName(person); // "Join Wick"
```

_Example with React, RN : defined a React's component_

```javascript
const Avatar(props) {
  const image = props.image || 'default_avatar_url';
 
  ...
  const onPress = () => {
    props.navigation.navigate('UserSettingScreen')
  }
}
```

_Let refactor with destructuring_

```javascript
const Avatar({ navigation, image = "default_avatar_url" }) {
 ...
 // Here are benefits:
 // * Look at function signature -> can clear what properties are being use
 // * Not need defined again variables
 // * Linter can warn you some unused properties
}
```

_Example: function with `many arguments`_

```javascript
function showDialog(title, desc, type, cancellable) {
  // ...
}
showDialog('Title', 'Desc', 'info', true);
```

_Refactor: convert arguments to object with destructuring_

```javascript
function showDialog({ title, desc, type, cancellable }) {
  // ...
}
showDialog({
  title: 'Title',
  desc: 'Desc',
  type: 'info',
  cancellable: true
});
// Or call like this
showDialog({ desc: 'Desc only' });
```

#### Array methods

_Example: Find a item in an array_

```javascript
const numbers = [0, -2, 1, 4, 5, 7];
// Check the array include 5 or not?
```

_Junior code_

```javascript
let isExist = false;
for (const number of numbers) {
  if (number === 5) {
    isExist = true;
  }
}
```

_Refactor with some new JS functions_

```javascript
// Use array.includes to quick check a simple array
const isExist = numbers.includes(5);

// Or use array.find with more powerful (can custom compare function)
const found = numbers.find(number => number > 5);
```

> Other array functions also helpful, pls note it
> `array.map`, `array.filter`, `array.reduce`, `array.some`

### Double bang (!!)

> Convert a values to boolean

Relate concept: [Truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) and  [Falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)

_Example_

```javascript
// Normal way
function BankAccount(cash) {
  this.cash = cash;
  this.hasMoney = cash > 0 ? true : false;
}
// Can rewrite with double bang
function BankAccount(cash) {
  this.cash = cash;
  this.hasMoney = !!cash;
}

const myAccount = new BankAccount(100); // cash = 100, hasMoney = true
const emptyAccount = new BankAccount(0); // cash = 0, hasMoney = false
```

#### Nullish coalescing operator (??)

> The nullish coalescing operator (??) is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand.

_Example: Function to get the display name of user_

```javascript
const user = {
    firstName = null,
    lastName = null,
    nickName = 'cuibap'
}

function getDisplayName({ firstName, lastName, nickName }) {
    if (firstName) {
        return firstName;
    }
    if (lastName) {
        return lastName;
    }
    if (nickName) {
        return nickName;
    }
    return "Anonymous";
}

getDisplayName(user); // cuibap
```

_Can rewrite one line with `Nullish operator`_

```javascript
function getDisplayName({ firstName, lastName, nickName }) {
    return firstName ?? lastName ?? nickName ?? "Anonymous";
}
```

### Optional chaining (?.)

_Example: read a property of an object obj which has a nested structure (many level)_

```javascript
let customer = {
  name: "Nam",
  details: {
    age: 30,
    location: "Da Nang"
  }
};

// Requires validating the references parent prop before access child prop
let customerCity = customer && customer.details && customer.details.address && customer.details.address.city;
```

_Refactor with `optional chaining (?.)`_

```javascript
let customerCity = customer.details?.address?.city; // Underfined

// Also good when use with nullish coalescing operator to set failback valued
let customerCity2 = customer.details?.address?.city ?? "Unknown"; // Unknown
```

