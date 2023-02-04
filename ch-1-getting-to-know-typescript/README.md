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