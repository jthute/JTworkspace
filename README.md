# JTworkspace
Typescript.js
TypeScript Cheat Sheet

Installing
For the latest stable version:

npm install -g typescript
For our nightly builds:

npm install -g typescript@next

In order to build the TypeScript compiler, ensure that you have Git and Node.js installed.

Clone a copy of the repo:

git clone https://github.com/Microsoft/TypeScript.git
Change to the TypeScript directory:

cd TypeScript
Install Gulp tools and dev dependencies:

npm install -g gulp
npm install
Use one of the following to build and test:

gulp local            # Build the compiler into built/local
gulp clean            # Delete the built compiler
gulp LKG              # Replace the last known good with the built one.
                      # Bootstrapping step to be executed when the built compiler reaches a stable state.
gulp tests            # Build the test infrastructure using the built compiler.
gulp runtests         # Run tests using the built compiler and test infrastructure.
                      # You can override the host or specify a test for this command.
                      # Use --host=<hostName> or --tests=<testPath>.
gulp baseline-accept  # This replaces the baseline test results with the results obtained from gulp runtests.
gulp lint             # Runs tslint on the TypeScript source.
gulp help             # List the above commands.

Flow-to-TypeScript Build Status npm mit
Compile Flow files to TypeScript

Installation
# Using Yarn:
yarn add flow-to-typescript

# Or, using NPM:
 npm install flow-to-typescript --save
Usage
CLI
# Install globally
 yarn global add flow-to-typescript

Now you can build your test files with a simple command in the console:
 tsc --watch --project test/tsconfig.json

# Compile a file (all of these are equivalent)
flow2ts my/file.js.flow
flow2ts my/file.js.flow my/file.ts
flow2ts my/file.js.flow > my/file.ts
flow2ts -i my/file.js.flow -o my/file.ts
flow2ts --input my/file.js.flow --output my/file.ts
Programmatic
import { compile } from 'flow-to-typescript'
import { readFileSync, writeFileSync } from 'fs'

let path = 'path/to/file.js.flow'
let file = readFileSync(path, 'utf-8')

compile(file, path).then(ts =>
  writeFileSync('path/to/file.ts', ts)
)
TypeScript vs. Flow
Features
Done?		Flow	TypeScript
white_check_mark	Maybe	?type (NullableTypeAnnotation)	type | null | undefined
white_check_mark	Null	null	null
white_check_mark	Undefined	typeof undefined	undefined
white_check_mark	Mixed	mixed	unknown
white_check_mark	Void	void	void
white_check_mark	Functions	(A, B) => C	(a: A, b: B) => C
⚔	Predicates (0)	(a: A, b: B) => %checks	(a: A, b: B) => C
⚔	Predicates (1)	(a: A, b: B) => C %checks	(a: A, b: B) => C
white_check_mark	Exact types	{| a: A |}	{ a: A }
white_check_mark	Indexers	{ [A]: B }	{ [a: A]: B }
white_check_mark	Opaque types	opaque type A = B	type A = B (not expressible)
white_check_mark	Variance	interface A { +b: B, -c: C }	interface A { readonly b: B, c: C }
white_check_mark	Bounds	<A: string>	<A extends string>
white_check_mark	Casting	(a: A)	(a as A)
white_check_mark	Import default type	import type A from './b'	import A from './b'
white_check_mark	Import named type	import type { A } from './b'	import { A } from './b'
Utilities
Done?		Flow	TypeScript
Keys	$Keys<A>	keyof A
Values	$Values<A>	A[keyof A]
white_check_mark	ReadOnly	$ReadOnly<A>	Readonly<A>
white_check_mark	Exact	$Exact<A>	A
Difference	$Diff<A, B>	TODO`
Rest	$Rest<A, B>	Exclude
Property type	$PropertyType<T, k>	T[k]
Element type	$ElementType<T, K>	T[k]
Dependent type	$ObjMap<T, F>	TODO
Mapped tuple	$TupleMap<T, F>	TODO
Return type	$Call<F>	ReturnType
Class	Class<A>	typeof A
Supertype	$Supertype<A>	any (warn - vote for https://github.com/Microsoft/TypeScript/issues/14520)
Subtype	$Subtype<A>	B extends A
Existential type	*	any (warn - vote for https://github.com/Microsoft/TypeScript/issues/14466)
white_check_mark Done
