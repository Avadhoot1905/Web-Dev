
continuing from [[JavaScript]]

https://youtu.be/d56mG7DezGs?si=4smm_n_8FSdHG0EB

- Dynamically typed language with type safety
![[Pasted image 20250113011916.png]]

# stuff we uncomment in tsconfig

- rootdir - sets a root directory to store all ts files
-  outdir - sets a directory to store corresponding js files
- noEmitOnError - Disable emitting files if any type checking errors are reported
-  sourceMap - helps us understand how each js file maps to the correspndant ts files - not imp - used for debugging
- noImplicitAny - so basically if u pass a variable in a function, u would get an error and u would have to explicitly write it as a any variable; enabling this, does it by default

# Data Types

![[Pasted image 20250113013738.png]]

Q) Difference between let and var in ts

A)
```ts
var x = 10;
var x = 20; // No error

let y = 30;
let y = 40; // Error: Cannot re-declare block-scoped variable 'y'
```

- arrays in ts or js can generally contain all sorts of data types unless specifically mentioned or if a particular data type is used implicitly 

# Functions

```ts
function function_name(parameter: data_type(optional)): return_data_type(optional){
	//funtion definition
	return variable; //should be of the particular return data type if mentioned or could be any data type
}
```

- u can also make certain parameters optional by using the "?"
```ts
function function_name(parameter1 ,parameter2?): return_data_type(optional){
	//funtion definition
	return variable; 
}
```

- or u can also give the parameter a default value which would be used if no argument was passed

![[Pasted image 20250113020310.png]]

# Objects

- in js, objects are dynamic unlike in ts
- ![[Pasted image 20250113020613.png]]

- union data type - can make a variable to have multiple data types

# Very Imp

In TypeScript, **type aliases** are a way to give a type a new, reusable name. They allow you to define a custom type that can represent more complex types or combinations of types, improving code readability, maintainability, and reusability.

### Defining a Type Alias

You define a type alias using the `type` keyword, followed by the name of the alias and the type it represents.

```ts
type AliasName = TypeDefinition;
```

### Examples of Type Aliases

#### Basic Example

```ts
type StringAlias = string;

let myString: StringAlias = "Hello, TypeScript!";
```

Here, `StringAlias` is just an alias for the `string` type.

#### Union Types

Type aliases are especially useful with union types, where a value can be of multiple types.

```ts
type ID = string | number;

let userId: ID = 123; // number
userId = "abc123";    // string
```

#### Object Types

You can use type aliases to define the shape of an object.

```ts
type User = {
  id: number;
  name: string;
  isAdmin: boolean;
};

const user: User = {
  id: 1,
  name: "Alice",
  isAdmin: true,
};
```

#### Function Types

Type aliases can define the signature of a function.

```ts
type AddFn = (a: number, b: number) => number;

const add: AddFn = (a, b) => a + b;
```

#### Intersection Types

Type aliases can also combine multiple types using intersections.

```ts
type Address = {
  street: string;
  city: string;
};

type Contact = {
  phone: string;
  email: string;
};

type Employee = Address & Contact;

const employee: Employee = {
  street: "123 Main St",
  city: "Metropolis",
  phone: "123-456-7890",
  email: "employee@example.com",
};
```

### Differences Between Type Aliases and Interfaces

Both **type aliases** and **interfaces** can define the shape of objects, but there are key differences:

|Feature|Type Alias|Interface|
|---|---|---|
|Object Types|✅|✅|
|Union and Intersection Types|✅|❌ (only for objects via `extends`)|
|Extendability|❌ (cannot be reopened)|✅ (can extend and be extended)|
|Declaration Merging|❌|✅|

#### Example:

```ts
type User = {
  name: string;
};

// Cannot add properties to an existing type alias.
type User = {
  age: number; // Error: Duplicate identifier 'User'.
};

interface User {
  name: string;
}

// Can add properties to an existing interface.
interface User {
  age: number;
}

const user: User = {
  name: "Alice",
  age: 30,
};
```

### When to Use Type Aliases

- For **union** and **intersection** types.
- When defining function signatures.
- When you want more flexibility in defining complex types.

### When to Use Interfaces

- For defining **objects** and **classes**, especially when you need extendability or declaration merging.

### Conclusion

Type aliases are a versatile feature of TypeScript, complementing interfaces by enabling the definition of unions, intersections, and other more flexible type structures. Use them where they fit best based on your specific needs!