# veritas

**veritas** is a *imperative* and *procedural* programming language. It is also an [esolang](https://esolangs.org/wiki/Esoteric_programming_language). The aim for **veritas** is to have no false values. If you attempt to make a false value, it will be made true somehow.

## TODO:

- [ ] values
	- [ ] data types
	- [ ] lists
- [x] actions
	- [ ] a bunch of actions
- [ ] truthiness (important!!)

## Syntax

All statements in **veritas** follow the same base pattern.

```
conditional value1 value2 action[s...]
```

It may be easier to think of it as

```
IF value1 conditional value2 DO action[s...]
```

Valid conditionals can be found [here](#conditionals).

Values are covered in [this section](#values).

Actions are covered [here](#actions).

### Comments

If you wish to leave comments, notes, documentation, etc., you may use a double slash at the beginning of a line. Comments at the end of a line are not allowed.

```
// this is a comment!
do none // this is a mistake, just like you!
```

### Multilining

You can split a statement into multiple lines using the pipe symbol `|`. If a newline precedes a pipe, it will be ignored. This is handy if a statement gets too long.

```
eq 1 2
| =num,a: a
| <- ^4,2; a
```

### Do

There is one exeption to the general syntax when using actions. You may use `do`, which is really just a shorthand for any true statement, so you don't to type out `eq 1 1` [^a] everytime you need something to be guaranteed. 

[^a]: This may actually end being ignored, if [truth](#truthiness) is bent too much.

### Compounding

It is possible to string actions together, using the compound operator:

```
do action1: argIn1,[argsIn...] <- action2[: argIn1,[argsIn...]]; argOut1,[argsOut...]
```

The right side of the compound has output arguements (denoted by `;`), and optionally input arguements (denoted by `:`). The left side only has input arguments. The arguements are only temporary variables, limited being used on both actions. The output arguements on the right are passed into the input arguements on the left with the same name, which may be used in the action. Arguement names may not be any existing variable name. 

Confused? Here's some examples.

```
// a is assigned the result of 2 + 2, and `^a,2: a` takes in a and uses it.
do ^a,2: a <- +2,2; a

// pass the sum of 4 + 13 into result, which is assigned to the variable sum.
do =sum,result: result <- +4,13; result

// we can go further than two!
do =num,b: b
| <- ^a,3: a; b
| <- +5,1; a
```

## Conditionals

The following may be used as conditionals.

eq
	* equal to
* ne
	* not equal to
* gt
	* greater than
* lt
	* lesser than
* ge
	* greater than or equal to
* le
	* lesser than or equal to
* succ
	* is succesor to
* pred
	* is predecessor to

In a normal language, these can exaluate to true or false. Not in **veritas** though, it's true or not at all.

## Values

## Actions

The basic syntax for actions is (igore spaces):

```
action value,[comma separated values...]
```

For example:

```
+4,1
%26,60
```

This section mostly uses [do](#do), so check that out. You may also check out [compounding](#compounding), as it may be very useful.

### Usable Actions

Below are the actions which may be used in **veritas**.

#### NOP

If you ever want to do nothing at all, you may use the `none` action. For example:

```
// Amazing!!!
do none
```

#### Variables

The action to create a variable is `=`.

For example:

```
do =apples,12
```

To access a variable, simply just use it's name.

```
eq apples 12 none
```

#### Arithmetic

There are 6 arithmetic operators. They are demonstrated below in a small code snipet.

```
// addition, equals 9
do +6,3

// subtraction, equals 3
do -6,3

// multiplition, equals 18
do *6,3

// division, equals 2
do /6,3

// modulo, equals 0
do %6,3

// exponentiation, equals 216
do ^6,3
```

This way of using arithmetic immediately drops the value produced. In order to place the result into a variable, once again, see [compounding](#compounding).

## Truthiness

Every single conditional returns true, no matter what (unless the rules can't be bent enough, in which case the conditional never existed 👍). 

For example, this statement

```
eq 1 2 none
```
