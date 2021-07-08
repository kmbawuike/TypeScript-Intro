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
* Private and Public are very important concepts in OOP which helps in defining how the class properties and methods are been used or manipulated. Private properties or methods can only be accessed inside the class, while public properties can be accessed in the class or outside the classs. Also, readOnly access modifier enforces immutability of properties.  Once they are intialized, they can't be modified.
```typescript
class Department {
  private employees: string[] = [];
  constructor(public name: string, private readonly id: number) {
    this.name = name
    this.id = id

  }
  describe(this: Department): void {
    console.log(`Department with name of ${this.name} and id of ${this.id}`)
  }

  addEmployee(this: Department, employee: string){
    this.employees.push(employee)
  }
  printEmployees(this: Department){
    console.log(this.employees)
  }
}



const accounting = new Department("Account", 5)
accounting.addEmployee("Kelechi Mbawuike")

// accounting.employees = "Stella" won't work
accounting.describe()

accounting.printEmployees()

```
* Inheritance is an OPP principle or concept which allows two or more classes share properties or methods. it is a core concept of  OOP as it helps in creating scalable systems. a class can inherit from another class by using the  **extends** keyword. During inheritance, the super keyword is used to initialize the properties of the parent class (call the constructor function of the parent class)
```typescript
class Department {
  private employees: string[] = [];
  constructor(private id: number, public name: string) {
    this.name = name
    this.id = id

  }
  describe(this: Department): void {
    console.log(`Department with name of ${this.name} and id of ${this.id}`)
  }

  addEmployee(this: Department, employee: string) {
    this.employees.push(employee)
  }
  printEmployees(this: Department) {
    console.log(this.employees)
  }
}

class ITDepartment extends Department {
  public adminRoles: string[]
  constructor(id: number, adminRoles: string[]) {
    super(id, 'Information Techmology')
    this.adminRoles = adminRoles
  }
  getRoles(this: ITDepartment){
    this.adminRoles.map((role, key) => console.log(`Role ${key} is ${role}`))
  }
}

class UtilityDepartment extends Department{
  constructor (id: number, private permissions: number[]){
    super(id, 'Utility Department')
    this.permissions = permissions
  }
  getPermissionsNumber(this: UtilityDepartment){
    return this.permissions.length
  }
}

const payStackIT = new ITDepartment(5, ["Admin", "Employee", "Manager"])
payStackIT.addEmployee("Kelechi Mbawuike")

// accounting.employees = "Stella" won't work
payStackIT.describe()

payStackIT.printEmployees()
payStackIT.getRoles

const payStackUtil = new UtilityDepartment(7, [1,3 ,6])
payStackUtil.addEmployee("Festus")
payStackUtil.getPermissionsNumber()

```
* unlike **private**, a class **protected** properties or methods is accessible it's  child classes
```typescript
class Department {
  protected employees: string[] = [];
  constructor(private id: number, public name: string) {
    this.name = name
    this.id = id

  }
  describe(this: Department): void {
    console.log(`Department with name of ${this.name} and id of ${this.id}`)
  }

  addEmployee(this: Department, employee: string) {
    this.employees.push(employee)
  }
  printEmployees(this: Department) {
    console.log(this.employees)
  }
}

class ITDepartment extends Department {
  public adminRoles: string[]
  constructor(id: number, adminRoles: string[]) {
    super(id, 'Information Techmology')
    this.adminRoles = adminRoles
  }
  getRoles(this: ITDepartment) {
    this.adminRoles.map((role, key) => console.log(`Role ${key} is ${role}`))
  }

  addEmployee(this: ITDepartment, employee: string) {
    if (employee.toLocaleLowerCase().includes("mbawuike")) {
      return this.employees.push(employee)
    }
  }
}

const payStackIT = new ITDepartment(5, ["Admin", "Employee", "Manager"])
payStackIT.addEmployee("Kelechi")
payStackIT.addEmployee("Mbawuike Kelechi")

// accounting.employees = "Stella" won't work
payStackIT.describe()

payStackIT.printEmployees()
payStackIT.getRolesclass Department {
  protected employees: string[] = [];
  constructor(private id: number, public name: string) {
    this.name = name
    this.id = id

  }
  describe(this: Department): void {
    console.log(`Department with name of ${this.name} and id of ${this.id}`)
  }

  addEmployee(this: Department, employee: string) {
    this.employees.push(employee)
  }
  printEmployees(this: Department) {
    console.log(this.employees)
  }
}

class ITDepartment extends Department {
  public adminRoles: string[]
  constructor(id: number, adminRoles: string[]) {
    super(id, 'Information Techmology')
    this.adminRoles = adminRoles
  }
  getRoles(this: ITDepartment) {
    this.adminRoles.map((role, key) => console.log(`Role ${key} is ${role}`))
  }

  addEmployee(this: ITDepartment, employee: string) {
    if (employee.toLocaleLowerCase().includes("mbawuike")) {
      return this.employees.push(employee)
    }
  }
}

const payStackIT = new ITDepartment(5, ["Admin", "Employee", "Manager"])
payStackIT.addEmployee("Kelechi")
payStackIT.addEmployee("Mbawuike Kelechi")

// accounting.employees = "Stella" won't work
payStackIT.describe()

payStackIT.printEmployees()
payStackIT.getRoles



```
* getters are basically methods that returns properties of a class, usually private or protected properties. a getter function must always return a value. The **get** keyword is used to define a getter method. Similar to getter, a setter is used to manipulate class properties. Getters and setters of private or protected properties is often used to encaspulate logic from the outside word.
* **static** properties and methods are tied directly to the class and are accessed directly without instatiating the class. e.g **Math.pow()**
```typescript
class Department {
  protected employees: string[] = [];
  constructor(private id: number, public name: string) {
    this.name = name
    this.id = id

  }

  addEmployee(this: Department, employee: string) {
    this.employees = [...this.employees, employee]
  }
  printEmployees(this: Department) {
    console.log(this.employees)
  }
}

class ITDepartment extends Department {
  public adminRoles: string[]
  constructor(id: number, adminRoles: string[]) {
    super(id, 'Information Techmology')
    this.adminRoles = adminRoles
  }
  getRoles(this: ITDepartment) {
    this.adminRoles.map((role, key) => console.log(`Role ${key} is ${role}`))
  }
 
  get getEmployees(){
    if (this.employees.length > 0){
      return this.employees
    }else{
      throw new Error("Employees array is empty");
      
    }
  }

  set setEmployees(employees: string[]){
    if(employees.length <= 0){
      throw new Error("Cannot set empty array");
    }else{
      this.employees = [...this.employees, ...employees]
    }
  }

  addEmployee(this: ITDepartment, employee: string) {
    if (employee.toLocaleLowerCase().includes("mbawuike")) {
      return this.employees.push(employee)
    }
  }

  static createEmployee(name: string){
    return {name}
  }
}

const payStackIT = new ITDepartment(5, ["Admin", "Employee", "Manager"])

payStackIT.setEmployees = ["Kenny", "Fletcher", "next"]
console.log(payStackIT.getEmployees, "Getter method")
console.log(ITDepartment.createEmployee('Newman Stanley'))
payStackIT.getRoles
```
* Abstract Classes - Abstract class is very important while working with related classes that share similar properties and methods. An abstract method in an abstract class will always force it's child class to implement it. they are defined with the **abstract** keyword
```typescript
abstract class Department {
  protected employees: string[] = [];
  constructor(protected id: number, public name: string) {
    this.name = name
    this.id = id

  }
  abstract describe(): void;
  addEmployee(this: Department, employee: string) {
    this.employees = [...this.employees, employee]
  }
  printEmployees(this: Department) {
    console.log(this.employees)
  }
}

class ITDepartment extends Department {
  public adminRoles: string[]
  constructor(id: number, adminRoles: string[]) {
    super(id, 'Information Techmology')
    this.adminRoles = adminRoles
  }

  describe(){
    console.log(`${this.name} : ${this.id}`)
  }

  static createEmployee(name: string) {
    return { name }
  }
}

const payStackIT = new ITDepartment(5, ["Admin", "Employee", "Manager"])

console.log(ITDepartment.createEmployee('Newman Stanley'))

payStackIT.describe()
```
* Singletons and Private Constructors: The singleton pattern of OOP ensures a class has only one instance of itself. This done by defining a private constructor

```typescript
abstract class Department {
  protected employees: string[] = [];
  constructor(protected id: number, public name: string) {
    this.name = name
    this.id = id

  }
  abstract describe(): void;
  addEmployee(this: Department, employee: string) {
    return this.employees = [...this.employees, employee]
  }
  printEmployees(this: Department) {
    console.log(this.employees)
  }
}

class ITDepartment extends Department {
  public adminRoles: string[]
  private static instance: ITDepartment
  private constructor(id: number, adminRoles: string[]) {
    super(id, 'Information Techmology')
    this.adminRoles = adminRoles
  }

  describe() {
    console.log(`${this.name} : ${this.id}`)
  }

  static getInstance() {
    if (ITDepartment.instance) {
      return this.instance
    }
    this.instance = new ITDepartment(5, ['Admin', 'Employee', 'Manager'])
    return this.instance

  }

  static createEmployee(name: string) {
    return { name }
  }
}

const payStackIT = ITDepartment.getInstance()
 console.log(payStackIT, payStackIT.addEmployee("Lionel Messi"))
 payStackIT.describe()
```

##_Interfaces_
* An interface simply describes the structure of an object (How an object should look like). They are basically used to type check objects.
```typescript
interface Person {
  name: string;
  age: number;
  greet(phrase: string): void;
}

let user1: Person;
user1 = {
  name: "Kelechi",
  age: 24,
  greet(phrase: string) {
    console.log(`${phrase} ${this.name}`)
  }
}

user1.greet('Good Morning')
```
* Interfaces are similar to Custom Types in TS, however, unlike custom types which have union types, interfaces can only have a single type thus making it clearer.
* Interface are basically used as contracts followed by a class. They are basically used to share functionalities amongst differnt classes not regarding their complete implemetation. Interfaces are similar to abstract classes, however in Interfaces unlike Abstract classes who can't have implemetations or values inside an interface. A class can implement multiple interfaces by sepearating them with commas.
```typescript
interface Greetable {
  name: string;
  greet(phrase: string): void;
}

class Person implements Greetable {
  name: string;
  constructor(name: string){
    this.name = name
  }
  greet(phrase: string) {
    console.log(`${phrase} ${this.name}`)
  }
}

let user1: Greetable
user1 = new Person("Kelechi")

user1.greet('Good Morning')
```
* interfaces just as custom types can also have readonly attribute accessors and can inherit(extend) from one another
```typescript

interface Named{
 readonly name: string;
}

interface Greetable extends Named {
  greet(phrase: string): void;
}

interface Aged{
  age: number
}

class Person implements Greetable, Aged {
  name: string;
  constructor(name: string, public age: number){
    this.name = name
    this.age = age
  }
  greet(phrase: string) {
    console.log(`${phrase} ${this.name}`)
  }
}

const user1 = new Person("Kelechi", 5)

user1.greet('Good Morning')
```
* Interfaces and Classes can also have optional properties and methods (they are not required)
```typescript

interface Named {
  readonly name?: string;
}

interface Greetable extends Named {
  greet(phrase: string): void;
}

interface Aged {
  age: number
}

class Person implements Greetable, Aged {
  name?: string;
  constructor(name: string = 'Mr Nothing', public age: number) {

    this.name = name

    this.age = age
  }
  greet(phrase: string) {
    console.log(`${phrase} ${this.name}`)
  }
}

const user1 = new Person(undefined, 5)

user1.greet('Good Morning')
```

 
