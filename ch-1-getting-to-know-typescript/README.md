# Item 1: Understand the Relationship Between TS & JS

Important to note that TS neither runs in an interpreter (Python or Ruby) nor complies down to a lower-level language (Java or C). Rather, it compiles to another high-level lanugage - JavaScript. 

## TypeScript offers gentle migration. 
If you have a js codebase and want to migrate to typescript, 

> All JavaScript is TypeScript, but not all TypeScript is JavaScript.

If you throw something like:

`
function sayHi(): void {
	console.log('hi');
};
`

Into node, you will get an error stating that ':' isn't recongized. 

> Type annotations tell ts what your *intent* is and lets it spot places where your code's behavior does not match your intent.

TypeScripts type system *models* the runtime behavior of JavaScript. 

# Item 2: Know Which TS Options You're Using

The TypeScript compiler accepts options (up to about 100 different ones) that dictate behavior at compilation. 

You can set the options at the command line or via a config file (preferred). The config file approach is preferred because it makes it easy for coworkers and tools to know exactly how you plan to use TS. 

Create one by running 
`tsc --init`

## Most Important TS Settings

#### noImplicitAny
This controls whether variables must have known types

` {
	'noImplicitAny': true
}`

Under this config, the following code would pass the TS compliation.

`function add(a, b) {
	return a + b;
}`

You should take on the challenge of enabling 'noImplicitAny' when you're starting a new project as it forces you to correctly type everything. In a situation where you're updating a js project to ts, you wouldn't want to do this however. 

#### strictNullChecks

strictNullChecks controls whether null and undefined are permissible values in every type. 

With strictNullChecks disabled, something like this would be okay:

`
const name: string = null; 
` 

However, with strictNullChecks enabled (true), you would need to update the above statement to:

`const name: string | null = null;`

Same advice goes for strictNullChecks as for noImplicitAny. If you're starting a fresh repo, enable it and use TS to it's fullest. However, if you're bringing an old js-only project up to ts standards, you probably want to disable this as you will have a flurry of errors looking like:

` Type 'null' is not assignable to type .... `
or another fan favorite: 
`undefind is not an object `

#### strict setting

If you want to enforce the strictest settings including the two above and others, simply enable strict in your ts config and you won't have to explicitly set the others. This is the ideal and will likely be painful at first, but will force you to use the language to it's fullest. 

Remember - keep ts settings the same across your team as you won't be able to reproduce certain errors without doing so. 

# Item 3 - Understand that code gen is independent of types

## The TypeScript Compiler (tsc) does two things:
1. Converts next-gen TS/JS to an older version of JS that works in the browser (process called transpiling);
2. Checks your code for type errors

It's important to note that these two behaviors are independent of each other. Meaning, a type error *can* still produce a code output. 

We can think of type errors as warnings - they will indicate that there is a problem, but the code will still build. 

| Saying your code "doesn't compile" isn't technically correct. Better to say your code has errors or that it doesn't type check.

## Typescript types have no runtime performance

Because types and type operations are erased when you generate JS, they have no effect on runtime performance. 
TS static types are truly zero cost.

# Item 4 - Get comfortable with structural typing

- JS is duck typed and TS uses structrual typing to model this (values assignalbe to your interfaces might have properties beyond those explicitly listed in your type declarations). Types are not "sealed." 

# Item 5 - Limit use of the *any* type. 

TS's type system is both *gradual* and *optional* 

*Gradual* because you can add types to your code bit by bit

*Optional* because you can disable the type checker whenever you like. 

Using *any* pretty much eliminates the type safety all together. It lets you assign a string to a number, etc. 

Remeber, since js is pretty loosely typed, it is problematic to use *any* in your ts as it might introduce unexpected behavior such as that of JS being willing to implicitly convert between types. 

### *Any* disables autocomplete

Do you like your code editor showing you the available properties on an object? Well, *any* disables that. 