# Chapter 2 - TypeScript's Type System

TS generates code, but the type system is the main event. 

## Item 6: Use your editor to interrogate and explore the Type System
When you install TS, you get two executables: 
- tsc, the TS compiler 
- tsserver, the TS standalone server

Editors will show you the inferred type.

Take advantage of the TS language services by using an editor that can use them.
Use your editor to build an intuition for how the type system works and how TS infers types.
Known how to jump into type declaration files to see how they model behavior. 

## Item 7: Think of types as sets of values
At runtime, every variable has a single value chosen from JS's universe of values. Could be:
- undefined
- null
- 10
- 'hello world'

But before your code runs, when TS is checking for errors, a variable just has a *type*. 
And this is best thought of as a *set of possible values*.
This set is known as the *domain* of the type. 

The smallest set is the empty set, which contains no values. It corresponds to the *never* type in TS. 

`const x: never = 12`  // Type '12' is not assignable to type 'never';

The next smallest sets are those which contain single values. These correspond to literal types in TS, aka "unit types".
`
type A = 'A';
type Twelve = 12;
`
There's also union unit types:

`type AB = 'A' | 'B';`

Union types corresopnd to unions of sets of values; 

At the end of the day, almost all the type checker is doing is testing whether one set is a subset of another. 

#### Intersections
`
type Person = {
	name: string;
}

type Lifespan = {
	birth: Date;
	death?: Date;
}

type PersonSpan = Person & Lifespan;
`

The & operator computes the intersection of two types.

Remember that an object can still belong to a type even if it has additional props that were not mentioned in the type declaration. 



