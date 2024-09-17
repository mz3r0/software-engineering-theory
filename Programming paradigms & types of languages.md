# Programming paradigms & types of languages

Programming paradigms are a way to classify programming languages based on their features. One programming language can be classified into multiple paradigms.

Some paradigms are concerned mainly with implications for the execution model of the language, such as allowing side effects, or whether the sequence of operations is defined by the execution model. Other paradigms are concerned mainly with the way that code is organized, such as grouping a code into units along with the state that is modified by the code. Yet others are concerned mainly with the style of syntax and grammar.

According to the criticism section on Wikipedia, some programming language researchers criticize the notion of paradigms as a classification of programming languages, e.g. Harper, and Krishnamurthi. They argue that many programming languages, in reality, include features from several paradigms.

**Degree of coupling and cohesion**

In software engineering, coupling is the degree of interdependence between software modules; a measure of how closely connected two routines or modules are; the strength of the relationships between modules. Coupling is usually contrasted with cohesion. Low coupling often correlates with high cohesion, and vice versa. Low coupling is often thought to be a sign of a well-structured computer system and a good design, and when combined with high cohesion, supports the general goals of high readability and maintainability.

The software quality metrics of coupling and cohesion were invented by Larry Constantine in the late 1960s as part of a structured design, based on characteristics of “good” programming practices that reduced maintenance and modification costs. Structured design, including cohesion and coupling, were published in the article Stevens, Myers & Constantine (1974) and the book Yourdon & Constantine (1979).

> In a nutshell: Tight coupling = more interdependency, coordination and information flow while low coupling = higher organization and modularity.

Among the types of cohesion mentioned on Wikipedia, functional cohesion is considered superior. See also 'perfect cohesion' under [High Cohesion](https://en.wikipedia.org/wiki/Cohesion_(computer_science)#High_cohesion).

Peter Van Roy created a [map](https://upload.wikimedia.org/wikipedia/commons/f/f7/Programming_paradigms.svg) with various programming paradigms. Cited sources are: [Programming Paradigms for Dummies: What Every Programmer Should Know](https://www.info.ucl.ac.be/~pvr/VanRoyChapter.pdf) and the book [Concepts, Techniques, and Models of Computer Programming](https://books.google.gr/books?id=_bmyEnUnfTsC&redir_esc=y)

> **TODO: Read the 2 above sources and update this document.**

As stated previously, just as software engineering (as a process) is defined by differing methodologies, so the programming languages (as models of computation) are defined by differing paradigms. 

"Programming paradigms can also be compared with programming models, which allows invoking an execution model by using only an API. Programming models can also be classified into paradigms based on features of the execution model."

> **TODO: Learn what exactly programming models are and how they relate to paradigms.** Context: Using APIs, parallel computing and the below paragraph. Not much is listed on the [Wikipedia article](https://en.wikipedia.org/wiki/Programming_model)

For parallel computing, using a programming model instead of a language is common. The reason is that details of the parallel hardware leak into the abstractions used to program the hardware. This causes the programmer to have to map patterns in the algorithm onto patterns in the execution model (which have been inserted due to leakage of hardware into the abstraction). **As a consequence, no one parallel programming language maps well to all computation problems**. Thus, it is more convenient to use a base sequential language and insert API calls to parallel execution models via a programming model. Such parallel programming models can be classified according to abstractions that reflect the hardware, such as [shared memory](https://en.wikipedia.org/wiki/Shared_memory "Shared memory"), [distributed memory](https://en.wikipedia.org/wiki/Distributed_memory "Distributed memory") with [message passing](https://en.wikipedia.org/wiki/Message_passing "Message passing"), notions of _place_ visible in the code, and so forth. These can be considered flavors of programming paradigm that apply to only parallel languages and programming models.

---

## Unstructured vs Structured

**Non-structured programming** is the historically earliest programming paradigm capable of creating Turing-complete algorithms (citation needed). It is often contrasted with the structured programming paradigm, in particular with the use of **goto statements** or equivalent. The distinction was particularly stressed by the publication of the influential "Go To Statement Considered Harmful" open letter in 1968 by Dutch computer scientist Edsger W. Dijkstra, who coined the term "structured programming".

There are both high- and low-level programming languages that use non-structured programming. Some include JOSS, FOCAL, TELCOMP, assembly languages, MS-DOS batch files, and early versions of BASIC, Fortran, COBOL, and MUMPS.

**Structured programming** (aka modular programming) is a programming paradigm aimed at improving the clarity, quality and development time of a computer program by making extensive use of the structured control flow constructs of selection (if/then/else) and repetition (while and for), block structures, and subroutines. Code becomes more efficient and easy to understand. It is possible to do structured programming in any programming language.

### Early exit

The most common deviation, found in many languages, is the use of a return statement for early exit from a subroutine. This results in multiple exit points, instead of the single exit point required by structured programming. At the level of functions, this is a return statement. At the level of loops, this is a break statement (terminate the loop) or continue statement (terminate the current iteration, proceed with next iteration). Break and continue can be replicated by adding additional branches or tests, but returns from nested code can add significant complexity, and especially as seen in some languages that have "labeled breaks", which allow breaking out of more than just the innermost loop.

The most common problem in early exit is that cleanup or final statements are not executed – for example, allocated memory is not deallocated, or open files are not closed, causing memory leaks or resource leaks. These must be done at each return site, which is brittle and can easily result in bugs. For instance, in later development, a return statement could be overlooked by a developer, and an action that should be performed at the end of a subroutine (e.g., a trace statement) might not be performed in all cases. Languages without a return statement, such as standard Pascal and Seed7, do not have this problem.

Kent Beck, Martin Fowler and co-authors have argued in their refactoring books that nested conditionals may be harder to understand than a certain type of flatter structure using multiple exits predicated by guard clauses. **Their 2009 book flatly states that "one exit point is really not a useful rule. Clarity is the key principle: If the method is clearer with one exit point, use one exit point; otherwise don’t"**.

In his 2004 textbook, David Watt writes that "single-entry multi-exit control flows are often desirable". Using Tennent's framework notion of sequencer, Watt uniformly describes the control flow constructs found in contemporary programming languages and attempts to explain why certain types of sequencers are preferable to others in the context of multi-exit control flows. ... Watt also examines how exception sequencers differ from escape and jump sequencers; this is explained in the next section of [this Wikipedia article](https://en.wikipedia.org/wiki/Structured_programming#CITEREFWattFindlay2004).

### Exception handling

Based on the coding error from the Ariane 501 disaster, software developer Jim Bonang argues that any exceptions thrown from a function violate the single-exit paradigm, and proposes that all inter-procedural exceptions should be forbidden. Bonang proposes that all single-exit conforming C++ should be written along the lines of:

```C
bool MyCheck1() throw() {
  bool success = false;
  try {
    // Do something that may throw exceptions.
    if (!MyCheck2()) {
      throw SomeInternalException();
    }
    // Other code similar to the above.
    success = true;
  } catch (...) {
    // All exceptions caught and logged.
  }
  return success;
}
```

Peter Ritchie also notes that, in principle, even a single throw right before the return in a function constitutes a violation of the single-exit principle, but argues that Dijkstra's rules were written in a time before exception handling became a paradigm in programming languages, so he proposes to allow any number of throw points in addition to a single return point. He notes that solutions that wrap exceptions for the sake of creating a single-exit have higher nesting depth and thus are more difficult to comprehend, and even accuses those who propose to apply such solutions to programming languages that support exceptions of engaging in cargo cult thinking.

David Watt also analyzes exception handling in the framework of sequencers (introduced in the aforementioned article). Watt notes that an abnormal situation (generally exemplified with arithmetic overflows or input/output failures like file not found) is a kind of error that "is detected in some low-level program unit, but (for which) a handler is located in a high-level program unit". For example, a program might contain several calls to read files, but the action to perform when a file is not found depends on the meaning / purpose of the file in question to the program and thus a handling routine for this abnormal situation cannot be located in low-level system code. Watts further notes that introducing status flag testing in the caller, as single-exit structured programming or even (multi-exit) return sequencers would entail, results in a situation where "the application code tends to get cluttered by tests of status flags" and that "the programmer might forgetfully or lazily omit to test a status flag. In fact, abnormal situations represented by status flags are by default ignored!" He notes that in contrast to status flags testing, exceptions have the opposite default behavior, causing the program to terminate unless the programmer explicitly deals with the exception in some way, possibly by adding code to willfully ignore it. Based on these arguments, Watt concludes that jump sequencers or escape sequencers are not as suitable as a dedicated exception sequencer with the semantics discussed above.

In addition, the necessity to limit code to single-exit points appears in some contemporary programming environments focused on parallel computing, such as OpenMP. The various parallel constructs from OpenMP, like parallel do, do not allow early exits from inside to the outside of the parallel construct; this restriction includes all manner of exits, from break to C++ exceptions, but all of these are permitted inside the parallel construct if the jump target is also inside it.

### Multiple entry

More rarely, subprograms allow multiple entry. This is most commonly only re-entry into a coroutine (or generator / semi-coroutine), where a subprogram yields control (and possibly a value), but can then be resumed where it left off (Python does this using `yield`). There are a number of common uses of such programming, notably for streams (particularly input/output), state machines, and concurrency. From a code execution point of view, yielding from a coroutine is closer to structured programming than returning from a subroutine, as the subprogram has not actually terminated, and will continue when called again – it is not an early exit. However, coroutines mean that multiple subprograms have execution state – rather than a single call stack of subroutines – and thus introduce a different form of complexity.

From the [Multiple entry](https://en.wikipedia.org/wiki/Structured_programming#Multiple_entry) section, "It is very rare for subprograms to allow entry to an arbitrary position in the subprogram, as in this case the program state (such as variable values) is uninitialized or ambiguous, and this is very similar to a goto".

> **TODO: Find out examples of multiple entry code.** The words "very rare" imply the existence of such code, which I'm curious about.

---

## High level vs Low level

A **high-level programming language** is a language that has a relatively high level of abstraction.

These languages are programmer-friendly and focus on usability over optimal program efficiency. They deal with variables, arrays, objects, complex arithmetic or Boolean expressions, subroutines, functions, loops, threads, locks, and other abstract computer science concepts. High-level languages are easier to understand and maintain, but they may be less memory-efficient compared to low-level languages.

Examples of high-level languages include Java, Python, C#, and even C and C++. The latter two provide more freedom and control over memory, making them more low-level but not low enough to be considered a low-level programming language.

A **low-level programming language** is a language that is closer to machine language and contains commands that are more specific to processor instructions.

These languages are machine-friendly and focus on efficient program execution. They deal with registers, memory addresses, call stacks, and other low-level computer components. Low-level languages are more difficult to understand for humans but are easier for machines to interpret. They are often used when performance and efficiency are crucial, such as in real-time applications or embedded systems.

Examples of low-level languages include assembly languages and machine code.

---

## Compiled vs Interpreted

Compiled and interpreted programming languages differ in how they are processed and executed by the computer.

In a **compiled language**, the source code is translated directly into machine code that the processor can execute, resulting in faster and more efficient execution. Examples of compiled languages include C, C++, and Fortran.

On the other hand, in an **interpreted language**, the source code is not directly translated into machine code. Instead, an interpreter reads and executes the code line by line, allowing for modifications while the program is running. Examples of interpreted languages include Python, JavaScript, and Ruby.

The key differences between compiled and interpreted programming languages:

| Aspect                  | Compiled Language                                      | Interpreted Language                                      |
|-------------------------|--------------------------------------------------------|------------------------------------------------------------|
| Execution               | Directly translated into machine code                  | Read and executed by an interpreter, usually line by line           |
| Steps to Execution      | Only one step from source code to execution | At least two steps from source code to execution |
| Speed                   | Compiled programs run faster than interpreted programs  | Interpreted programs can be modified while running and tend to be slower        |
| Debugging               | Compilation errors prevent the code from compiling     | Debugging occurs at run-time                               |

Most programming languages can have both compiled and interpreted implementations, and the distinction between compiled and interpreted languages refers to the typical implementation rather than the language itself.

---

## Dynamically typed vs statically typed

In programming, a **statically typed language** is one where the data type of a variable is known at compile time, and remains unchanged throughout the execution of the program. Type checking occurs at compile time, and the type associated with each variable must be known before the source code is compiled. Examples of statically typed languages include C, C++, and Java.

On the other hand, a **dynamically typed language** is one where type checking occurs at runtime or execution time. Variables are checked against types only when the program is executing, and the majority of type checking is performed at run-time. Dynamic typing can be more flexible and easier to use, as developers do not need to specify types explicitly. Examples of dynamically typed languages include Python, JavaScript, Ruby, and PHP.

> In a nutshell: Statically typed refers to type checking at compile time, while dynamically typed refers to type checking at runtime.

### Type systems & type safety

There are multiple [type systems](https://en.wikipedia.org/wiki/Type_system) which determine how the types of data is handled by software. A **type system** is a logical system comprising a set of rules that assigns a property called a type (for example, integer, floating point, string) to every term (a word, phrase, or other set of symbols). Usually the terms are various language constructs of a computer program, such as variables, expressions, functions, or modules.

Even a type can become associated with a type. An implementation of a type system could in theory associate identifications called data type (a type of a value), class (a type of an object), and kind (a type of a type, or metatype). These are the abstractions that typing can go through, on a hierarchy of levels contained in a system.

Whether automated by the compiler or specified by a programmer (automatic inference vs manual annotation), a type system makes program behavior illegal if outside the type-system rules. Advantages provided by programmer-specified type systems include abstraction and documentation, while advantages provided by compiler-specified type systems include optimization and safety.

In computer science, **type safety** and type soundness are the extent to which a programming language discourages or prevents type errors. The behaviors classified as type errors by a given programming language are usually those that result from attempts to perform operations on values that are not of the appropriate data type, e.g., adding a string to an integer when there's no definition on how to handle this case. This classification is partly based on opinion.

Type enforcement can be static, catching potential errors at compile time, or dynamic, associating type information with values at run-time and consulting them as needed to detect imminent errors. Type enforcement can also be a combination of both.

A C example that is not memory-safe:

```c
int x = 5;
char y[] = "37";
char* z = x + y;
printf("%c\n", *z);
```

In this example `z` will point to a memory address five characters beyond `y`, equivalent to three characters after the terminating zero character of the string pointed to by `y`. This is memory that the program is not expected to access. In C terms this is simply undefined behavior and the program may do anything; with a simple compiler it might actually print whatever byte is stored after the string "37".

### Strong vs weak typing

One of the many ways that programming languages are colloquially classified is whether the language's type system makes it strongly typed or weakly typed (loosely typed). However, there is no precise technical definition of what the terms mean and different authors disagree about the implied meaning of the terms and the relative rankings of the "strength" of the type systems of mainstream programming languages. For this reason, writers who wish to write unambiguously about type systems often eschew the terms "strong typing" and "weak typing" in favor of specific expressions such as "type safety".

Generally, a strongly typed language has stricter typing rules at compile time, which implies that errors and are more likely to happen during compilation. Most of these rules affect variable assignment, function return values, procedure arguments and function calling. Dynamically typed languages (where type checking happens at run time can also be strongly typed. In dynamically typed languages, values, rather than variables, have types.

A weakly typed language has looser typing rules and may produce unpredictable or even erroneous results or may perform implicit type conversion at runtime. Advocates of dynamically typed (generally "weakly typed") languages find such concerns to be overblown and believe that static typing actually introduces an exponentially larger set of problems and inefficiencies. A different but related concept is [latent typing](https://en.wikipedia.org/wiki/Latent_typing "Latent typing").

> **TODO: Expand on the topic of latent typing**

Strongly typed language examples include Java, C, C++. Some languages considered weakly typed include Python, PHP and JavaScript, which allow for more flexibility in type conversions.

---

## Imperative & Declarative

Programming paradigms classify programming languages based on their features. One language may be classified into multiple paradigms.

**Imperative programming**. In this programming paradigm, we describe the statements that change the program's state. Focus is on how the program operates, step by step; given a sequence of instructions/commands. This is often contrasted to high-level descriptions of its expected results, as observed in Declarative programming.

Imperative languages are often low-level, meaning they are closer to the hardware and have more control over the memory and performance. Some examples of imperative languages are C, Java, and Python.

The programming paradigm used to build programs for almost all computers typically follows an imperative model. Digital computer hardware is designed to execute machine code, which is native to the computer and is usually written in the imperative style, although low-level compilers and interpreters using other paradigms exist for some architectures such as lisp machines. Many imperative programming languages (such as Fortran, BASIC, and C) are abstractions of assembly language.

> Imperative literally means giving authoritative command for a specific needs.

**Declarative programming**. In this programming paradigm logic of computation is expressed without describing its control flow. Many languages that apply this style attempt to minimize or eliminate side effects by describing what the program must accomplish in terms of the problem domain, rather than describing _how_ to accomplish it as a sequence of the programming language primitives; the how being left up to the language's implementation. This is in contrast with imperative programming, which implements algorithms in explicit steps.

In a few words, declarative programming focuses on what to achieve rather than how to achieve it. Declarative languages are often high-level, meaning they are more abstract and expressive and have less control over the details.

Common declarative languages include those of database query languages (e.g., SQL, XQuery), regular expressions, logic programming (e.g. Prolog, Datalog, answer set programming), **functional programming** (Haskell, OCamel), and configuration management systems. Functional and logic programming languages are characterized by a declarative programming style.

**Imperative vs Declarative**. In reality, most programming languages and applications are not purely imperative or declarative, but rather a mix of both (also called hybrid languages). For example, Python is an imperative language that supports some declarative features, such as list comprehensions and generators. SQL is a declarative language that allows some imperative commands, such as loops and variables. Makefiles, specify dependencies in a declarative fashion, but include an imperative list of actions to take as well. Similarly, yacc specifies a context free grammar declaratively, but includes code snippets from a host language, which is usually imperative (such as C). Hybrid approaches can combine the best of both worlds and offer more flexibility and functionality.

---

## Procedural programming

Procedural programming is a programming paradigm, derived from imperative programming, based on the concept of the procedure call. Procedures (a type of routine or subroutine) simply contain a series of computational steps to be carried out. Any given procedure might be called at any point during a program's execution, including by other procedures or itself. The first major procedural programming languages appeared c. 1957–1964, including Fortran, ALGOL, COBOL, PL/I and BASIC. Pascal and C were published c. 1970–1972.

Procedural programming languages are also imperative languages, because they make explicit references to the state of the execution environment. This could be anything from variables (which may correspond to processor registers) to something like the position of the "turtle" in the Logo programming language. Procedural programming could be considered a step toward declarative programming. A programmer can often tell, simply by looking at the names, arguments, and return types of procedures (and related comments), what a particular procedure is supposed to do, without necessarily looking at the details of how it achieves its result. At the same time, a complete program is still imperative since it _fixes_ the statements to be executed and their order of execution to a large extent.

**Distinction from imperative programming**. Often, the terms "procedural programming" and "imperative programming" are used synonymously. However, procedural programming relies heavily on blocks and scope, whereas imperative programming as a whole may or may not have such features. As such, procedural languages generally use reserved words that act on blocks, such as if, while, and for, to implement control flow, whereas non-structured imperative languages use goto statements and branch tables for the same purpose.

**Relation to logic programming**: on [Wikipedia](https://en.wikipedia.org/wiki/Procedural_programming#Logic_programming)

---

## Functional programming

In computer science, **functional programming** is a programming paradigm where programs are constructed by applying and composing functions. It is a declarative programming paradigm in which function definitions are trees of expressions that **map values to other values**, rather than a sequence of imperative statements which update the running state of the program.

In functional programming, functions are treated as first-class citizens, meaning that they can be bound to names (including local identifiers), passed as arguments, and returned from other functions, just as any other data type can. This allows programs to be written in a declarative and composable style, where small functions are combined in a modular manner.

Functional programming (FP) has its roots in academia, evolving from the lambda calculus, a formal system of computation based only on functions. FP has historically been less popular than imperative programming, but many functional languages are seeing use today in industry and education, including Common Lisp, Scheme, Clojure, Wolfram Language, Racket, Erlang, Elixir, OCaml, Haskell, and F#.

Functional programming is also key to some languages that have found success in specific domains, like JavaScript in the Web, R in statistics, J, K and Q in financial analysis, and XQuery/XSLT for XML. Domain-specific declarative languages like SQL and Lex/Yacc use some elements of functional programming, such as not allowing mutable values. In addition, many other programming languages support programming in a functional style or have implemented features from functional programming, such as C++11, C#, Kotlin, Perl, PHP,  Python, Go, Rust, Raku, Scala, and Java (since Java 8).

The principles of modularity and code reuse in practical functional languages are fundamentally the same as in procedural languages, since they both stem from structured programming. So for example:
- Procedures correspond to functions. Both allow the reuse of the same code in various parts of the programs, and at various points of its execution.
- By the same token, procedure calls correspond to function application.
- Functions and their modularly separated from each other in the same manner, by the use of function arguments, return values and variable scopes.
- Functional programming languages support (and heavily use) first-class functions, anonymous functions and closures, although these concepts have also been included in procedural languages at least since Algol 68.

**The main difference between the styles is that functional programming languages remove or at least deemphasize the imperative elements of procedural programming.** The feature set of functional languages is therefore designed to support writing programs as much as possible in terms of pure functions.

### Purely functional programming

Functional programming is sometimes treated as synonymous with **purely functional programming**, a subset of functional programming which treats all functions as deterministic mathematical functions, or pure functions. When a pure function is called with some given arguments, it will always return the same result (deterministic), and cannot be affected by any mutable state or other side effects (pure). It is a style where all computation is treated as the evaluation of mathematical functions.

> Declarative, deterministic, and unchanging (immutability) are terms used to describe purely functional programming.

Purely functional programming consists of ensuring that functions, inside the functional paradigm, will only depend on their arguments, regardless of any global or local state. A pure functional subroutine only has visibility of changes of state represented by state variables included in its scope.

**Randomness and time functions are impure**, because they depend on the state of the system or the environment, which can change at any time. Moreover, they can also affect the state of the system or the environment, which can affect other functions.

> See also: [Pure Function](https://en.wikipedia.org/wiki/Pure_function)

This is in contrast with impure procedures, common in imperative programming, which can have side effects (such as modifying the program's state or taking input from a user). Proponents of purely functional programming claim that by restricting side effects, programs can have fewer bugs, be easier to debug and test, and be more suited to formal verification.

> The exact difference between pure and impure functional programming is a matter of controversy. Sabry, Amr (January 1993). "What is a purely functional language?". Journal of Functional Programming. 8 (1): 1–22 [DOI](https://www.cambridge.org/core/journals/journal-of-functional-programming/article/what-is-a-purely-functional-language/3A39D50DA48F628D17D9A768A1FA39C3)

### Concepts

A number of concepts and paradigms are specific to functional programming, and generally foreign to imperative programming (including object-oriented programming). However, programming languages often cater to several programming paradigms, so programmers using "mostly imperative" languages may have utilized some of these concepts.

**Higher-order functions** are functions that can either take other functions as arguments or return them as results. In calculus, an example of a higher-order function is the differential operator d/dx, which returns the derivative of a function f.

**Pure functions** (or expressions) have no side effects (memory or I/O). This means that pure functions have several useful properties, many of which can be used to optimize the code:
- If the result of a pure expression is not used, it can be removed without affecting other expressions.
- If a pure function is called with arguments that cause no side-effects, the result is constant with respect to that argument list. This can enable caching optimizations such as memoization.
- If there is no data dependency between two pure expressions, their order can be reversed, or they can be performed in parallel and they cannot interfere with one another (in other terms, the evaluation of any pure expression is [thread-safe](https://en.wikipedia.org/wiki/Thread-safe)). (does this apply to any two pure functions though?).
- If the entire language does not allow side-effects, then any evaluation strategy can be used; this gives the compiler freedom to reorder or combine the evaluation of expressions in a program (for example, using [deforestation](https://en.wikipedia.org/wiki/Deforestation_(computer_science) "Deforestation (computer science)")).

> **TODO: Check how pure functions are thread-safe.**

> While most compilers for imperative programming languages detect pure functions and perform common-subexpression elimination for pure function calls, they cannot always do this for pre-compiled libraries, which generally do not expose this information, thus preventing optimizations that involve those external functions. Some compilers, such as gcc, add extra keywords for a programmer to explicitly mark external functions as pure, to enable such optimizations. Fortran 95 also lets functions be designated pure. C++11 added `constexpr` keyword with similar semantics.

Iteration (looping) in functional languages is usually accomplished via recursion. Recursive functions invoke themselves, letting an operation be repeated until it reaches the base case. In general, recursion requires maintaining a stack, which consumes space in a linear amount to the depth of recursion. This could make recursion prohibitively expensive to use instead of imperative loops. However, a special form of recursion known as [tail recursion](https://en.wikipedia.org/wiki/Tail_recursion "Tail recursion") can be recognized and optimized by a compiler into the same code used to implement iteration in imperative languages. Common patterns of recursion can be abstracted away using higher-order functions, with [catamorphisms](https://en.wikipedia.org/wiki/Catamorphism "Catamorphism") and [anamorphisms](https://en.wikipedia.org/wiki/Anamorphism "Anamorphism") (or "folds" and "unfolds") being the most obvious examples. Such recursion schemes play a role analogous to built-in control structures such as loops in imperative languages.

**Strict versus non-strict evaluation**.

Functional languages can be categorized by whether they use _strict (eager)_ or _non-strict (lazy)_ evaluation, concepts that refer to how function arguments are processed when an expression is being evaluated. The technical difference is in the [denotational semantics](https://en.wikipedia.org/wiki/Denotational_semantics "Denotational semantics") of expressions containing failing or divergent computations. Under strict evaluation, the evaluation of any term containing a failing subterm fails. For example, the expression:

```python
print length([2+1, 3*2, 1/0, 5-4])
```

fails under strict evaluation because of the division by zero in the third element of the list. Under lazy evaluation, the length function returns the value 4 (i.e., the number of items in the list), since evaluating it does not attempt to evaluate the terms making up the list. In brief, strict evaluation always fully evaluates function arguments before invoking the function. Lazy evaluation does not evaluate function arguments unless their values are required to evaluate the function call itself.

The usual implementation strategy for lazy evaluation in functional languages is [graph reduction](https://en.wikipedia.org/wiki/Graph_reduction). Lazy evaluation is used by default in several pure functional languages, including Miranda, Clean, and Haskell.

> Main article: [Evaluation strategy](https://en.wikipedia.org/wiki/Evaluation_strategy)

**Referential transparency**.

Functional programs do not have assignment statements, that is, the value of a variable in a functional program never changes once defined. This eliminates any chances of side effects because any variable can be replaced with its actual value at any point of execution. So, functional programs are referentially transparent.

> Main article: [Referential transparency](https://en.wikipedia.org/wiki/Referential_transparency)

Related to FP: [total functional programming](https://en.wikipedia.org/wiki/Total_functional_programming "Total functional programming"), [type systems](https://en.wikipedia.org/wiki/Type_system), [functional logic programming](https://en.wikipedia.org/wiki/Functional_logic_programming), [logic programming](https://en.wikipedia.org/wiki/Logic_programming)

---

## Data-driven programming

In computer programming, **data-driven programming** is a programming paradigm in which the program statements describe the data to be matched and the processing required rather than defining a sequence of steps to be taken. Standard examples of data-driven languages are the text-processing languages sed and AWK, and the document transformation language XSLT, where the data is a sequence of lines in an input stream – these are thus also known as **line-oriented languages** – and pattern matching is primarily done via regular expressions or line numbers.

Data-driven programming is similar to event-driven programming, in that both are structured as pattern matching and resulting processing, and are usually implemented by a main loop, though they are typically applied to different domains.

---

## Object-Oriented programming

**Object-oriented programming** (OOP) is a programming paradigm based on the concept of objects, which can contain data and code: data in the form of fields / attributes / properties, and code in the form of procedures / methods. A common feature is the special name `this` or `self` which is used to refer to the current object and its fields or methods. OOP originates from MIT in the late 1950s and early 1960s.

> Related topic: Open recursion

The concept of Encapsulation is at the core of OOP. **Encapsulation** prevents external code from being concerned with the internal workings of an object. It achieves data abstraction. This facilitates code refactoring, for example allowing the author of the class to change how objects of that class represent their data internally without changing any external code (as long as "public" method calls work the same way). It also encourages programmers to put all the code that is concerned with a certain set of data in the same class, which organizes it for easy comprehension by other programmers. Encapsulation is a technique that encourages decoupling.

From Wikipedia:
- Languages called "pure" OO languages treat everything consistently as an object, from primitives such as characters and punctuation, all the way up to whole classes, prototypes, blocks, modules, etc. They were designed specifically to facilitate, even enforce, OO methods. Examples: Ruby, Scala, Smalltalk, Eiffel, Emerald, JADE, Self, Raku. [Read more](https://www.codingninjas.com/studio/library/is-java-an-object-oriented-language)
- Languages designed mainly for OO programming, but with some procedural elements. Examples: Java, Python, C++, C#, Delphi / Object Pascal, VB.NET.
- Languages that are historically procedural languages, but have been extended with some OO features. Examples: PHP, JavaScript, Perl, Visual Basic (derived from BASIC), MATLAB, COBOL 2002, Fortran 2003, ABAP, Ada 95, Pascal.
- Languages with most of the features of objects (classes, methods, inheritance), but in a distinctly original form. Examples: Oberon (Oberon-1 or Oberon-2).
- Languages with [abstract data type](https://en.wikipedia.org/wiki/Abstract_data_type "Abstract data type") support which may be used to resemble OO programming, but without all features of object-orientation. Examples: JavaScript, Lua, Modula-2, CLU.
- Chameleon languages that support multiple paradigms, including OO. [Tcl](https://en.wikipedia.org/wiki/Tcl "Tcl") stands out among these for TclOO, a hybrid object system that supports both prototype-based and class-based OO.

**Cohesion & OOP**

In OOP, if the methods that serve a class tend to be similar in many aspects, then the class is said to have high cohesion. Cohesion is increased if:
- The functionalities embedded in a class, accessed through its methods, have much in common.
- Methods carry out a small number of related activities, by _avoiding_ [coarsely grained](https://en.wikipedia.org/wiki/Granularity#Data_granularity "Granularity") or unrelated sets of data.
- Related methods are in the same source file or otherwise grouped together; for example, in separate files but in the same sub-directory/folder.

Advantages of high cohesion (or "strong cohesion") are:
- Reduced module complexity (they are simpler, having fewer operations).
- Increased system maintainability, because logical changes in the domain affect fewer modules, and because changes in one module require fewer changes in other modules. (Careful design and application of various principles leads to this)
- Increased module reusability, because application developers will find the component they need more easily among the cohesive set of operations provided by the module.

**Distinction from procedural programming**

The focus of procedural programming is to break down a programming task into a collection of variables, data structures, and subroutines, whereas in object-oriented programming it is to necessary break down a programming task into objects that expose behavior (methods) and data (members or attributes) using interfaces. The most important distinction is that while procedural programming uses procedures to operate on data structures, object-oriented programming bundles the two together, so an "object", which is an instance of a class, operates on its "own" data structure. Nomenclature varies between the two, although they have similar semantics:

|Procedural|Object-oriented|
|---|---|
|Procedure|Method|
|Record|Object|
|Module|Class|
|Procedure call|Message|

**Bonus**

Design Patterns: Elements of Reusable Object-Oriented Software is an influential book published in 1994 by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides, often referred to humorously as the "Gang of Four". Along with exploring the capabilities and pitfalls of object-oriented programming, it describes 23 common programming problems and patterns for solving them. Related guidelines are SOLID and GRASP.

> These will be multiple references to these terms from this point onward.

> **TODO: Create "Programming design patterns.md"**

Many of the most widely used programming languages (such as C++, Java, Python, etc.) are multi-paradigm and they support object-oriented programming to a greater or lesser degree, typically in combination with imperative, procedural programming.

Sourced from Wikipedia: Significant object-oriented languages include: Ada, ActionScript, C++, Common Lisp, C#, Dart, Eiffel, Fortran 2003, Haxe, Java, JavaScript, Kotlin, Logo, MATLAB, Objective-C, Object Pascal, Perl, PHP, Python, R, Raku, Ruby, Scala, SIMSCRIPT, Simula, Smalltalk, Swift, Vala and Visual Basic.NET.

> I didn't include any OOP examples as they can be easily found online in whichever programming language you might be learning.

### Class-based vs prototype-based

Two more specific programming paradigms exist that are based on OOP.

In **class-based languages** the _classes_ are defined beforehand and the _objects_ are instantiated based on the classes. If two objects _apple_ and _orange_ are instantiated from the class _Fruit_, they are inherently fruits and it is guaranteed that you may handle them in the same way; e.g. a programmer can expect the existence of the same attributes such as _color_ or _sugar_content_ or _is_ripe_.

In **prototype-based languages** the objects are the primary entities. No classes even exist. The prototype of an object is just another object to which the object is linked. Every object has one prototype link (and only one). New objects can be created based on already existing objects chosen as their prototype. You may call two different objects apple and orange a fruit, if the object fruit exists, and both apple and orange have fruit as their prototype. The idea of the fruit class does not exist explicitly, but as the equivalence class of the objects sharing the same prototype. The attributes and methods of the prototype are delegated to all the objects of the equivalence class defined by this prototype. The attributes and methods owned individually by the object may not be shared by other objects of the same equivalence class; e.g. the attribute *sugar_content* may be unexpectedly not present in apple. Only single inheritance can be implemented through the prototype.

> In a nutshell, behavior reuse is performed via a process of reusing existing objects that serve as prototypes (by cloning and extending). This model can also be known as prototypal, prototype-oriented, _classless, or instance-based programming.

Almost all prototype-based systems are based on interpreted and dynamically-typed languages.

Prototypal inheritance in JavaScript is described by Douglas Crockford as:

> You make prototype objects, and then … make new instances. Objects are mutable in JavaScript, so we can augment the new instances, giving them new fields and methods. These can then act as prototypes for even newer objects. We don't need classes to make lots of similar objects… Objects inherit from objects. What could be more object oriented than that?

Python supports both Class-based and prototype-based OOP.

In simpler words and using the fruit example, a "fruit" object would represent the properties and functionality of fruit in general. A "banana" object would be cloned from the "fruit" object and general properties specific to bananas would be appended. Each individual "banana" object would be cloned from the generic "banana" object. In a class-based scenario there would be a "banana" class extending the "fruit" class.

Most prototype-based systems enable the alteration of prototypes during runtime whereas few class-based OOP systems allow classes to be altered during the execution; namely Common Lisp, Dylan, Objective-C, Perl, Python, Ruby, or Smalltalk. These languages can be thought of supporting both*.

> *verification needed

### The getters setters debate

Getter and setter methods, also known as accessors, have been a subject of debate in the object-oriented programming community. While they are commonly used in languages like Java, there are arguments against their widespread use.

Two main points against getters and setters:
1. **Violation of Encapsulation**: Getter and setter methods provide external access to an object's internal state, violating the principle of encapsulation which aims to hide the internal state of an object and only allow controlled access to it. This leads to difficulties in maintaining the code.
2. **Tight Coupling or violation of loose coupling**: Changing the internal representation will affect the code that uses it. This makes flexible and maintainable code difficult, if not impossible.

Behavior-driven design, where the focus is on the behavior of objects rather than their state, is an alternative approach to relying heavily on getters and setters. Properties should also be used in languages that support them.

> **TODO: Add the concept of properties briefly**

Sources: InfoWorld [article](https://www.infoworld.com/article/2073723/why-getter-and-setter-methods-are-evil.html?page=2) by Allen Holub, Yegor Bugayenko, Marcus Biel

#### More on the topic from Allen Holub's column

> Note that a big part of this section has not been paraphrased at all. Credits go to Allen Holub.

##### On the nature of design

It's not an accident that every chapter in the Gang of Four's _Design Patterns_ book includes a "Consequences" section that describes when and why using a pattern is inappropriate.

> **TODO: Add a link here** when I finish the programming design patterns document

One basic principle of OO systems is data abstraction. You should completely hide the way in which an object implements a message handler from the rest of the program. **That's one reason why all of your instance variables (a class's non-constant fields) should be private**.

If you make an instance variable public, then you can't change the field as the class evolves over time because you would break the external code that uses the field. You don't want to search 1,000 uses of a class simply because you want to change that class.

Without implementation hiding, there's little point in using other OO features.

Accessor methods are dangerous for the same reason that public fields are dangerous: They provide external access to implementation details.

The lack of getter/setter methods doesn't mean that some data doesn't flow through the system. Nonetheless, it's best to minimize data movement as much as possible. My experience is that maintainability is inversely proportionate to the amount of data that moves between objects. Though you might not see how yet, you can actually eliminate most of this data movement.

***Don't ask for the information you need to do the work; ask the object that has the information to do the work for you.***

Most accessors find their way into code because the designers weren't thinking about the dynamic model: the runtime objects and the messages they send to one another to do the work. They start (incorrectly) by designing a class hierarchy and then try to shoehorn those classes into the dynamic model. This approach never works. **To build a static model, you need to discover the relationships between the classes, and these relationships exactly correspond to the message flow**. An association exists between two classes only when objects of one class send messages to objects of the other. The static model's main purpose is to capture this association information as you model dynamically.

Without a clearly defined dynamic model, you're only guessing how you will use a class's objects. Consequently, accessor methods often wind up in the model because you must provide as much access as possible since you can't predict whether or not you'll need it. This sort of design-by-guessing strategy is inefficient at best. You waste time writing useless methods (or adding unnecessary capabilities to the classes).

Accessors also end up in designs by force of habit. When procedural programmers adopt Java, they tend to start by building familiar code. Procedural languages don't have classes, but they do have the C `struct` (think: class without methods). It seems natural, then, to mimic a `struct` by building class definitions with virtually no methods and nothing but `public` fields. These procedural programmers read somewhere that fields should be `private`, however, so they make the fields `private` and supply `public` accessor methods. But they have only complicated the public access. They certainly haven't made the system object oriented.

> In a nutshell: The whole point of an abstraction layer is to isolate your business logic from a subsystem's mechanics.

##### When is an accessor okay?

It's okay for a method to return an object in terms of an interface that the object implements because that interface isolates you from changes to the implementing class. This sort of method (that returns an interface reference) is not really a "getter" in the sense of a method that just provides access to a field.

> **TODO: Find code examples for this case**

Next, I think of all OO systems as having a procedural boundary layer. The vast majority of OO programs runs on procedural operating systems and talks to procedural databases. The interfaces to these external procedural subsystems are generic by nature. Java Database Connectivity (JDBC) designers don't have a clue about what you'll do with the database, so the class design must be unfocused and highly flexible. Normally, unnecessary flexibility is bad, but in these boundary APIs, the extra flexibility is unavoidable. These boundary-layer classes are loaded with accessor methods simply because the designers have no choice.

In fact, this not-knowing-how-it-will-be-used problem infuses all Java packages. It's difficult to eliminate all the accessors if you can't predict how you will use the class's objects. Given this constraint, Java's designers did a good job hiding as much implementation as they could. This is not to say that the design decisions that went into JDBC and its ilk apply to your code. They don't. We _do_ know how we will use the classes, so you don't have to waste time building unnecessary flexibility.

##### A design strategy & CRC

The OO design process centers on use cases: a user performs standalone tasks that have some useful outcome. (Logging on is not a use case because it lacks a useful outcome in the problem domain. Drawing a paycheck is a use case). An OO system, then, implements the activities needed to play out the various scenarios that comprise a use case. The runtime objects that play out the use case do so by sending messages to one another. Not all messages are equal, however. **You haven't accomplished much if you've just built a procedural program that uses objects and classes**.

The CRC card is mentioned, which is relevant here. Class-responsibility-collaboration (CRC) cards are a brainstorming tool used in the design of object-oriented software. They were originally proposed by Ward Cunningham and Kent Beck as a teaching tool but are also popular among expert designers and recommended by extreme programming practitioners.

Brief explanation. CRC cards are usually created from index cards, meaning they're small and portable. Members of a brainstorming session will write one CRC card for each relevant class/object of their design. The card is partitioned into three areas:
1) The top for the class name
2) The left for the responsibilities of the class
3) The right for collaborators (other classes) with which the class interacts to fulfill its responsibilities.

Additionally, using small cards minimizes the complexity of the design, reduces class responsibilities and keeps designers focused on the essentials.

The classes then act out based on the following rules.
- Perform the activities that comprise the use case by talking to one another.
- You can only talk to your collaborators. If you must talk to someone else, you should talk to a collaborator who can talk to the other person. If that isn't possible, add a collaborator to your CRC card.
- You may not ask for the information you need to do something. Rather, you must ask the collaborator who has the information to do the work. It's okay to pass to that collaborator information he needs to do the work, **but keep this interaction to a minimum**.
- If something needs to be done and nobody can do it, create a new class (and CRC card) or add a responsibility to an existing class (and CRC card).
- If a CRC card gets too full, you must create another class (CRC card) to handle some of the responsibilities. Complexity is limited by what you can fit on a 4x6 index card.

The process Holub just described _is_ the OO design process, albeit simplified for a classroom environment. Some people design real programs this way using CRC cards. More often than not, however, designers develop the dynamic and static models in Unified Modeling Language (UML). The point is that an OO system is a conversation between objects. If you think about it for a moment, get/set methods just don't come up when you have a conversation. By the same token, get/set methods won't appear in your code if you design in this manner before you start coding.

##### Summing up

Let's pull everything together: You shouldn't use accessor methods (getters and setters) unless absolutely necessary because these methods expose information about how a class is implemented and as a consequence make your code harder to maintain. Sometimes get/set methods are unavoidable, but an experienced OO designer could probably eliminate 99 percent of the accessors currently in your code without much difficulty.

Getter/setter methods often make their way in code because the coder was thinking procedurally. The best way to break out of that procedural mindset is to think in terms of a conversation between objects that have well-defined responsibilities. Cunningham's CRC card approach is a great way to get started.

"Parts of this article are adapted from my forthcoming book, tentatively titled Holub on Patterns: Learning Design Patterns by Looking at Code, to be published by Apress (www.apress.com) this fall.

Allen Holub has worked in the computer industry since 1979. He currently works as a consultant, helping companies not squander money on software by providing advice to executives, training, and design-and-programming services. He's authored eight books, including Taming Java Threads (Apress, 2000) and Compiler Design in C (Pearson Higher Education, 1990), and teaches regularly for the University of California Berkeley Extension. Find more information on his Website (http://www.holub.com). This story, "Why getter and setter methods are evil" was originally published by JavaWorld.

> I felt a need to include the above as it is.

### Composition, inheritance, and delegation

Composition defines a has-a relationship; a car has wheels. In terms of code, we would have a Car class with fields of the Wheel class. Inheritance defines an is-a relationship; an apple is a fruit. In terms of code, we would have an Apple class that inherits all fields and methods from the Fruit class and possibly adding its own fields and methods. In inheritance, subclasses can override the methods defined by super-classes or parent-classes.

> **Important side note:** All methods are functions, but only those functions defined inside a class can be called methods.

Some languages, like Go do not support inheritance at all. In Java, the `final` keyword can be used to prevent a class from being sub-classed. Preventing sub-classing is a feature of some languages.

A term related to composition is aggregation. Composition defines a strong has-a relationship, while aggregation defines a weak has-a relationship. Given classes X, C and A, if X is composed of objects of type C, then we have composition and once the object of type X ceases to exist, its composite C objects are also deleted. By using aggregation, objects of class X would have **references** to objects of class A. Deleting a class X object wouldn't affect objects of class A as they're independent and would continue to exist in memory.

Modeling in UML is also relevant here. There are four ways of composing objects in UML: property, association, aggregation and composition. [UML on Wikipedia](https://en.wikipedia.org/wiki/Unified_Modeling_Language)

The "open/closed principle" advocates that classes and functions "should be open for extension, but closed for modification". This is one of the SOLID set of principles.

> **TODO: Add a link here** when I finish the programming design patterns document

#### Abstract classes

In a language that supports inheritance, an abstract class is a class that cannot be directly instantiated. Instantiation of an abstract class can occur only indirectly, via a concrete subclass. Abstract classes exist only to be inherited.

An abstract class is either labeled as such explicitly or it may simply specify abstract methods (aka virtual methods). An abstract class may provide implementations of some methods, and may also specify virtual methods via signatures that are to be implemented by direct or indirect descendants of the abstract class. In other words, before instantiating a class derived from an abstract class, all abstract methods of its parent classes must be implemented by some class in the derivation chain.

For example, in Java, C# and PHP, the keyword `abstract` is used. In C++, an abstract class is a class having at least one abstract method given by the appropriate syntax in that language (a pure virtual function in C++ parlance).

> In C++ there is the concept of a virtual function and a pure virtual function. A virtual function is a member function of a base class which _may or may not_ be overridden by a class in the derivation chain. This means that a virtual function defines code and may or may not be redefined by a derived class. A pure virtual function is a member function of a base class whose only declaration is provided (so, no code) and _should be defined_ in the derived class. In this case, the base class is called an abstract class. Additionally, if the derived class doesn't define the pure virtual function, it also becomes abstract.

A class consisting of only pure virtual methods is called a pure abstract base class (or pure ABC) in C++ and is essentially known as an interface. Such a class can only contain abstract publicly accessible methods. Other languages, notably Java and C#, support interfaces (a variant of ABCs) via a keyword in the language. In these languages, multiple inheritance is not allowed, but a class can implement multiple interfaces.

#### Multiple inheritance

**Multiple inheritance** is a feature of some object-oriented computer programming languages in which an object or class can inherit features from more than one parent object or parent class. It has been a controversial issue for many years with opponents pointing to its increased complexity and ambiguity in situations such as the "diamond problem".

The "diamond problem" (sometimes referred to as the "Deadly Diamond of Death") is an ambiguity that arises when two classes B and C inherit from A, and class D inherits from both B and C. If there is a method in A that B and C have overridden, and D does not override it, then which version of the method does D inherit: that of B, or that of C?  

Method lookup rules, also known as member lookup rules, are a feature in programming languages that allows for the resolution of method calls, particularly in the context of object-oriented programming. These rules help determine the appropriate method to execute when a message is sent to an object.

Languages have different ways of dealing with problems of repeated inheritance.
- C++ uses what is called virtual inheritance. Virtual inheritance prevents the same fields of class A to be duplicated in class D, in the context of the diamond problem.
- Python has the same structure as Perl, but, unlike Perl, includes it in the syntax of the language. The order of inheritance affects the class semantics. Python had to deal with this upon the introduction of new-style classes, all of which have a common ancestor, object. Python creates a list of classes using the [C3 linearization](https://en.wikipedia.org/wiki/C3_linearization) (or Method Resolution Order (MRO)) algorithm. That algorithm enforces two constraints: children precede their parents and if a class inherits from multiple classes, they are kept in the order specified in the tuple of the base classes (however in this case, some classes high in the inheritance graph may precede classes lower in the graph).

> I don't fully understand how this works in python so I might update this section in the future.

The diamond problem can be addressed in various ways (for languages, see [Mitigation](https://en.wikipedia.org/wiki/Multiple_inheritance#Mitigation) on Wikipedia), including alternate methods of object composition not based on inheritance such as **mixins** and **traits** that have been proposed.

##### Mixins

From [Mixin](https://en.wikipedia.org/wiki/Mixin) on Wikipedia: In object-oriented programming languages, a mixin (or mix-in) is a class that contains methods for use by other classes without having to be the parent class of those other classes. How those other classes gain access to the mixin's methods depends on the language. Mixins are sometimes described as being "included" rather than "inherited".

For example, class `UnicodeConversionMixin` might provide a method `unicode_to_ascii()` when included in class `FileReader` and class `WebPageScraper`, which do not share a common parent.

**A mixin can also be viewed as an interface with implemented methods**. This pattern is an example of enforcing the dependency inversion principle, which is part of the SOLID set of principles.

> **TODO: Add a link here** when I finish the programming design patterns document

Mixins allow inheritance and use of only the desired features from the parent "class".

> **TODO: Add more info on how particular features are chosen.** This is a feature of traits (see below)

In Python, an example of the mixin concept is found in the `SocketServer` module, which has both a `UDPServer` class and a `TCPServer` class. They act as servers for UDP and TCP socket servers, respectively. Additionally, there are two mixin classes: `ForkingMixIn` and `ThreadingMixIn`. Normally, all new connections are handled within the same process. By extending `TCPServer` with the `ThreadingMixIn` as follows:

```python
class ThreadingTCPServer(ThreadingMixIn, TCPServer):
    pass
```

The `ThreadingMixIn` class adds functionality to the TCP server such that each new connection creates a new thread. Using the same method, a `ThreadingUDPServer` can be created without having to duplicate the code in `ThreadingMixIn`. Alternatively, using the `ForkingMixIn` would cause the process to be forked for each new connection. Clearly, the functionality to create a new thread or fork a process is not terribly useful as a stand-alone class.

In this usage example, the mixins provide alternative underlying functionality without affecting the functionality as a socket server.

Languages that use mixins include: C#, MATLAB, Python, PHP's traits, Ruby, Scala, Swift, Java, JavaScript.

##### Traits

In computer programming, a trait is a concept used in programming languages which represents a set of methods that can be used to extend the functionality of a class.

The rationale. In object-oriented programming, behavior is sometimes shared between classes which are not related to each other. For example, many unrelated classes may have methods to serialize objects to JSON. Historically, there have been several approaches to solve this without duplicating the code in every class needing the behavior. Other approaches include multiple inheritance and mixins, but these have drawbacks: the behavior of the code may unexpectedly change if the order in which the mixins are applied is altered, or if new methods are added to the parent classes or mixins.

Traits solve these problems by allowing classes to use the trait and get the desired behavior. If a class uses more than one trait, the order in which the traits are used does not matter. The methods provided by the traits have direct access to the data of the class. Characteristics can be found on [Wikipedia](https://en.wikipedia.org/wiki/Trait_(computer_programming)#Characteristics).

> **TODO: Explore traits and how they could be simulated using mixins or interfaces.**

#### Delegation

In OOP, delegation refers to evaluating a member of one object (receiver or delegate) in the context of another object (sender or original). In other words, the delegate is a helper object that takes the responsibility of the original object, but with the original context. It is said that in object-oriented design, delegation uses composition to achieve the same code reuse as inheritance, i.e. with a delegation link.

> From the Introduction to Gamma et al. 1994: Delegation is a way to make composition as powerful for reuse as inheritance (Lie86, JZ91). Some sources complicate the definition by using the term 'receiver' which can refer to both the initial object that receives the request and the delegate object that handles it after it receives the request from the initial object. I hope that makes sense.

Inheritance is also described as 'implicit delegation' by using `self` which becomes evident in the example below. In the delegate pattern however, this is instead accomplished by explicitly passing the original object to the delegate (or a reference to it), as an argument to a method.

> Inheritance (or implicit delegation) makes use of the member lookup rules of the programming language by dispatching so-called [self-calls](https://en.wikipedia.org/w/index.php?title=Self-call&action=edit&redlink=1 "Self-call (page does not exist)") defined by [Lieberman](https://en.wikipedia.org/wiki/Henry_Lieberman "Henry Lieberman") in his 1986 paper "Using Prototypical Objects to Implement Shared Behavior in Object-Oriented Systems".
> In delegation the binding of `self` is characterized late, as it happens at 'evaluation time' which I assume means runtime. Source: [Delegation in OOP, Wikipedia](https://en.wikipedia.org/wiki/Delegation_(object-oriented_programming))
##### Delegation Example & Object schizophrenia

Calling `b.foo()` in both cases prints `b.bar`. The `this` keyword in the delegation example is described as ambiguous. The ambiguity disappears when using inheritance, in the second code snippet, thus making it more useful and desirable.

**Delegation**
```java
class A {
    void foo() {
        // "this" aka "current", "me" and "self" in other languages
        this.bar();
    }
    
    void bar() {
        print("a.bar");
    }
}

class B {
    private delegate A a; // delegation link
    
    public B(A a) {
    
        this.a = a;
    }
    
    void foo() {
        a.foo(); // call foo() on the a-instance
    }
    
    void bar() {
        print("b.bar");
    }
}

a = new A();
b = new B(a); // establish delegation between two objects
b.foo();
```

**Inheritance**
```java
class A {
    void foo() {
        this.bar();
    }
    void bar() {
        print("A.bar");
    }
}

class B extends A {
    public B() {}
    
    void foo() {
        super.foo(); // call foo() of the superclass (A)
    }
    
    void bar() {
        print("B.bar");
    }
}

b = new B();
b.foo();
```

**Object schizophrenia** or **self schizophrenia** is a complication arising from delegation and related techniques in OOP, where `self` / `this` can refer to more than one object.
##### Additional content on this topic

Check out this less theoretical and insightful post on SO: [What is a delegate in OOP](https://stackoverflow.com/questions/2044301/what-is-delegate)

A related concept is _forwarding_ where one sender-object simply uses a member of another receiver-object, evaluated in the context of the _receiver-object_. Forwarding is different from delegation and they particularly differ in the context used to evaluate a request from the sender-object.

The precise relationship between delegation and inheritance is complicated; some authors consider them equivalent, or one a special case of the other.

In the below excerpt from the Wikipedia article, a 'delegation link' is contrasted to an object reference. To me, this makes no sense, unless there's some implementation detail implied about the term 'object reference' thus making 'delegation link' more general, **but I'm not entirely sure**.

> In languages that support delegation via method lookup rules, method dispatching is defined the way it is defined for virtual methods in inheritance: It is always the most specific method that is chosen during method lookup. Hence it is the _original_ receiver entity that is the start of method lookup even though it has passed on control to some other object (through a delegation link, not an object reference).

I feel like the rest of the information in this section lacks ground so I included it purely as a pointer to more advanced details.

> Despite explicit delegation being fairly widespread, relatively few major programming languages implement delegation as an alternative model to inheritance.

> Delegation has the advantage that it can take place at run time and affect only a subset of entities of some type and can even be removed at run time. Inheritance, by contrast, typically targets the type rather than the instances, and is restricted to compile time. On the other hand, inheritance can be statically type-checked, while delegation generally cannot without generics (although a restricted version of delegation can be statically type-safe. [Wikipedia Citation](https://en.wikipedia.org/wiki/Delegation_(object-oriented_programming)#cite_note-8)).

### Polymorphism

In programming language theory and type theory, polymorphism is the use of a single symbol or a single interface to represent entities of different types.

The most commonly recognized major forms of polymorphism are:
- [Ad hoc polymorphism](https://en.wikipedia.org/wiki/Ad_hoc_polymorphism "Ad hoc polymorphism"): defines a common interface for an arbitrary set of individually specified types.
- [Parametric polymorphism](https://en.wikipedia.org/wiki/Parametric_polymorphism "Parametric polymorphism"): not specifying concrete types and instead use abstract symbols that can substitute for any type. A common example are templates in java: `List<String> x`. Related keywords are generics and templates.
- [Subtyping](https://en.wikipedia.org/wiki/Subtyping "Subtyping") (also called _subtype polymorphism_ or _inclusion polymorphism_): when a name denotes instances of many different classes related by some common superclass.
- Additional less known and interesting-sounding concepts include: Row polymorphism, Polytypism, Rank Polymorphism.

"**Ad-hoc polymorphism** is obtained when a function works, or appears to work, on several different types (which may not exhibit a common structure) and may behave in unrelated ways for each type." – [Christopher Strachey](https://en.wikipedia.org/wiki/Christopher_Strachey) 1967.

From [Strachey's Fundamental Concepts in Programming Languages of 1967](https://www.ics.uci.edu/%7Ejajones/INF102-S18/readings/05_stratchey_1967.pdf) 
> There seem to be two main classes (of polymporhpism), which can be called ad hoc polymorphism and parametric polymorphism ... In ad hoc polymorphism there is no single systematic way of determining the type of the result from the type of the arguments. There may be several rules of limited extent which reduce the number of cases, but these are themselves ad hoc both in scope and content ... Parametric polymorphism is more regular and may be illustrated by an example ...

> **TODO: Read the above source directly & update this section**

Examples include function overloading or operator overloading when we want to perform an addition operation whose implementation differs depending on the type. In dynamically typed languages the situation can be more complex as the correct function that needs to be invoked might only be determinable at run time. Implicit type conversion has also been defined as a form of polymorphism, referred to as "**coercion polymorphism**".

**Parametric polymorphism is a way to make a language more expressive while still maintaining full static type-safety**. Parametric polymorphism is ubiquitous in functional programming, where it is often simply referred to as "polymorphism". 

In subtyping code can be independent of which class in the supported hierarchy it is operating on – the parent class or one of its descendants. For example, objects of type Circle and Square are derived from a common class called Shape. The Draw function for each type of Shape implements what is necessary to draw itself while calling code can remain indifferent to the particular type of Shape being drawn. This is another type of abstraction that simplifies code external to the class hierarchy and enables strong separation of concerns.

> In a nutshell: The subtyping type of polymorphism most commonly seen in OOP is the process of adding detail to a general data type to create a more specific data type.

### Ad hoc vs Subtyping

From the following [StackExchange post](https://cs.stackexchange.com/questions/82485/is-subtype-polymorphism-a-kind-of-ad-hoc-polymorphism):

Strachey distinguished between **parametric** polymorphism, where there is no information about the actual type and _any_ type can be passed as an argument, and **ad hoc** where an arbitrary set of types has been nominated as acceptable. Subtyping is not parametric polymorphism because a specific type (the superclass) _is_ known. So the question is, is it ad-hoc?

The choice of the term **ad hoc** emphasizes that there need be no relationship between the different types in a given abstraction; the only unifying factor is the existence of concrete implementations that make them part of the set. Operator overloading and Haskell's type classes fit that criteria.

In contrast, subtyping requires a relationship between the subtypes and the supertype, one that allows subtypes to be used in place of the supertype. The currently-existing set of subtypes is only arbitrary in the sense that all code is arbitrary - being the set of code developers have chosen to write. While the implementation of each subtype can be entirely distinct and unique, the substitutability requirement means that inclusion in the set of acceptable types is principled and not ad hoc.

Another interesting read is [Polymorphism in Scala by BalmungSan](https://gist.github.com/BalmungSan/c19557030181c0dc36533f3de7d7abf4)

Duck typing is a related term, yet different from polymorphism. Polymorphism is a concept found on types, whereas duck typing is found on contracts. In polymorphism we encounter subclasses that inherit from a parent and override its methods. In the case of duck typing we instead create a new class with the same methods (so, methods have the same name) but different function; no subclassing involved. So, duck typing means code will simply accept any object that has a particular method. If a given object `animal` has the a `quack` method that we want to call, then we're good (no additional type requirements needed). It does not matter whether `animal` is actually a `Duck` or a different animal which also happens to quack. That's why it is called duck typing: if it looks like a duck then we can act as if that object is a duck).

The above is a mix of the answers provided in this [StackOverflow post](https://stackoverflow.com/questions/11502433/what-is-the-difference-between-polymorphism-and-duck-typing) about the difference between polymorphism and duck typing. Andy's answer is particularly insightful.

Another related term is the [structural type](https://en.wikipedia.org/wiki/Structural_type_system).

Another related term is the [type class](https://en.wikipedia.org/wiki/Type_class). Type classes seem to be related to polymorphism in the context of ad hoc polymorphism and specifically by adding constraints to type variables in parametrically polymorphic types. This allows functions and operators to be reused with many different types and have different behaviors depending on the instance of the type class.

While I don't have my mind fully (or even partly) wrapped around type classes, this [StackExchange post](https://cs.stackexchange.com/questions/129161/how-do-type-classes-make-ad-hoc-polymorphism-less-ad-hoc) has a couple useful links that I haven't yet explored.

> **TODO: Read on the above and expand this section**

### Behavioral subtyping

In object-oriented programming, **behavioral subtyping** is the principle that subclasses should satisfy the expectations of clients accessing subclass objects through references of superclass type, not just as regards syntactic safety (such as the absence of "method-not-found" errors) but also as regards _behavioral correctness_.

Behavioral subtyping is undecidable in general. Subtype polymorphism as enforced by the type checker in OOP languages (with mutable objects) cannot guarantee behavioral subtyping in any context. Class or object hierarchies must be carefully designed, considering possible incorrect uses that cannot be detected syntactically.

For example, both a Queue class and a Stack class have a put and a get method. A queue exhibits FIFO behavior, while a stack exhibits LIFO behavior. Clients accessing a Stack object through a reference of type Queue would expect FIFO behavior but observe LIFO behavior, invalidating these clients' correctness proofs and potentially leading to incorrect behavior of the program as a whole. In contrast, a program where both Stack and Queue are subclasses of a type Bag, whose specification for _get_ is merely that it removes _some_ element, does satisfy behavioral subtyping and allows clients to safely reason about correctness based on the presumed types of the objects they interact with. Indeed, any object that satisfies the Stack or Queue specification also satisfies the Bag specification.

This intuition that objects of a subclass can _safely_ substitute objects from the parent class is unfortunately false in most OOP languages, in particular in all those that allow mutable objects. Mutability leads to the violation of the expected behavior (citation needed). In a language with immutable objects, behavioral subtyping could work more effectively, as the state of the objects cannot be changed, ensuring that the expected behavior of the supertype is maintained.

The Liskov substitution principle, which is a fundamental concept in object-oriented programming, states that "if S is a subtype of T, then objects of type T in a program may be replaced with objects of type S without altering any of the desirable properties of that program". However, when mutable objects are involved, this substitution may lead to unexpected behavior, violating the principle.

> **TODO: Add a link here** when I finish the programming design patterns document

A study presented a model-theoretic analysis of correct behavioral subtyping for first-order, deterministic, abstract data types with immutable objects, indicating that behavioral subtyping could be effectively characterized in the context of immutable object. [Link to study](https://dr.lib.iastate.edu/entities/publication/289b6e26-fde7-4906-a118-00acdaf6567b/full) This study was found using Perplexity AI.

> **TODO: Read the study & expand this section.**

### Object-orientation and databases

Both OOP and relational database management systems (RDBMSs) are extremely common in software today. Since relational databases do not store objects directly (though some RDBMSs have OO features to approximate this), there is a general need to bridge the two worlds. The problem responsible for this bridging is known as **object-relational impedance mismatch**. The term originates from impedance matching in electrical engineering.

There's no general solution without downsides. One of the most common approaches is **object-relational mapping (ORM)**, as found in IDE languages such as Visual FoxPro and libraries such as Java Data Objects and Ruby on Rails' ActiveRecord. To clarify, the mismatch is not between OO and DBMSes. Object-relational impedance mismatch is eponymously only between OO and **R**DBMSes. Alternatives like NoSQL or XML databases don't have this problem. More on [Minimization in OO here](https://en.wikipedia.org/wiki/Object%E2%80%93relational_impedance_mismatch#Minimization_in_OO).

Object databases, which have been considered since the early 1980s, are different from (table-oriented) relational databases. An object database is also referred to as an OO data store or OO database (or OODB I guess).

> **TODO**: See how these 'object databases' are different from other types of DBs.

A third type, **object–relational databases (ORD)**, is the hybrid of both approaches mentioned earlier. An OODB model allows containers like sets and lists, arbitrary user-defined datatypes as well as nested objects. The info on Wikipedia makes these concepts a bit confusing, so more insight is definitely welcome.

"These alternative solutions have not been as technically and commercially successful as RDBMSs."

### Object-relational mapping

**Object–relational mapping** (**ORM**, **O/RM**, and **O/R mapping** tool) in computer science is a programming technique for converting data between a relational database and the heap of an object-oriented programming language.

Object–relational mapping provides automated support for mapping tuples to objects and back, while accounting for all of these differences. For example, consider an address book entry that represents a single person along with zero or more phone numbers and zero or more addresses. This could be modeled in an object-oriented implementation by a "Person object" with an attribute/field to hold each data item that the entry comprises: the person's name, a list of phone numbers, and a list of addresses. The list of phone numbers would itself contain "PhoneNumber objects" and so on. Each such address-book entry is treated as a single object by the programming language (it can be referenced by a single variable containing a pointer to the object, for instance). By contrast, relational databases, such as SQL, group scalars into tuples, which are then enumerated in tables. Tuples and objects have some general similarity, in that they are both ways to collect values into named fields such that the whole collection can be manipulated as a single compound entity. They have many differences, though, in particular:
- lifecycle management (row insertion and deletion, versus garbage collection or reference counting)
- references to other entities (object references, versus foreign key references)
- inheritance (non-existent in relational databases)
- and objects being managed on-heap, under the full control of a single process, while database tuples being shared, having to incorporate locking, merging, and retry

The heart of the problem involves translating the logical representation of the objects into an atomized form that is capable of being stored in the database while preserving the properties of the objects and their relationships so that they can be reloaded as objects when needed. If this storage and retrieval functionality is implemented, the objects are said to be **persistent**.

Disadvantages of ORM tools generally stem from the high level of abstraction obscuring what is actually happening in the implementation code. Also, heavy reliance on ORM software has been cited as a major factor in producing poorly designed databases.

> **TODO: This latter point needs some elaborating.**

An alternative to implementing ORM is to make use of the native procedural languages provided with every major database. These can be called from the client using SQL statements. The [Data Access Object](https://en.wikipedia.org/wiki/Data_access_object "Data access object") (DAO) design pattern is used to abstract these statements and offer a lightweight object-oriented interface to the rest of the application.

More formally, in software, a **data access object** is a pattern that provides an abstract interface to some type of database or other persistence mechanism. By mapping application calls to the persistence layer, the DAO provides data operations without exposing database details. This isolation supports the single responsibility principle. In a few words, it achieves abstraction; changing business logic can rely on a constant DAO interface, while changes to persistence logic do not affect DAO clients.

I think the "persistence layer" can also be termed as "data access layer".

> **TODO: Add a link here** when I finish the programming design patterns document

Potential disadvantages of using DAO include [leaky abstraction](https://en.wikipedia.org/wiki/Leaky_abstraction), code duplication, and [abstraction inversion](https://en.wikipedia.org/wiki/Abstraction_inversion). In particular, the abstraction of the DAO as a regular Java object can obscure the high cost of each database access. Developers may inadvertently make multiple database queries to retrieve information that could be returned in a single operation. If an application requires multiple DAOs, the same create, read, update, and delete code may have to be written for each DAO.

More alternatives to implementing ORM include OODBMS and **document-oriented databases** (such as native XML databases that provide more flexibility in data modeling). The equivalent of ORMs for document-oriented databases are called **object-document mappers (ODMs)**. Document-oriented databases also prevent the user from having to "shred" objects into table rows. Many of these systems also support the XQuery query language to retrieve datasets.

To get a better understanding, I read the following 2 sections on:
- ORM, DAO and DTO
- Document-oriented database

#### ORM, DAO and DTO

I've noticed the terms ORM, DAO and DTO used together while reading about ORMs, which confused me at first. A DTO (Data Transfer Object) is an object used for transferring data, generally from the controller to the client/application.

[From this SO post](https://stackoverflow.com/questions/4037251/dao-vs-ormhibernate-pattern) "ORM and DAO are orthogonal concepts. One has to do with how objects are mapped to database tables while the other is a design pattern for writing objects that access data. You don't choose 'between' them. You can have ORM and DAO in the same application, just as you don't need ORM to use the DAO pattern."

[From this reddit post](https://www.reddit.com/r/learnprogramming/comments/183mhe8/can_it_be_said_that_dao_or_data_access_object_is/) and in looser terms "A DAO is a very simple thing, it performs an operation on the database and returns a dataset when applicable, no mapping, no tracking, no magic. An ORM on the other hand is usually a library that does everything an DAO does and a lot more, including mapping, tracking and magic." DTO seems to be a Java term, although I'm unsure if _strictly_, and Oracle could've explained it better.

Another insightful [SO post](https://stackoverflow.com/questions/37644957/what-is-the-difference-between-dal-dto-and-dao-in-a-3-tier-architecture-style-i) talks about DAL (Data Access Layer), DTO, DAO and MVC.

#### Document-Oriented database

A [document-oriented database](https://en.wikipedia.org/wiki/Document-oriented_database) or **document store**, is a computer program and data storage system designed for storing, retrieving and managing document-oriented information, also known as semi-structured data. Document-oriented databases are one of the main categories of NoSQL databases. The popularity of the term "document-oriented database" has grown with the use of the term NoSQL itself.

The central concept of a document-oriented database is the notion of a _document_. While each document-oriented database implementation differs on the details of this definition, in general, they all assume documents encapsulate and encode data (or information) in some standard format or encoding. Encodings in use include [XML](https://en.wikipedia.org/wiki/XML "XML"), [YAML](https://en.wikipedia.org/wiki/YAML "YAML"), [JSON](https://en.wikipedia.org/wiki/JSON "JSON"), as well as binary forms like [BSON](https://en.wikipedia.org/wiki/BSON "BSON").

[XML databases](https://en.wikipedia.org/wiki/XML_database "XML database") are a subclass of document-oriented databases that are optimized to work with [XML](https://en.wikipedia.org/wiki/XML "XML") documents. [Graph databases](https://en.wikipedia.org/wiki/Graph_databases "Graph databases") are similar, but add another layer, the _relationship_, which allows them to link documents for rapid traversal. Document-oriented databases are inherently a subclass of the [key-value store](https://en.wikipedia.org/wiki/Key-value_database "Key-value database"), another NoSQL database concept.

Main article [on Wikipedia](https://en.wikipedia.org/wiki/Document-oriented_database)

> **TODO: Expand on this section.**

### Responsibility- vs. data-driven design

**Responsibility-driven design** defines classes in terms of a contract, that is, a class should be defined around a responsibility and the information that it shares. This is contrasted by Wirfs-Brock and Wilkerson with **data-driven design**, where classes are defined around the data-structures that must be held. The authors hold that responsibility-driven design is preferable.

Note that there is only a data-driven _programming_ article on Wikipedia. "Data-driven design is not the same as data-driven programming, which is concerned with using data to determine the control flow, not class design." The above paragraph in the OOP article writes data-driven _design_ but links to the data-driven _programming_ article. **Kinda fishy**.

Concerning classes, data-driven design is about designing your classes while first taking into consideration the the data structure and format used by messages that the classes send to each other.

> This last part isn't made clear so far. More info needed on data-driven design.

#### Responsibility-driven design

Main article [on Wikipedia](https://en.wikipedia.org/wiki/Responsibility-driven_design)

Responsibility-driven design is a design technique in OOP, which focuses on the objects as behavioral abstractions which are characterized by their responsibilities. It considers the actions that the object is responsible for and the information that the object shares, or simply put; the contract. It was proposed by Rebecca Wirfs-Brock and Brian Wilkerson.

The client-server model is used for the interaction between two classes or class instances and as long as requests are carried out according to a known specification, encapsulation can be increased and therefore improved. Another benefit is grouping classes together based on their clients, which is more evident when using CRC cards. The CRC-card modelling technique is used to generate the behavioral abstractions of classes while the rest of the object structure is assigned later, as and when required.

> To further the encapsulation of the server, Wirfs-Brock and Wilkerson call for language features that limit outside influence to the behavior of a class. They demand that the visibility of members and functions should be finely grained, such as in THE Eiffel programming language. Even finer control of the visibility of even classes is available in the Newspeak programming language.

A good object-oriented design involves an early focus on behaviors to realize the capabilities meeting the stated requirements and a late binding of implementation details to the requirements. This approach especially helps to decentralize control and distribute system behavior which can help manage the complexities of high-functionality large or distributed systems. Similarly, it can help to design and maintain explanation facilities for [cognitive models](https://en.wikipedia.org/wiki/Cognitive_model "Cognitive model"), [intelligent agents](https://en.wikipedia.org/wiki/Intelligent_agent "Intelligent agent"), and other [knowledge-based systems](https://en.wikipedia.org/wiki/Knowledge-based_systems).

### Criticism (OOP)

From the [OOP Wikipedia article](https://en.wikipedia.org/wiki/Object-oriented_programming#Criticism) and without any bias, I found the following interesting:

This

> For example, the [circle-ellipse problem](https://en.wikipedia.org/wiki/Circle-ellipse_problem "Circle-ellipse problem") is difficult to handle using OOP's concept of [inheritance](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming) "Inheritance (object-oriented programming)").

and

> However, [Niklaus Wirth](https://en.wikipedia.org/wiki/Niklaus_Wirth "Niklaus Wirth") (who popularized the adage now known as [Wirth's law](https://en.wikipedia.org/wiki/Wirth%27s_law "Wirth's law"): "Software is getting slower more rapidly than hardware becomes faster") said of OOP in his paper, "Good Ideas through the Looking Glass", "This paradigm closely reflects the structure of systems 'in the real world', and it is therefore well suited to model complex systems with complex behaviours" (contrast [KISS principle](https://en.wikipedia.org/wiki/KISS_principle "KISS principle")).

and 

> [Steve Yegge](https://en.wikipedia.org/wiki/Steve_Yegge "Steve Yegge") and others noted that natural languages lack the OOP approach of strictly prioritizing _things_ (objects/nouns before _actions_ (methods/verbs). This problem may cause OOP to suffer more convoluted solutions than procedural programming.

---

## Probabilistic Programming

**Probabilistic programming** (PP) is a programming paradigm in which probabilistic models are specified and inference for these models is performed automatically. It represents an attempt to unify probabilistic modeling and traditional general purpose programming in order to make the former easier and more widely applicable. It can be used to create systems that help make decisions in the face of uncertainty.

Probabilistic reasoning has been used for predicting stock prices, recommending movies, diagnosing computers, detecting cyber intrusions and image detection. The Gen probabilistic programming library (written in Julia) has been applied to vision and robotics tasks. Probabilistic programming languages are also commonly used in Bayesian cognitive science to develop and evaluate models of cognition.

PPLs often extend from a basic language. The choice of underlying basic language depends on the similarity of the model to the basic language's ontology, as well as commercial considerations and personal preference. For instance, Dimple and Chimple are based on Java, Infer.NET is based on .NET Framework, while PRISM extends from Prolog. However, some PPLs such as WinBUGS offer a self-contained language, that maps closely to the mathematical representation of the statistical models, with no obvious origin in another programming language. The language for winBUGS was implemented to perform Bayesian computation using Gibbs Sampling (and related algorithms). A probabilistic relational programming language (PRPL) is a PPL specially designed to describe and infer with probabilistic relational models (PRMs). PPL List on [Wikipedia](https://en.wikipedia.org/wiki/Probabilistic_programming)

> This last paradigm doesn't feel as detailed as I hoped it would be, but if I had to keep expanding this document it'd be a low priority.
