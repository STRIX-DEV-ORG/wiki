# STD - Coding with Javascript

## Objective

Describes what practices should be followed in order to code correctly when work with javascript.

## Content

It is necessary to review the following standard, if you are already familiar with it you can skip this part.



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

### Indentation and Spacing

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

## Versions

| Version | Description        | Responsibles                     | Date       |
| ------- | ------------------ | -------------------------------- | ---------- |
| 1.0     | Standard creation  | Erick Eduardo Avalos Riveros     | 15/01/2023 |
