# TypeScript-Intro

## _Introduction_
Typescript is a superset of the javascript language. It gives the javascript developer an option of checking run time errors before runtime with it’s type checking. TypeScript is a statically typed language and cannot run in the browser or a node environment, however, it makes writing clean and error free code more easier. Additional features such as interfaces and generics, decorators.

## _Set Up_
```bash
#install node

#install typescript
npm install -g typescript

#initialize typescript
tsc --iniit
```

## _Working with Types_

* Core (primitive) types in ts includes number (integer, float), string, boolean.
```typescript
const even: number = 4;
const name: string = "Kelechi Mbawuike";
const isLoading: boolean = true;
```
* Other types includes object, arrays, tuple, undefined, any, unknown, null
* With type inference, ts automatically assigns a type to a variable based on its values.
```typescript
const odd = 5; //implicitly assigns number type to odd
```
* Objects in TS are smiliar to objects in JS, however unlike JS, TS object are strictly typed such as you either defined the types of the object keys or TS assigns the type based on its value (implicit)
```typescript
//implicit type assign
const obj1 = {
  name: "kelechi",
  age: 5
}

//type assignment
const obj2: {name: string, age: number} = {
  name: "Kelechi",
  age: 22
}
```
* In TS arrays are strictly typed if the type of the content is known, however it can also be loosely typed if the types of the contnent and the length of the array is unknown.
```typescript
//strictly typed
const fruits: string[] = ["Orange", "Apple", "Mango"]
const oddNumbers: number[] = [1,4,5,7]

//loosely typed
const items: any[] = ['Orange', 2, true]

```
* Tuples are array like types, which takes a specific amount of items (specified length) with one or more types.
```typescript
const tupleEx: [string, number, boolean] = [“Kelechi”, 34, true]
```
* undefined, null thesame with that of javascript. uknown on the otherhand is similar to undefined, however unknown values cannot be accessed and will through an error during compile time.
* In TS union allow the assignment of two or more types to a variable
```typescript
let item: number | string;
item = 50
item = "fifty"
```
* In addition to the general types string and number, we can refer to specific strings and numbers in type positions. This type is called called **literal types**
```typescript
let x: "hello" = "hello";
// OK
x = "hello";
// ...
x = "howdy";
// Type '"howdy"' is not assignable to type '"hello"'.
```
* **Custom type or Type Alias** is used to create custom type which rides on already defined types. They help in making types reuseable
```typescript
type Combinable = string | number;
type CombineDescription = "as number" | 'as string'
type NumberArray = number[]

```
* **Void type** is usually used in functions that doesn't return anything
```typescript
function printResult(num: number): void{
  console.log('Result' + num)
}
```
* **Function Types** are functions that describes a functions with regards to the parameters and return values. You can also define callback function types.
```typescript
function combineValues: (a:number, b:number)=> number
const add(n1:number, n2:number){
  return n1 + n2
}
const printData = (x: number, z: number, cb: (num: number)=> void) => {
  const result =  x + y;
  cb(result)
}

printData(8, 9, (result)=> console.log(result))
``` 
## _TypeScript Complier_
*   **watch mode** in ts automatically complies the specified ts files automatically as it changes.
```
tsc app.ts -w
```
* tsconfig.json is used to mansge typescript project with multiple files.
```
# tracks all changes in the project
tsc -w
```
## _Classes_
* Class rides on the concept of object oriented programming
* classes are basically blueprints of objects. They make creating a similar objects easy
* the constructor function is a special function used to initialize properties or medthods in a class, it runs immediately the class is initiated
* functions in classes are called **methods
* this in objects simply refers to the object. it is used to access the properties and methods of the object.
```typescript
class Department {
  name: string;
  constructor(n: string){
    this.name = n

  }
  describe(this: Department):void{
    console.log(this.name)
  }
}



const accounting =  new Department("Account")
accounting.describe()

const accountCopy = {
  describe: accounting.describe,
  name: "Finance"
}

accountCopy.describe()  
```
* Private and Public are very important concepts in OOP which helps in defining how the class properties and methods are been used or manipulated. Private properties or methods can only be accessed inside the class, while public properties can be accessed in the class or outside the classs.
