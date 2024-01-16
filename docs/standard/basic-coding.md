# STD - Basic Coding

## Objective

Describes what practices should be followed in order to code correctly.

## Content

### Naming Variables

- Use Camel case as our naming convention for instances.

```js title="Example"

✅ const firstName =  User.name; 
✅ Car.wheelsNumber = 4;
✅ const square = number * number;

❌ const firstname =  User.name;
❌ Car.wheels_number = 4;
❌ const Square = number * number;
```

- The attributes, methods, classes, objects, or any variable you are going to use must have a coherent name to what you want to allude to. That is, if you were talking about a name, the attribute could be name.

```js title="Example"

✅ const firstName =  User.name; 
✅ Car.wheelsNumber = 4;
✅ const square = (number) => number * number; 

❌ const x =  User.name;
❌ Car.number = 4;
❌ const square = (i) => i*i;

```

- Avoid oversimplifying variable names. Continuing with the example, if you have a name attribute, and you need to divide it into first and last name. Choose to type "first name" and "last name" instead of "f name" and "l name" respectively.

```js title="Example"

✅ const firstName =  User.name; 
✅ Car.wheelsNumber = 4;
✅ const square = (number) => number*number; 

❌ const x =  User.name;
❌ Car.wNum = 4;
❌ const s = (n) => n*n;

```

### Indentation and Spacing

- The code must be correctly indented, opt for a 4-space indentation instead of 2.

```js title="Example"

✅ 

if (number < 5) {
    print("Hello")
else:
    print("Bye")                
}

❌ 

if (number < 5) {
  print("Hello")
  else:
    print("Bye")                
}
```

- Leave at least one free line between each function. In case the feature has a description with comments, there should be no space between the description and the role.

```js title="Example"

✅ 

// This function greets
function Greet({ hello }) {
  return <div>{hello}</div>;
}

// This function is being said goodbye
function Bye({ goodbye }) {
  return <div>{goodbye}</div>;
}

❌ 

// This function greets

function Greet({ hello }) {
  return <div>{hello}</div>;

  
}
// This function is being said goodbye
function Bye({ goodbye }) {
  return <div>{goodbye}</div>;
}

```
- Avoid spaces before commas and require a space after commas

```js title="Example"

✅ const foo = 1, bar = 2;
✅ const arr = [1, 2];

❌ const foo = 1,bar = 2;
❌ const arr = [1 , 2];
```

### Comments & Descriptions

- When a block of code is complex, you should add a comment that explains the intent of the block. To indicate that the code block is complete, use a line break.

```js title="Example"

✅ 

/*
   This set of JavaScript functions provides simple mathematical operations:

   1. calculateSquare: Calculates the square of a given number.
   2. calculateCube: Calculates the cube of a given number.
   3. displayResult: Displays the results of square and cube calculations for a given number.

   Ensure to provide a valid number as input to avoid errors.
*/

// Function to calculate the square of a number.
function calculateSquare(number) {
    if (typeof number === 'number') {
        return number * number;
    } else {
        console.error('Invalid input. Please provide a valid number.');
        return NaN;
    }
}

// Function to calculate the cube of a number.
function calculateCube(number) {
    if (typeof number === 'number') {
        return number * number * number;
    } else {
        console.error('Invalid input. Please provide a valid number.');
        return NaN;
    }
}

// Function to display the result of square and cube calculations.
function displayResult(number) {
    const squareResult = calculateSquare(number);
    const cubeResult = calculateCube(number);

    if (!isNaN(squareResult) && !isNaN(cubeResult)) {
        console.log(`For the number ${number}:`);
        console.log(`Square: ${squareResult}`);
        console.log(`Cube: ${cubeResult}`);
    }
}

❌ 

// Function to calculate the square of a number.
function calculateSquare(number) {
    if (typeof number === 'number') {
        return number * number;
    } else {
        console.error('Invalid input. Please provide a valid number.');
        return NaN;
    }
}

// Function to calculate the cube of a number.
function calculateCube(number) {
    if (typeof number === 'number') {
        return number * number * number;
    } else {
        console.error('Invalid input. Please provide a valid number.');
        return NaN;
    }
}

// Function to display the result of square and cube calculations.
function displayResult(number) {
    const squareResult = calculateSquare(number);
    const cubeResult = calculateCube(number);

    if (!isNaN(squareResult) && !isNaN(cubeResult)) {
        console.log(`For the number ${number}:`);
        console.log(`Square: ${squareResult}`);
        console.log(`Cube: ${cubeResult}`);
    }
}


```

- When a function implements complex logic or the name of the function is not descriptive enough, it is necessary to write a brief description of the function with a brief comment.

```js title="Example"

✅ 

// This function checks if a given number is prime.
function isPrime(number) {
    if (number <= 1) {
        return false;
    } else if (number <= 3) {
        return true;
    } else if (number % 2 === 0 || number % 3 === 0) {
        return false;
    } else {
        for (let i = 5; i * i <= number; i += 6) {
            if (number % i === 0 || number % (i + 2) === 0) {
                return false;
            }
        }
        return true;
    }
}

❌ 

function isPrime(number) {
    if (number <= 1) {
        return false;
    } else if (number <= 3) {
        return true;
    } else if (number % 2 === 0 || number % 3 === 0) {
        return false;
    } else {
        for (let i = 5; i * i <= number; i += 6) {
            if (number % i === 0 || number % (i + 2) === 0) {
                return false;
            }
        }
        return true;
    }
}

```

- When you use an external function without altering or reinterpreting it, i.e. making a copy paste. You must add the source link as a comment before the feature.

```js title="Example"

✅ 

// Function to calculate the cube of a number. Obtained of "www.example.com"
function calculateCube(number) {
    if (typeof number === 'number') {
        return number * number * number;
    } else {
        console.error('Invalid input. Please provide a valid number.');
        return NaN;
    }
}


❌ 

// Function to calculate the cube of a number.
function calculateCube(number) {
    if (typeof number === 'number') {
        return number * number * number;
    } else {
        console.error('Invalid input. Please provide a valid number.');
        return NaN;
    }
}


```

- Avoid leaving commented code, unless it is consulted with the work team. If approved, refrain from leaving space between the comment symbol and the code when commenting.

```js title="Example"

✅ 

// Function to calculate the cube of a number.
function calculateCube(number) {
    if (typeof number === 'number') {
        return number * number * number;
    } else {
        //console.error('Invalid input. Please provide a valid number.');
        return NaN;
    }
}

❌ 

// Function to calculate the cube of a number.
function calculateCube(number) {
    if (typeof number === 'number') {
        //   return number * number * number;
    } else {
        //console.error('Invalid input. Please provide a valid number.');
        //  return NaN;
        console.error('No.');
    }
}

```

## Versions

| Version | Description        | Responsibles                     | Date       |
| ------- | ------------------ | -------------------------------- | ---------- |
| 1.0     | Standard creation  | Erick Eduardo Avalos Riveros     | 15/01/2023 |
