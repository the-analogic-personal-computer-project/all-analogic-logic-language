# SYNTAX AND RULES OF ALL
1. [Addition `+`](#addition)
2. [Subtraction `-`](#subtraction)
3. [Multiplication `*`](#multiplication)
4. [Division `/`](#division)
5. [Comparison `?`](#comparison)
6. [Inputs/Constants `:`](#inputsconstants)
7. [Simple functions `=`](#simple-functions)
8. [Inline functions `()`](#inline-functions)
9. [Complex or composite functions `{} []`](#complex-or-composite-functions)
10. [Outputs `|`](#outputs)
11. [Comments `//`](#comments)
12. [Functions with a variable number of arguments `#`](#functions-with-a-variable-number-of-arguments)
13. [Good pratices and objectives](#good-pratices-and-objectives)

# Operations
There is five operations, represented by the symbols `+ - * / ?`.
**Warning:** The order to be followed is the writing one !
### Addition
Represented normally with the `+` symbol.
Example of use:
`a = 1 + 1;` a = 2

### Subtraction
Represented normally with the `-` symbol, can also be used to write negative values.
Equivalent examples of use:
`a = 3 - 1;` a = 2;
`a = 3 + -1;` a = 2.

### Multiplication
Represented normally with the `*` symbol.
Example of use:
`a = 1 * 1;` a = 1.

### Division
Represented normally with only one `/` symbol.
Example of use:
`a = 4 / 2;` a = 2.

### Comparison
Represented by the use of `?` symbol, followed by 2 or 3 arguments, everything split by `,`.
The arguments must start with `<` or `>`, always having the `!` argument.
Examples of use for `a = B ? C, > 5, < 6, ! 7;` where:
`B = 2, C = 1` a = 5, because B is greater than C `>`;
`B = 1, C = 2` a = 6, because B is less than C `<`;
`B = 1, C = 1` a = 7, because none of the conditions was satisfied `!`.


# Variables
**Warning:** All of them must end with `;` like many languages.
### Inputs/Constants
Must be defined with `:`.
By being defined with numbers, they become constants.
By being defined with the own name, they become inputs on their scope (the general program or complex function).
Equivalent examples of use:
`A:1; B:B; a = A + B;` Puting the value "1" on input "B" the result of "a" will be "2";
`A:1; a = A + :B;` Is possible to define in abreviated mode, using the name after colon.
*Recomended to be written in UPPERCASE.*

### Simple functions
Must be defined with `=`.
Can be read later, but never re-written.
Example:
`a = 1 + 2; b = a * 3;` b = 9.
Can also use it's own name as "memory" inside the function:
`mem = A ? B, > C, ! mem;`
In this example, if "A" is greater "B" the value will be replaced by "C", otherwise will stay the same as the previous iteration.
The read value of the first iteration will always be null, meaning zero.
*Recomended to be writen in lowercase.*

### Inline functions
Must be written inside `()` in another variables.
Examples:
`a = 2 * (9 - 1);` a = 16;
`a = 2 * 9 - 1;` a = 17, because the written order was followed.

### Complex or composite functions
Must be defined with `{}` and called with `[]` alongside with the arguments, passes with `=`.
The last part must be the own name as a simple function, with the value to be returned.
Example:
```
func{
	a = :B + :C;
	func = a + 1;
};
result = func[B=1, C=2];
```
Where the result would be 4.
Like simple functions, the memory rule of apply the own name also applies.
Internal components of the function can be read is mentionated with `.`, or even read two values at the same time, by using `,` on call:
`result, a = func[B=1, C=2].a;` result = 4, a = 3.
*Recomended to be writen in lowercase.*

### Outputs
Are declared with `|` before the name, after the target value.
Must be think as "probes".
The name cannot be repeated in the same escope.
Example:
`A:1; A|Output; a = A + A;` Output = 1.
*Recomended to be writen in CamelCase.*


# Extras
### Comments
Like in many languages, can be written with `//`, but the end must have `;` like variables do.
`a = 1 + 1; //Text to be ignored by the compiler/interpreter; b = 2 + 2;` a = 2, e b = 4.

### Functions with a variable number of arguments
When composite functions are so generic that they could use different ammount of arguments, they can use inputs with variable size.
To declare such inputs, the symbol `#` is used, followed with arguments (like comparation operation) with the number of subarguments or if the number is divisible by a number, followed with an inline function with how each subargument must be threat sequentially.
When the number of arguments is repetitive, `.` can be used instead of written all of them.
To call, is especified the arguments inside `[]` for such input.
Example with addition function:
```
sum{
	sum = A#/1(A+.);
};
a = sum[ A=[1,1] ]; //Output is 2;
b = sum[ A=[1,1,1] ]; //Output is 3;
```
Example of a function with optional but limited arguments:
```
func{
	func = A#0(1),1(A),2(A + A);
}
a = func[];				//Output is 1;
b = func[A=[]];			//Output is 1;
c = func[A=[5]];		//Output is 5;
d = func[A=[7, 3]];		//Output is 10;
e = func[A=[1, 2, 3]];	//Invalid expression;
```
*In case of the expression seems dubious, do not use it !*

### Good pratices and objectives
- Being a language to project/express the function of components inside an analogic computer, it must seem natural for almost any reader, and be centered in physical connections that the components may have - putting the order of where the data will go from top to bottom, definitions on another pages, at end or begin.
- The name of inputs or outputs on the main escope must be the components of interaction from the computer, ex: `TERMOMETER` and `GaugePointer`, or even, parts must have each subpart named.
- Being the components something that threat electrical signals, makes sense to use multiplication and division as they are proportion changers, but addition and subcration with constants (and not other kinda of variables) may not make sense, for that is recommended to have an input on global escope `:ONE` to be used as reference for certain calcules. Its important to think in propotions and not values.  
- In comparison function, the argument `!` must be think in being activated with the values dont have a significative difference to activate the other(s) argument(s). Because in real components is necessary a certain level to trigger, or special cases like [schmitt triggers](https://en.wikipedia.org/wiki/Schmitt_trigger) do.
- Like memory can be used repeating the self name as argument, feedback can be represented using an argument of a function that will be declared/called later on the program.
- To threat values that tends to infinity (up or down) must be though in the limits of the voltages of the circuit. For values that are result of division of 0, this limits may be the return. A good pratice would be use constants with values on volts or multiples, ex: `GND:0; VCC:5000;`.
