# JavaScript Advanced Functions: Introduction to Context

## Learning Goals

- Define the term "record"
- Define the term "record-oriented programming"

## Introduction

Let's take a moment to appreciate where we are. We've reviewed the basic use
and creation of functions. We've applied these skills in the context of
collection-processing methods like `map`, `reduce`, and `forEach`. We're now
ready to face one of the (infamously) most-challenging parts of JavaScript:
working with execution context. We're going to start this sequence of lessons
off by defining five key terms. Each will be addressed in depth elsewhere, but
we want to give you a survey first so you can say "Oh, this is important" when
you see the terms.

**Definitions**

1. Execution Context: When JavaScript functions run, they have an associated
   JavaScript `Object` that goes along with them which they can access by the
   keyword `this`.
2. `this`: Inside a function, `this` is the `Object` represents the function's
   execution context
3. `call`: This is a method _on a function_ which calls the function, just like
   `()`. You provide a new execution context as the first argument,
   traditionally called `thisArg`, and the arguments you want to send to the
   function after the `thisArg`. An invocation of `call` looks like:
   `Calculator.sum.call(multilingualMessages, 1, 2)
3. `apply`: This is a method _on a function_ which calls the function, just like
   `()`. You provide a new execution context as the first argument,
   traditionally called `thisArg`, and the arguments you want to send to the
   function ***as an `Array`*** after the `thisArg`. An invocation of `call`
   looks like: `Calculator.sum.apply(multilingualMessages, [1, 2])
4. `bind`: This method returns _a copy_ of the function but with the execution
   context "set" to the argument that's passed to `bind`. It looks like this:
   `sayHello.bind(greenFrog)("Hello") //=> "Mr. GreenFrog says *Hello* to you
    all."`

Printing up these definitions is what _most_ JavaScript documentation does.
People accept these as a truth and shrug and muddle their way through. We think
it can be done better.

In this lesson we're going to practice what we've already learned about
JavaScript to build a time-card application, guided by tests. This application
is an example of a "record-oriented" application, which we'll explain below.
Once we have a working application, we'll show how execution context, `this`,
`call`, `apply` and `bind` can DRY up our code.

With these capabilities, we hope you'll learn to love functions even more
&mdash; maybe even as much as JavaScript does!

## Define the Term "Record"

Back in the old days (1960s and earlier) computers didn't have much memory.
Records were stored on, if you can even believe this, small paper cards called
punch-cards. They looked like this:

<PIC>

These cards, or records, had information on them in "fields." In the
`first_name` field you'd find a first name, etc. So when a business needed to
figure out how much to pay each person for a week's work, they would

* Load up all the employees' cards into a tray
* Feed the tray into the computer
* The computer would read the data on the cards
* Calculate the hours worked for the week per card
* Emit a new _record_ with all the old data but this a new field added like
`wagesPaidInWeek33OfYear: 550`
* Print out a table of the employee name and the amount owed

> **ASIDE**: Come to think of it, iterating over a collection, performing a
> transformation and emitting a new collection where every element has been
> transformed sounds an _awful_ lot like `map` to us.

Then the pay table could be taken and the payroll department and the
appropriate person could write (write!) out paychecks to the employees.

If the executive team needed to know how much payroll was for the company for
this week, they'd (you guessed it!) load up all those punch cards in a tray and
run them through a different program that calculated a total.

> **ASIDE**: Come to think of it, iterating over a collection, performing an
> evaluation on each element and emitting a new value based on those elements
> sounds an _awful_ lot like `reduce` to us.

Ultimately the "punch card" was an intermediate step between paper records and
digital records. But it was during the punch-card era that computing really got
big, so a _lot_ of our ways of thinking about programming started by thinking
about "records."

## Define the Term "Record-Oriented Programming"

[Record-oriented programming][rop] is a style of programming based on finding
records and processing them so that they're updated (`map`-like) or so that
their information is aggregated (`reduce`-like).

The amazing thing is that in the 21st century this style of programming is back
in vogue! We're not using punch cards, but the ability to spin up hundreds of
little computers in a cloud, hand them each a bundle of records, and get
answers back is _cutting-edge_.

In fact, a program to do `map` and `reduce` operations at scale on a cloud was
standardized in the 2000's. Guess what it's called? [`mapReduce`][mapreduce]
&mdash; and you should know why. The "Go" programming language, argued by some
to be the next Java as of 2019, is built around building and processing records
at scale. Record-Oriented Programming is not likely to go away any time soon.

## Lab

In this lab we're going to build a time-card and payroll application using the
record-oriented approach. 

The tests guide you to implementing a time card system: when someone enters the
company's state of the art technical office, the employee has to insert their
card in a time-clock which will record the time they came in. When it's time to
leave, the employee will "punch out."

For simplicity's sake, we'll make these assumptions:

1. Assume that employees always check in **and** check out
2. Assume employees always check in and our on the hour
3. The time is represented on a 24-hour clock (1300 is 1:00 pm); this keeps the
   math easier and is the standard in most of the world
4. When timestamps are needed, they will be provided as `String`s in the form:
   `"YYYY-MM-DD 800"` or `"YYYY-MM-DD 1800"` e.g. `"2018-01-01 2300"`
5. Employees will never work across days i.e. in at `2200` and out at `0400` the
   next day.

The lab tests will guide you toward a solution. Keep in mind, the goal is to
understand how to "grow" an application in "record-oriented" fashion in
JavaScript, _as well_ as pass the lab. Make sure you're learning about this app
design while you pass the solutions.

Take advantage of your collection-processing strengths that you trained up over
the last few lessons.

Put your code in `index.js`.

## Conclusion

Congratulations! At the end of this lab you should have built several
incredibly simple functions that leveraged `map` and `reduce` to transform and
aggregate data. Take a look at your code and see where you might be repeating
yourself. Finding these repetitions will be where we can bring in the
innovation of execution context. We'll learn how this can DRY up our code using
execution contexts in the next lesson.

It's also worth your time to take a look at the tests in `test/indexTest.js`.
Because of this application's design, it's incredibly easy to test the
functions which drive the application. Some programmers consider this style of
programming to be optimal for the ease of testing and simplicity of code.

## Resources

* [Record / Record-Oriented Programming][rop]

[rop]: https://en.wikipedia.org/wiki/Record_(computer_science)
[mapreduce]: https://en.wikipedia.org/wiki/MapReduce
