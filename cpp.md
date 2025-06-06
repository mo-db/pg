# setup
- x86-64 Debian Utm -> for valgrind, gdb, testing
  - setup git and ssh
- able to compile c, cc, asm with make

# Libraries
- in posix librariy names have to start with `lib`
- static:
  - `ar r libExample.a file1.o file2.o` -> somewhat like a compressed zip
  - `ranlib libExample.a` -> indexes the functions so they can be used
  - `-L. -lExample` search for the example lib in current dir
- dynamic:

# Compilation and Build process
- use shell -> use make -> use cmake
- give a compiler all source files without flags
- `-c` just compile without linking
- Makefile.am -> `automake` -> Makefile.in -> `configure` -> Makefile

## Keywords [https://en.cppreference.com/w/cpp/keyword]
- `extern` -> declare something that is outside the current `uebersetzungseinheit`
  so not int the header or a same named source but in a library or such
  - `erno` is a global posix variable, to use it it has to be declared as extern
- `operator`
  - `user-defined literal` -> like a function but uses a literal as identifier
  - `operator overloading`


## Object
- data and action associated
- size, type, allignment, storage duration, lifetime, value, name

## Funciton
- collection of statements

## Statement
- ends in ;
- can compile into many machine lang instructions
- Types:
    Declaration statements
    Jump statements
    Expression statements
    Compound statements
    Selection statements (conditionals)
    Iteration statements (loops)
    Try blocks

## Containers [https://en.cppreference.com/w/cpp/container]
- containers are `homogeniouse`
- implemneted as `class templates`
- if something is called container, it fullfills the requirements here:
  [https://en.cppreference.com/w/cpp/named_req/Container]
- C++ array data types:
  - (`C-Style array`) no c++ container
  - `std::vector`, most flexible
  - `std::array`, more limited than vector, but more performant

## Classes
- virtual function
- friend functions/classes have access to private members
- const member functions can be called even with non-const values

## initialization [https://www.learncpp.com/cpp-tutorial/variable-assignment-and-initialization/]
- types of initialization:
  - default: `int x;`
  - copy: `int x = 5;`, great since c++17
  - direct: `int x ( 5 );`, used for some explicit things
  - list: `int x { 5 };`, modern, used with std::vector, does not allow
    narrow conversion:
    - compiler error if try to init value that variable can not 
      savely hold -> initializing an int with a floating point number
  - value: `int x {};`, list 0 initialization 

# Debugging & Errors
- Segfaults are good
- `-fsanitize=address` is as good as valgrind
- `-DNDEBUG` takes all asserts out of executable
  - so `assert(do_stsuff() == true)` is not ok

# Compiler, runtime, compile-time
## Optimization
- turnd off by default for better debugging
- `profiler` to check time neede for functions
- `optimizer` enhances code, example: i = i * 2; into i <<= 1;
  - modern C++ compilers have builtin optimizers 
  - `as-if-rule`: compiler can refactor to optimize code however it wants,
    but observed behavour of the code must remain unchanged
  - `compile-time evaluation` of expressions = performance increase
    - `constant folding` replace (3+4) with 7
    - `constant propagation` replaces variables with their constant values
      if they not change trough the programm to not have to access memory
      - so constant variables help the compiler to optimize better
    - `dead code elimination` removes unused code
## runtime, compile-time
- `compile-time debugging` is underdeveloped in C++
- `compile-time constants`: const int b { 5 }; const int d { b };
  - literals
  - objects with compile-time initializer constants
- `runtime constants`: int a { 5 }, const int e { a }; const int f { e };
                        const int g { five() };
  - constant function parameters
  - objects with non-constant or runtime constant initializers


# Identifiers and Names
- start with a-zA-z_

# Utilities library [https://en.cppreference.com/w/cpp/utility]
## Function Object - functor
- function with state - functions are normally not objects

# I/O library [https://en.cppreference.com/w/cpp/io]
## basic_ios
- facilities to interface with `std::basic_streambuf` objects
## basic_ostream [https://en.cppreference.com/w/cpp/io/basic_ostream]
- cout, cerr, clog
## basic_istream [https://en.cppreference.com/w/cpp/io/basic_istream]
- cin

# Facts
- C: `call by value` -> objects are copied in and out of scopes
- C: `argv[argc] = 0`, `argv[argc+n]` -> environment information
- a pointer with value 0 is `nullptr (NULL)`
  - `*(int *)0 = 0;` is a nullptr dereference -> segfaults
- C has printf < C++ iostream < std::format < std:print < fmt (lib)
- dont use malloc() and free() in C++
- `\r` is carriage return, gets to start of line
- `literals (literal constants)` are fixed values int the executable
  while `variables` are placed into memeory
- `implicit` (automatically by the language/compiler) -> type promotion
- `explicit` (intentionally coded by the programmer) -> type cast
- `%` opperator not math like for negative numbers: -21 % 4 = 1
- `$?` -> result of last terminated process
- non-primitive datatypes can be `casted` -> one struct casted into another
- `rosa einhorn` u8"\U0001f984" -> gibt einen Punkt in der Klausur
- character literals that represent decimals follow directly after another
  - for other character literals this is dependent on the encoding
  - so `a + 1 = b` not necessarily true

# Recursion
- recursive function stack: `ulimit -s` 8mb, `ulimit -s unlimited`
- ever recursion problem can be solved iteractive (for/while)
  - for non-trivial problems recursion can be simpler to write and read
  - fibonacci for example -> `EX` try iteractive and recursive fibonacci 

# Unix commands
- locate, same as `find /path -name <name>` but can prebuild

# Need to learn about
- STL containers
- iterators, containers and algorithms
- templates, generics (function and class templates)

# [https://www.learncpp.com/] readlist
## 01 - Basics
- 01: rev
  - `statements` -> instructions, can be executed by the program, end in `;`
    - declaration, jump, expression, compound, selection, iteration, try block
  - `function` -> collection of statements
- 10: rev
  - `expression` -> non-empty sequence of literals, variables, operators and
    function calls that `evaluates` (gets executed) into `result`
## 05 - Constants and Strings
- 04: !rev
  - compiler has built in `optimizer`, that operates after the `as-if-rule`
  - `compile-time evaluation`
    - contant folding, constant propagation, dead-code elimination, ...
  - `compile-time vs runtime`
- 05: !rev
  - `compile-time programming` -> using language features that result in
    compile-time evaluation of code -> need constant expressions
    - constexpr variables, constexpr functions, templates, static_assert, ...
  - `constant expression` -> contains only compile-time constants
    - can not be used in constant expression:
      - non-const variables, const non-integral variables (use constexpr),
        return values of non-constexpr functions, function parameters,
        new, delete, throw, typeid
    - if no constant expression is required in a specific context,
      compiler `must not evaluate at compile-time`
- 06: !rev
  - c styele `const` -> difficult to tell if var is constant in some situations
    - only use if initializer is not a constant to indicate variable not change
  - `constexpr` is always a compile time constant
    - initializer must be a constant expression -> else compilation error
    - function parameters of normal functions cannot be constexpr

## 07 - Scope, Duration and Linking
- 14: !rev
- ADD:
  - namespaces can be used for custom `type suffixes` -> _feet in meter

## 09 - Debugging and Errors - check
- 01: rev
- 02: !rev
  - `code coverage`: state, branch, loop, ...
- 03: rev
- 04: rev
  - C++ has `exceptions` that can be cached but terminate when reach main
- 05: rev
- 06: !rev
  - `static_assert` to trigger assert at compile-time

## 19 - Dynamic Memory Management
- 01: !rev
  - 

## 11 - Function Overloading and Class Templates
- 01: rev
  - `overloading` -> name identical functions with diffent parameter types
- 02: rev
  - `differentiation` based on number of parameters, types of parameters.
    The return type doesn't matter here.
- 03: !rev
  - compiler does `overload resolution`
  - `ambigious function call` -> compiler cant differentiate
- 04: !rev
  - define function as `deleted` if it should not be callable with a specific
    combination of types
  - `deleted function templated` to make a function only callable with 
    the specific type that is defined
- 05: !rev
  - `default argument` is used if caller provides no argument
- 06: !rev
  - compiler uses `template` to `generate overloaded functions`
  - templates can use `placeholder types`
  - templates can work with `types that did not exist` when template was written
  - declaration: `template <typename T>`
- 07: !rev
  - calling: `some_function<actual_type>(arg1, arg2);`
  - functions `instanciated` from a template are called `specialization` or
    `instanciated functions` and this template is the `primary template`
  - can use template argument deduction `some_function<>(arg1, arg2)`
    or even `some_function(arg1, arg2)`
  - template functions can have `non-template parameters`
  - template usage is called `generic programming`

## 28 - I/O [https://en.cppreference.com/w/cpp/io/manip]
- 01: !rev
  - `std::cout` and `std::cin` use stdin and stdout under the hood
  - `stream` -> sequence of bytes that can be accesed in sequence
  - classes:
    - istream, ostream, iostream, standard stream (cin, cout, cerr, clog)
- 02: !rev
  - `<<, >>` operator skip whitepaces

# Screen Casts PG2
- 31.03:
[https://en.cppreference.com/w/cpp/language/operators]
[https://en.cppreference.com/w/cpp/language/user_literal#Literal_operators]
  - 0:10 `overloading`
    - `operator` used like function but in place of identifier is a symbol
    - `"hello" + "world"` works because + operator is overloaded
    - string literale enden auf '\0'
    - unix right management are just octal numbers: 7 = 0b111
    - `inter/float literale` sind `unsigned`: -1 negiert 1 mit dem - operator
    - `nullptr` als parameter von überladener funktion -> wie C: if (var == NULL)
    - `declare` vs `declare and define`
    - `declaration` is compile-time, definition has a role in run-time
    - datentyp ist `nicht primitiv` -> mehrere Komponenten
    - innerhalb `< >` compile-time, also nur Konstanten erlaubt
- 03.04:
[https://en.cppreference.com/w/cpp/language/reference]
  - 0:02 - reference
    - `&` address operator, type identifier operator
    - `&` `reference parameter`, change the mode of `parameter transfer`
    - `using` (compile-time) is similar to `typedef` (run-time)
    - `objects` are run-time constructs and classes are compile-time types
    - bei `&` referencen beziehen wir uns nicht auf speicheradressen
  - 1:05 - tipps fuer ostern uebung
    - `lvalue reference` == alias, funktioniert wie pointer aber besser zu handeln
    - referenzen sind compile-time, belegen `keinen speicher` zur laufzeit
    - `rvalue reference` etwas was rechts vom = steht
    - referenzen haben keine adresse zur laufzeit
    - `int *&ir = &var` is a reference of a pointer
    - functionen returnen rvalues, als referenz koennen diese dennoch geaendert werden
    - referenz ist ein `unveraenderlicher pointer`
    - muss bei der vereinbarung initialisiert werden
  - [EX]
    - `-frtti` -> runtime type informations, off by default
    - `OpCode`
- 07.04
  - 0:00 reference
    - `int &func(int&);` returns a lvalue, `func(int&) += 5` is thus possible
  - 0:42 - enum
    - enums are compile-time constructs, reserve no run-time memory
    - c++ enum class is type save
    - `enum struct` get value with scope operator `struct::thing1` namespace
    - alias definitions with `using` and `typedef`
  - 1:05 - objektorientierung
    - data saved in `member variables` describe the `state` of an object
    - objects are `statefull` - zustandbehaftet
    - `encapsilation` -> allows to can change the `implementation` 
      while the `interface` stays the same
    - c++ strcut can contain `function with body`, and be used without keyword
    - `extern` -> declare something global without reserving stack memory
    - `inline` -> allows more than one definition
    - `const pointer` -> deref. value cannot be change
- 10.04 
  - 0:00 - const
    - `const int *p` or `int const *p` prevents the value from changing
    - `int *const p` prevents the pointer from changing
    - not constant reference to constant variable is error
  - 0:18 - (volatile) - braucht man fast nie
    - mark that a variable can be changed from another process, is not stable
      - prevents compiler from optimizing the memory calls away
    - `setjump` jump from process into operating system -> `nonlocal goto`
      -> `hardware exceptions`
    - `setjump(catchPos)` -> catch position saves the state of the process
    - `longjump` jumps back to local process
    - `longjump(catchPos, failVal)`
  - 0:46 - `trailing return` of functions
  - 1:00 - operators
  [https://www.learncpp.com/cpp-tutorial/overloading-the-comparison-operators/]
    - `<=>` space ship operator -> overloading comparison operator [!rev]
      [https://en.cppreference.com/w/cpp/language/operator_member_access]
    - `int ds::*ip;` defines pointer ip that can only point to members the namespace
      variables of the object ds
    - `i2.*ip;` access member variable of an object instance 
      with the namespace pointer ip
    - `ds::*ip = &ds::b;`
- 14.04
  - !REV spaceship operator
  - `struct s;` `s da { 3, 4 }, db ( 6, 7 };`
  - `for each` schleife for (int &x : array) {;}
- 24.04
  - for bool `proxy iterator` `&&` because bool is packed in containers
  - c++ containers can be returned from function scope -> `Copy-elision`
  - for classes we differentiate `implementation` and `interface`
  - 3 levels of class visibility: `public`, `private`, `protected`
  - classes are blueprints for objects
  - at runtime there exist only objects, no classes
  - defintion of member functions outside of class with ::

