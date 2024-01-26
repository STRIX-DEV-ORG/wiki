---
description: Standards about Typescript code
tags: [typescript, js, code]
---

# STD - Typescript Code

## Objective

TypeScript introduces a wealth of features that go beyond traditional JavaScript, providing a robust set of tools for building scalable applications. To maximize the benefits of this powerful language, our TypeScript coding standards focus on specific features unique to TypeScript, ensuring a consistent and effective approach to their usage.

## Content

### Typescript Specific Standards

TypeScript coding standards focus on specific features unique to TypeScript, ensuring a consistent and effective approach to their usage. Next, some of the most important features of Typescript, why we should use them and how.

- #### Type Annotations:
    Emphasizing explicit type annotations ensures that the types of variables, function parameters, and return values are clear and well-defined. This enhances code readability and helps catch potential issues early in the development process.
    ```ts
    const numberA: number = props.a
    const numberB: number = props.b

    const total: string = numberA + numberB
    //Type `number` is not assignable to type `string`.
    ```

- #### Interfaces:
    Interfaces are a cornerstone of TypeScript, offering a way to define clear object shapes and contracts. Leveraging interfaces promotes consistency in data structures, facilitates documentation, and fosters a shared understanding of our codebase.
    ```ts
    interface Person {
        name: string,
        lastName: string,
        ...
    }
    ```

- #### Classes:
    TypeScript's class-based object-oriented programming brings structure to our applications. Proper constructor initialization and the use of access modifiers enforce encapsulation, contributing to maintainable and scalable code.
    ```ts
    class GoodGreeter {
        name: string;
        
        constructor() {
            this.name = "hello";
        }
    }
    ```
    

- #### Enums:
    Enums provide a concise and readable way to represent sets of named constants. By using enums, we enhance code readability, reduce the likelihood of errors, and promote a standardized approach to constant values.
    ```ts
    enum Options {
        OPTA,
        OPTB,
        OPTC
    }

    switch(optionFromUI){
      case Options.OPTA:
        // do something
        break; 
      case Options.OPTB:
        // do something 
        break;
      case Options.OPTC:
        // do something
        break;
  }
    ```
    See more about enums and its types [here](https://www.typescriptlang.org/docs/handbook/enums.html)

- #### Generics:
    Generics offer a powerful mechanism for writing flexible and reusable functions and classes. Embracing generics enhances code efficiency, reduces redundancy, and facilitates the creation of versatile components.
    ```ts
    class GenericNumber<NumType> {
        zeroValue: NumType;
        add: (x: NumType, y: NumType) => NumType;
    }
    
    let myGenericNumber = new GenericNumber<number>();

    myGenericNumber.zeroValue = 0;
    myGenericNumber.add = function (x, y) {
        return x + y;
    };
    ```
    See more about generics [here](https://www.typescriptlang.org/docs/handbook/2/generics.html)

- #### Type Assertion:
    Type assertion is a valuable tool for dealing with dynamic data types. We advocate for the use of the as syntax, providing clear type information and ensuring a modern and consistent approach.
    ```ts
    const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
    ```

- #### Namespace Usage:
    Modern JavaScript practices favor ES6-style module systems over TypeScript namespaces. This guideline ensures that our code organization aligns with current industry standards, fostering compatibility and ease of maintenance.
    ```ts
    namespace Shapes {
        // do something...
    }
    ```
    See more about Namespaces [here](https://www.typescriptlang.org/docs/handbook/namespaces.html#first-steps
)
   
- #### Module Systems:
    Choosing a suitable module system is crucial for managing dependencies effectively. Our recommendation aligns with widely adopted module systems, promoting a standardized and scalable approach to code organization.
    ```ts
    export function f() { return g() }
    function g() { }
    ```
    See more about Module [here](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#module-system)

- #### Decorators:
    Decorators offer a clean and concise way to enhance class behavior and annotate metadata. Incorporating decorators in our codebase enables us to streamline functionality and maintain a clear separation of concerns.
    ```ts
    function second() { }
    console.log("second(): factory evaluated");
    return function (target: any, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("second(): called");
    };
  ```
  See more about Namespaces [here](https://www.typescriptlang.org/docs/handbook/decorators.html#introduction)

### Top Recommendations

As you may know the Typescript Programming Language was designed to make it easier to build and maintain large-scale applications by providing features such as static typing, interfaces, classes, and modules, so from our general experience and how the official documentation marks, we encourage you to:

#### 1. Explicitly define types for variables, function parameters, and return values.

TypeScript supports an extension of the JavaScript language, which offers places for you to tell TypeScript what the types should be, this also helps to the developer what we want to use in a certain function, or why we should not add strings to a counter variable, in summary makes the code more maintainable and easy to understand.

Example:
```ts
// Remember to use primitive types when possible!
const listOfNames: string[] = ["Atreus", "Thor", "Mimir"]
let totalFriends: number = 0

listOfNames.forEach((name: string) => {
    if(Kratos.isFriendOf(name)) {
        totalFriends += 1;
    }
});
```
#### 2. Avoid the use of the `any` type whenever possible.

We know that the `any` type is useful when you don’t know what a third party function or component returns (like a callback that returns the error from a invalid input in Formik). **But** this is also a double-edged sword, this might confuse the reader, and also generate the common error of "property not found in undefined" for example:

```ts
function showToastFromLibrary() {
    const toast = ToastThirdPartyLibrary();
    toast.show().catch((error: any) => {
        // the error could have a message property or not
        console.log(error.message)
    });
}
```

So in order to avoid this please consult the official documentation fo that component or if it possible to control what we should return please go ahead and create the error object. <!-- TODO add - See more in error handling.-->


#### 3. Use Optional Chaining (?)

In TypeScript 3.7 they added this pretty useful feature, optional chaining lets us write code where TypeScript can immediately stop running some expressions if we run into a null or undefined. The star of the show in optional chaining is the new ?. operator for optional property accesses. When we write code like:


```tsx
interface Person {
    name: string,
    lastName: string,
    zipCode?: number
}
function PersonComponent({
    name,
    lastName,
    zipCode,
    ...props
}: Person): JSXElement {
    
    if (zipCode != null){
        isValidZipCode(zipCode)
    }
    // rest of the code
}
```

This is one of the most important things to do, **check for nullable values** this will make the code more defensive of human errors, and also allows to skip a property if we don't need to pass it for a specific reason.

### Conclusion

The TypeScript coding standards presented emphasize explicit type annotations, proper use of interfaces, classes, enums, generics, and other language features to ensure consistent and effective code. Key recommendations include explicitly defining types, avoiding the any type when possible, and leveraging optional chaining for defensive coding. Following these standards will enhance code readability, maintainability, and scalability in TypeScript projects.

You can find more about `Do and Don'ts` [here](https://www.typescriptlang.org/docs/handbook/declaration-files/do-s-and-don-ts.html)

## Versions

| Version | Description       | Responsibles                     | Date       |
| ------- | ----------------- | -------------------------------- | ---------- |
| 1.0     | Standard creation | Ernesto Cabañas Albarran | 25/01/2024 |
