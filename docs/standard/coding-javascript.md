# STD - Coding with Javascript

## Objective

Describes what practices should be followed in order to code correctly when work with javascript.

## Content

### Importing Libraries

- The import of the libraries should be given priority to the external components, then and if required, to the library of the styles and finally to the components created for that project.

```js title="Example"

✅ 

import Box from '@mui/material/Box';
import Container from '@mui/material/Container';
import Stack from '@mui/material/Stack';
import Typography from '@mui/material/Typography';

import styled from '@mui/material/styles/styled';

import QuestionItem from "../molecules/QuestionItem";
import { FAQProps } from '../props';

❌ 

import QuestionItem from "../molecules/QuestionItem";
import { FAQProps } from '../props';

import Box from '@mui/material/Box';
import Container from '@mui/material/Container';
import Stack from '@mui/material/Stack';
import Typography from '@mui/material/Typography';

import styled from '@mui/material/styles/styled';

```

- Prioritize components as they are called in the code, i.e. if you start a grid and there is a button inside it, you must first import the grid library and then the button library.

```js title="Example"

✅ 

import Box from '@mui/material/Box';
import Stack from '@mui/material/Stack';
import Typography from '@mui/material/Typography';

❌ 

import Stack from '@mui/material/Stack';
import Typography from '@mui/material/Typography';
import Box from '@mui/material/Box';

```

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

- Use Pascal case as our naming convention for React components.

```js title="Example"

✅ import ReservationCard from './ReservationCard';
✅ import ControlledInput from './ControlledInput';
✅ import ControlledSelect from './ControlledSelect';

❌ import reservationCard from './ReservationCard';
❌ import reservation_card from './ReservationCard';
❌ import reservationcard from './ReservationCard';
```

- Use the file name as the component name.

```js title="Example"

✅ import ReservationCard from './ReservationCard';
✅ import ControlledInput from './ControlledInput';
✅ import ControlledSelect from './ControlledSelect';

❌ import Controlled from './ControlledSelect';
❌ import Footer from './Footer/Footer';
❌ import Footer from './Footer/index';
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

-  When importing the libraries, you leave a line break between the external components, the library that allows you to modify the styles and components created for the project.

```js title="Example"

✅ 

import Box from '@mui/material/Box';
import Container from '@mui/material/Container';
import Stack from '@mui/material/Stack';
import Typography from '@mui/material/Typography';

import styled from '@mui/material/styles/styled';

import QuestionItem from "../molecules/QuestionItem";
import { FAQProps } from '../props';

❌ 

import Box from '@mui/material/Box';
import Container from '@mui/material/Container';

import Stack from '@mui/material/Stack';
import Typography from '@mui/material/Typography';
import QuestionItem from "../molecules/QuestionItem";

import { FAQProps } from '../props';

import styled from '@mui/material/styles/styled';

```

### Declaring Variables and Methods

- If you're working with variables that will be modified during code execution, use "let". Whereas if your variable will not change its value at any time, use "const".

```js title="Example"

✅ 

let y = 30;
const x = 20;
if (true) {
    let y = 40; 
    console.log(y); 
}
console.log(x); 

❌ 

const y = 30;
let x = 20;
if (true) {
    const y = 40; 
    console.log(y); 
}
console.log(x); 

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
| 1.0     | Standard creation  | Erick Eduardo Avalos Riveros     | 26/12/2023 |
