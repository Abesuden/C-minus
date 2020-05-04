<meta name="keywords"    content="C-, C-minus, C minus, C, C- compiler, C- grammar, C- Eggen, C minus Eggen, C- University of North Florida, compilers University of North Florida, compilers, cop4620, C- cop4620, cop4620 C-, Alex Besuden, Alexander Besuden, Austin Laurin">
<meta name="description" content="This documentation is about the C- language and how to understand it for making a compiler.">
<meta name="author"      content="Alexander Besuden, Austin Laurin">

# C- Grammar Rules

[![Language](https://img.shields.io/badge/Language-C---informational.svg)](https://github.com/abesuden/C-minus/contributors)
[![Contributors](https://img.shields.io/badge/Contributors-2-informational.svg)](https://github.com/abesuden/C-minus/contributors)
[![Maintenance](https://img.shields.io/badge/Maintained-yes-brightgreen.svg)](https://github.com/abesuden/C-minus/graphs/commit-activity)
[![Progress](https://img.shields.io/badge/Progress-100%25-brightgreen.svg)](https://github.com/abesuden/C-minus)
[![Issues](https://img.shields.io/badge/Issues-0-bluegreen.svg)](https://github.com/abesuden/C-minus/graphs/commit-activity)

[![OOP](https://img.shields.io/badge/OOP-no-informational.svg)](https://github.com/abesuden/C-minus/contributors)
[![NamingConvention](https://img.shields.io/badge/NamingConvention-camelCase-informational.svg)](https://github.com/abesuden/C-minus/contributors)
[![CaresAboutWhiteSpace](https://img.shields.io/badge/CaresAboutWhiteSpace-no-informational.svg)](https://github.com/abesuden/C-minus/contributors)

![C- Logo](https://github.com/Abesuden/C-minus/blob/master/img/logo.png)

As students of [Dr. Eggen's](unf.edu/~ree) Compilers class, at the [University of North Florida](unf.edu), we decided to help create documentation for [Dr. Eggen's](unf.edu/~ree) C- language for all future students. The main motivation came from the fact that Google does not have every answer and when we tried to search for knowledge on the C- language, we could not find anything of use. Hopefully this helps all future students with understanding the C- language and have it help to build the compiler.

## Table of Contents

  - [Recommendations](#Recommendations)
  - [Summary](#Summary)
  - [Getting Started](#Getting-Started)

    <details>
    <summary><strong>-expand-</strong></summary>

    - [Variables Naming Convention](#Variables-aming-Convention)
    - [Run Time Error](#Run-Time-Error)
    - [Initializing Variables](#Initializing-Variables)
    - [Assigning Variables](#Assigning-Variables)
    - [Functions](#Functions)
      - [Headers](#Headers)
      - [Body](#Body)
      - [Return Statement](#Return-Statement)
    
    </details>

  - [Conditionals](#Conditionals)
  - [Loops](#Loops)
  - [Compund Statement](#Compund-Statement)
  - [Quadruples](#Quadruples)
  - [Contributing](#Contributing)
  - [Versioning](#Versioning)
  - [Authors](#Authors)
  - [License](#License)
  - [Acknowledgments](#Acknowledgments)


## Recommendations

  * Be familiar with the C language
  * Currently taking or have taken a compilers class

[^TOC](#Table-Of-Contents)

## Summary

The C- language is a subset of the C language. That means anything you can do in C- can be done in C, but not everything in C can be done in C-. The twenty-nine grammer rules for C- can be found [here](https://csunplugged.files.wordpress.com/2012/12/compiler-construction-principles-and-practice-k-c-louden-pws-1997-cmp-2002-592s.pdf) on page 492 (501). As with any grammar, the type of parser will have to be chosen, such as LR(1) or LALR(1), and once done the grammar may need to be modified in order to work with the chosen parser. However, this level of detail will not be coverd in this documentation. What will be covered deals with what acceptable syntax and symantics look like.

[^TOC](#Table-Of-Contents)

## Getting Started

The C- language has the nice property of being made up of only a small amount of rules as compared to the C language. This property makes C- easier to code a compiler and you will see that the implementation of its grammar will be straightforward. It is important to note that, when constructing a program in C-, the program needs to have a `main` function just like that found in the C language. Below is an example of a required `main` funciton setup:

```
int main(void) {

  return 0;
}
```
> you will see many further examples without the main function, however the `main` function is required for all programs to compile correctly in C- and will be implied.

It is also important to note that the `main` function must be the last function and every other function that is created must come before the `main` function. Also, the C- language does not care about whitespace.

[^TOC](#Table-Of-Contents)

### *Variables Naming Convention*

In the C- language, the naming convention is not like other programming languages. Variable names can only consist of letters, like those seen in the below example:

```
var
varName
varOne
VarTwo
```
> Note: camel case is allowed

Below are examples that are not acceptable:

```
var1
var_two
Var_Three
```
> Note: numbers and snake case are not allowed

[^TOC](#Table-Of-Contents)

### *Run Time Error*

The term `run time error` will come up quite a bit and it is important to understand what it means. Whenever there is a `run time error` the code is considered to be acceptable and that you will not need to catch and handle the errors. The errors will appear during run time and it is the C- developers job to know how to avoid such `run time error`. Basically, you are off the hook and do not need to worry about that specific facet of code.

[^TOC](#Table-Of-Contents)

### *Initializing Variables*

When initializing variables, the only variable type that will be used is `int`. You will still need to handle `void` types, however `void` types will not be initialized, rather `void` types will be generated by functions that are returning the type `void`. Below is an example of how a variable will be initialized:

```
int a;
int arrayOne[5];
```
> arrays are included in the C- language

Notice how a did not have a number assigned to it. This is because in the C- language, initializations and assignments ***CANNOT*** happen on the same line. Below is an example of code that will not pass the syntax analyzer because it will print `REJECT`:

```
int a = 42;
int array = {0,1,2,3,4};
int array[5] = {0,1,2,3,4};
```

[^TOC](#Table-Of-Contents)

### *Assigning Variables*

In C-, all variable declarations must be made **before** any assignments are made in a scope in order to follow the grammar rules. Assigning variables is a little bit more complicated because arrays are part of the C- language. Assigning to a variable includes not only values but also indexed arrays and function returns. Below are examples:

```
a = 42;
a = arrayOne[3];
a = arrayOne[b];
a = arrayOne[fun(4)];
a = mathFun(2, 4);
arrayOne[2] = a;
arrayTwo[1] = mathFun(2, 4);
```

Remember that any initialized variable is of type `int` and that it can only be assigned a type `int`. Thus, `a` and any arrays can only store the return value of the `mathFun(2,4)` if it is of type `int`. Below are examples that would not be accepted:

```
a = "Hello World!";
a = "void";
a = True;
a = 'z';
a = voidFun();
arrayOne[0] = "Hello World!";
arrayOne[0] = "void";
arrayOne[0] = True;
arrayOne[0] = 'z';
arrayOne[0] = voidFun();
```
> Note: the `voidFun()` is a function that returns a void type

Once you understand the above examples, then you will need to understand how complicated assigning can actually become. Below are examples of complicated variable assignments but they are still acceptable:

```
a = 5 - 2 + 6 / 3;
a = b = c = d - 4;
a = arrayOne[25]; // even though this array is of size 5, this is still accepted
a = arrayOne[6/2];
a = arrayOne[0] = arrayOne[3] = arrayOne[2-1] = arrayOne[4/1];
```
> Note: an array indexing outside its available size is acceptable because it is considered a [run time error](#Run-Time-Error)

[^TOC](#Table-Of-Contents)

### *Functions*

The C- language supports two types of functions, both type `int` and type `void`. Remember that, in the C laguage, the type specified in the function header is the type thq5 needs to be returned at the end of the function. 

[^TOC](#Table-Of-Contents)

#### *Headers*

Inside a function header, there will be variable initialization, but these, again, will only be of type `int`. Also remember that, like in the C language, the C- language requires the function return type to be defined. Below are examples of acceptable function headers:

```
int funOne () {
```
```
int funOne (int x, int y) {
```
```
void funTwo () {
```
```
void funTwo (int x, int y) {
```
> Note: all function headers must have a `}` at some point and was not shown in the exmple

Examples of not acceptable function headers can be found below:

```
int fun1 () {
```
```
int funOne (void x) {
```
```
int funOne (String x) {
```
```
int funOne (char x) {
```
```
int funOne (bool x) {
```
> Note: the function return type `int` can be replaced with type `void` and it has the same effect

[^TOC](#Table-Of-Contents)

#### *Body*

The body of any function maintains the same rules as found throughout this documentation. However, keep in mind that scope does play a role here. So, if a function has not been defined above, then the current function cannot reference it and there will be an error. For example, this is acceptable:

```
int funOne (int x) {
  return x + 2;
}

void funTwo (int x) {
  if (funOne(x) > 4) {
    return funOne(x);
  } else {
    return x/2;
  }
}
```
> Note: `funOne` was defined before `funTwo` which is calling `funOne`. This is acceptable.

The below example is not acceptable:

```
void funTwo (int x) {
  if (funOne(x) > 4) {
    return funOne(x);
  } else {
    return x/2;
  }
}

int funOne (int x) {
  return x + 2;
}
```

[^TOC](#Table-Of-Contents)

#### *Return Statement*

Return statements are tied to the type specified in the header, whether it was `int` or `void`. The below examples are the acceptable return statment for either types `void` or `int`.

```
return;
```
> for type `void`, a return statement is not needed, but it can still have one

```
return a;
```
> for type `int` the returned variable needs to be of type `int`, which all are anyways

```
return array[3];
```
> for type `int` indexed arrays are acceptable

```
return thisFun(y);
```
> for type `int` functions can be recursively called or any previously defined functions

```
return 4 - 3 / 4 * x + 1 - arrayOne[2] aboveFun(4, 5 - 2);
```
> for type `int` complex math should be expected

**Note**: the parser should handle seeing the `return` statements, however if the `return` is not in every possible code path, then it is considered a [run time error](#Run-Time-Error). As seen in the following example below:

```
int funOne (int x) {

  if (x < 5) {
    return 1;
  } else {
    x = 0;
  }

}
```

[^TOC](#Table-Of-Contents)

## Conditionals

Before getting to the conditionals, it is important to know what conditional operators are allowed in the C- language. Following the grammer rules resource text from earlier (also found [here](https://csunplugged.files.wordpress.com/2012/12/compiler-construction-principles-and-practice-k-c-louden-pws-1997-cmp-2002-592s.pdf)), on page 491 (500) there is a reference to what operators are valid. Below is the list for convenience:

```
< <= > >= ++ != =
```

In the C- language, the only conditional that can be used is the `if ()` and `else` statements. The C- language does not support `else if ()` or `switch` statements. The following are acceptable ways to use a conditional:

```
if (x < 5 ) {
  // do something
} else {
  // do something else
}
```
```
if ((x + 3) <= (5 + y / funOne(4, y))) {
  // do something
}
```
> Note: the `else {` can start on a seperate line from the `}`

Below is an example of a conditional that is not acceptable:

```
if ('c' == x) {
  // do something
} else if (4 <= 5) {

}
```
```
if (4 << x) {
  // do something
} else {
  // do something else
}
```
> Note: turnary statements are also not excepted

[^TOC](#Table-Of-Contents)

## Loops

While the concept of loops are supported in the C- language, the only loop that is allowed is the `while ()` loop. Below is an example of acceptable versions of the `while ()` loop:

```
while (count < 5) {
  // do somthing
  count = count + 1;
}
```
> incrementing count was just shown as an example of how to use the `while ()` loop to iterate

```
while (x <= (5 + y / 2 + funThree(4, x, y))) {
  // do somthing
  count = count + 1;
}
```
> math is supported when inside the conditional

Some examples of not acceptable `while ()` loops are as follows:

```
while (x <= 5) {
  // do somthing
  count += 1;
}
```
> the short hand `+=` is not supported in the C- language

```
while (True) {
  // do somthing
}
```
> booleans are not supported in the C- language

```
while (x < 5) {
  // do somthing
  break;
}
```
> `break` statments are not supported in the C- language


[^TOC](#Table-Of-Contents)

## Compound Statement

Compound statements refere to the use of `{` and `}` without any other code. The benifit of a compound statement is to create a new local scope which allows for new variable declerations inside the compound statement. These variables that are locally scoped cannot be used outside from any outer scoped references. An example can be found below:

```
// outer scope
{
  // do something within a local scope
}
// outer scope
```
> Note: anything that is in the outer scope can be referenced from inside the compound statement, but anything inside the compound statement cannot be used outside.

[^TOC](#Table-Of-Contents)

## Quadruples

Quadruples are assembly like code that is spit out so that a RISC (Reduced instruction set computing) device can interperate and produce machine level 1's and 0's. To learn more about what is needed to produce accurate C- language quadruples, find it [here](https://github.com/abesuden/C-minus/quadruples.md). The code that is produced looks similar to what is found below:


```
0       func     main     void       0
1      alloc       40              arr
2      alloc        4                y
3       mult        4        4      t0
4       disp      arr       t0      t1
5        add       t1        5      t2
6     assign       t2                y
7        end     func     main
```
> notice that there are 5 columns that are used to represent the RISC quadruples

The  C- code that the quadruples were generated from the following example:

```
void main(void) {
    int arr[10];
    int y;
    y = arr[4] + 5;
}
```

[^TOC](#Table-Of-Contents)

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code
of conduct, and the process for commiting to this repository.

[^TOC](#Table-Of-Contents)

## Versioning

We use [Git](https://git-scm.com/doc) for versioning. For the versions available, see the [tags on this repository](https://github.com/abesuden/C-minus/tags).

[^TOC](#Table-Of-Contents)

## Authors

  - **Alexander Besuden** - *Created README* - [@abesuden](https://github.com/abesuden)
  - **Austin Laurin** - *Created README* - [@AustinLaurin](https://github.com/AustinLaurin)

See also the list of [contributors](https://github.com/abesuden/C-minus/contributors) who participated in this project.

[^TOC](#Table-Of-Contents)

## License

This project is licensed under the [MIT](LICENSE.md) Creative Commons License - see the [LICENSE.md](LICENSE.md) file for details

[^TOC](#Table-Of-Contents)

## Acknowledgments

  * [@Austin Laurin](https://github.com/AustinLaurin) - for basically being a compiler himself.
  * [Alexander Besuden](http://AlexanderBesuden.com) - for making this documentation beautiful while still allowing for an easy to read and full understanding.
  
 [![ForTheBadge built-with-love](http://ForTheBadge.com/images/badges/built-with-love.svg)](https://GitHub.com/abesuden/C-minus)
 
