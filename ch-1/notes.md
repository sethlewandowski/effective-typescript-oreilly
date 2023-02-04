# Getting to Know TypeScript 

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