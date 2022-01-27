---
title: Coding Style
layout: default

parent: Developers
nav_order: 2
---

This document provides the general coding guidelines for C++ code in the OpenSpace project.  The guidelines are based on these [guidelines](http://geosoft.no/development/cppstyle.html), but were adapted and modified.  Following this document ensures a common coding style for the project.  Each developer using their own guidelines will quickly lead to fragmented code and decrease readability and maintainability.  Please note rule #1; if, in a specific situation, the application of a rule would make the source code less readable it is advised to not follow the rule.

Sections [A](#general), [B](#naming), and [C](#structure) contain the coding style rules.  Section [D](#best-practices) contains broader best practices for coding in general, and Section [E](#file-formatting) contains rules and examples on how to format the files in order to be consistent with the rest of the code base.

# General
## 1. Violations to the guidelines are allowed if it enhances readability of the code
The main goal of these guidelines is to improve readability and thereby the understanding, the maintainability, and general quality of the code.  It is impossible to cover all the specific cases in a general guide and the programmer should be flexible.  However, the guidelines should be followed as closely as possible without sacrificing readability.

## 2. Class and method headers must include Doxygen-style comments
 It is important to document the header so that other people do not need to dive into the code to understand the API.
 
## 3. File content must be kept within 90 columns
90 columns on a moderate font size allows two source files to be opened side-by-side.  Sticking to a fixed, manually enforced linebreak improves readability when unintentional line breaks are avoided when passing files between programmers.  See examples below on how to handle lines that are longer than 90 characters

## 4. All TABs must be 4 spaces
TABs can be handled differently on different operating systems and make it hard to correctly format code.  Most editors have settings that will automatically convert TABs to spaces

## 5. Use the `auto` keyword sparingly
The overuse of `auto` in the code can make the code much harder to understand.  If the return type of a function is known, the `auto` keyword must not be used unless the type is very verbose.  The only every-day location where `auto` would be necessary is generic lambdas or shorthand for iterator types.

## 6. Use `//` for all comments, including multi-line comments
Using `//` comments ensure that it is always possible to comment out entire sections of a file using /\* \*/ for debugging purposes etc.  Please note that his rule does not apply to the Doxygen comments in the header, as we use the variant that starts with `/**`

# Naming
## 7. Negated boolean variable names should be avoided
```cpp
bool isError; // NOT: isNoError
bool isFound; // NOT: isNotFound
```
The problem arises when such a name is used in conjunction with the logical negation operator as this results in a double negative.  It is not immediately apparent what `isNotFound` means. Leaving the code as simple as possible enhances readability.

## 8. Enumerations must not be in upper case and should be strongly typed
If there is no inherent mapping to integer types, the first value should be manually set to be equal to 0.  If possible, prefer strongly typed enumerations for type safety. Setting the first value to 0 will force the values to be consecutive integers and therefore any switch statement will be very efficient.  Strongly typed enumerations will prevent easy misuse in client code.  If a strongly typed enumeration is not possible (due to mixing with outside code, each enumerated type should contain the enum name as a prefix.
```cpp
enum Color {
    ColorRed = 0,
    ColorGreen,
    ...
}
enum class Color {
    Red = 0,
    Green,
    ...
}
```

This makes it easy to find values for that type as the code completion of any IDE will suggest when typing the initial name.  Strongly typed `enum`s are preferred as they are placed into their own namespace and do not collide with other definitions.

## 9. Names for methods or functions must be verbs and written in CamelCase starting with lower case
Methods should be named in such a way that, if applied to a properly named variable, it makes as much grammatical sense as possible.  If two methods only differ in the fact that one will return a modified copy while the other changes and object in-place, the passive and active form of the verb should be used respectively `Vector::normalize(vector)`vs. `normalizedVector = vector.normalized()`
Following this standard, it becomes easy to spot bugs where a return value is omitted.

## 10. Names representing namespaces must be all lowercase and should not be nested deeper than two levels
A third level is admissible if the last level is an `internal` namespace that is an implementation detail.  Limiting the `namespace`s to two prevents awkwardly long prefixes in the code which would otherwise require `using` statements.

## 11. Abbreviations in names must be avoided
```cpp
computeAverage();   // NOT: compAvg();
```
There are two types of words to consider.  First are the common words listed in the dictionary.  These must never be abbreviated. Never write: `cmd` instead of `command`, `cp` instead of `copy`, `init` instead of `initialize` etc.  Then, there are domain specific phrases that are more naturally known through their abbreviations/acronym. These phrases should be kept abbreviated.  Never write: `HypertextMarkupLanguage` instead of `html`, `CentralProcessingUnit` instead of `cpu`, etc.

## 12. Private class variables must have underscore prefix if part of a larger class
```cpp
class SomeClass {
// ...
private:
  int _depth;
};
```
 > Apart from its name and its type, the scope of a variable is its most important feature.  Indicating class scope by using underscores makes it easy to distinguish class variables from local variables.  There are two side effects of the underscore naming convention; first, it simplifies searching for member variables as code completion will list all member variables if `_` is entered.  Second, it nicely resolves the problem of finding reasonable variable names for setter methods and constructors:
```cpp
void setDepth(int depth) {
  _depth = depth;
}
```
 > An exception to this is simple `struct`s whose main purpose is to hold multiple values without much additional logic in which case the variable's prefix `_` can be omitted

## 13. The length of a variable name should correspond to the length of its scope
Variables with a large scope should have long names, variables with a small scope can have short names.  Obviously this is just a rule of thumb. Scratch variables used for temporary storage or indices are best kept short.  A programmer reading such variables should be able to assume that its value is not used outside of a few lines of code.

## 14. The terms get/set must be used where an attribute is accessed.  The prefix 'get' must be omitted in case the value is returned.  'get' is only to be used when the value is returned in a referenced parameter
```cpp
name = employee.name(); // Value is returned directly -> no get...
employee.setName(name);
string name;
employee.getName(name); // Value is returned in reference parameter -> get...
value = matrix.element(2, 4);
matrix.setElement(2, 4, value);
float value;
matrix.getElement(2, 4, value); // Value is returned in reference parameter -> get...
```
The preferred way is returning the value directly, returning by reference should only be a last resort.  Omitting the word `get` in the accessor turns it from a verb construct into a noun construct and it therefore makes more grammatical sense when it is used in code, c.f.: `if (employee.name().empty())` vs. `if (employee.getName().empty())`


## 15. The prefix `n` should be used for variables representing a number of objects
```cpp
nPoints, nLines, ...
```

## 16. The prefix `i` should be used for variables representing an entity number
```cpp
iTable, iEmployee
```
This effectively makes these variables named iterators.  In a short loop, using just the variable `i` is well understood and fine.

## 17. The prefixes `is`, `has`, `should`, or `can` should be used for boolean variables and methods
`isSet`, `isVisible`, `isFinished`, `isFound`, `isOpen`
Using the `is` prefix solves a common problem of choosing bad boolean names like `status` or `flag`.  `isStatus` or `isFlag` simply doesn’t fit, and the programmer is forced to choose more meaningful names.  There are a few alternatives to the is prefix that fit better in some situations.  These are the `has`, `can`, and `should` prefixes:
```cpp
bool hasLicense();
bool canEvaluate();
bool shouldSort();
```

## 18. Abbreviations and acronyms must not be uppercase when used as name
```cpp
exportHtmlSource(); // NOT: exportHTMLSource();
openDvdPlayer();    // NOT: openDVDPlayer();
```
Using all uppercase for the base name will give conflicts with the naming conventions given above.  A variable of this type would have to be named dVD, hTML etc. which obviously is not very readable.  Another problem is illustrated in the examples above; When the name is connected to another, the readability is seriously reduced; the word following the abbreviation does not stand out as it should.



# Structure
## 19. `#include` statements should be at the top of the file, sorted and grouped
Sorted by their hierarchical position in the system and sorted by name with low-level system or std files included last.  The first entry in a `.cpp` file is the corresponding `.h` file separated from the remaining heads by an empty line.  For the remaining headers, this means first the parent header (if it is a `cpp` file), then all `openspace` headers, then `ghoul` headers, then all other headers, each group sorted by name.
```cpp
#include "com/company/ui/PropertiesDialog.h"

#include "com/company/ui/MainWindow.h"
#include <qt/qbutton.h>
#include <qt/qtextfield.h>
#include <fstream>
#include <iomanip>
```
In addition to showing the individual include files, it also gives a clue about the modules that are involved in the source file.  Include file paths must never be absolute.  A `cpp` file should always include it’s accompanying header file first and separate the other includes by an empty line.

## 20. The parts of a class must be sorted `public`, `protected` and `private`
Not applicable sections should be left out.  The ordering is "most public first" so people who only wish to use the class can stop reading when they reach the protected/private sections.

## 21. Type conversions must always be done explicitly
Don’t rely on implicit type conversion.
```cpp
floatValue = static_cast<float>(intValue); // NOT: floatValue = intValue;
```
 Implementing this removes a lot of bugs that come from unexpected conversion.  By making it very visible that a casting is intended, it becomes easier to spot buggy casts

## 22. All definitions must reside in source or inline files
```cpp
class MyClass {
public:
  int getValue () { return _value; }  // No
  ...
private:
  int _value;
}
```
The header files should declare an interface and the source file should implement it.  Exceptions to this are template classes and template functions among others.  The implementations of those methods must go in a `*.inl` file that is included at the bottom of the header file.  The `inl` file does not require an include guard as it should never be included directly except in the header file it belongs to.  While this restriction increases the number of files that we have to take care of, it also drastically enhances the readability of the code when looking at the header as one doesn't have to mentally remove any code but can focus on the function definitions instead.

## 23. Implicit test for `0` should only be used for boolean variables and pointer-types
```cpp
bool isTrue;
if (isTrue) // NOT: if (isTrue == true)
int nLines;
if (nLines != 0) // NOT: if (nLines)
double value;
if (value != 0.0) // NOT: if (value)
std::unique_ptr<int> ptr;
if (ptr)        // OR: if (ptr != nullptr)
```
Using an explicit test, the statement gives an immediate clue of the type being tested.  Testing pointers for `nullptr` is so common that it can be used.

## 24. Complex conditional expressions should be avoided.  Introduce constant temporary boolean variables instead
```cpp
bool isFinished = (elementNo < 0) || (elementNo > maxElement);
bool isRepeatedEntry = elementNo == lastElement;
if (isFinished || isRepeatedEntry) {
... }
// NOT:
if ((elementNo < 0) || (elementNo > maxElement)||
     elementNo == lastElement) {
  ...
}
```
By assigning boolean variables to expressions, the program gets automatic documentation.  The construction will be easier to read, debug, and maintain.  In optimized code, the intermediate variables will be removed either way, so they don't incur any performance drawbacks.

## 25. Executable statements in conditionals should be avoided
```cpp
File* fileHandle = open(fileName, "w");
if (!fileHandle) {
... }
// NOT:
if (!(fileHandle = open(fileName, "w"))) {
... }
```
 > This is an extension of the "one statement per line" rule that makes things easier to debug.  Storing values in local variables is not a performance drawback as they will get optimized away.  This rule also discourages assignments in `if` statements as allowed in newer C++:  `if (int i = value()) { ... }`
 > This rule is somewhat relaxed with C++ feature of having an instruction and evaluating the result in the same if statement. As long as this lowers the scope of the variable the following is allowed:  `if (int count = countThings();  count > 0) {`

## 26. The use of magic values in the code should be avoided
Numbers other than `0`, `1`, or `-1` should be declared as named constants instead.  The same holds true for string constants, refactoring is made easier if they are defined as a constant.
 > This rule also enforces the "code as documentation" guide as it avoids magic constants, but makes things more readable

## 27. `nullptr` must be used instead of `0` or `NULL` for declaring null pointer
`NULL` is part of the standard C library, but is made obsolete in C++ and `0` has a double meaning as an integer and the null pointer.  Use the C++ `nullptr` instead.

# Best Practices
## Standard library is your friend
The C++ standard libraries `<algorithm>` header contains many useful functions that can make programming life very easy.  Good examples are [`std::for_each`](https://en.cppreference.com/w/cpp/algorithm/for_each), [`std::accumulate`](en.cppreference.com/w/cpp/algorithm/accumulate), [`std::lower_bound`](https://en.cppreference.com/w/cpp/algorithm/lower_bound), [`std::all_of`](https://en.cppreference.com/w/cpp/algorithm/all_any_none_of). See [Cppreference](https://en.cppreference.com/w/cpp/algorithm).

## Keep it simple, sailor
Looking at the time spend for each line of code, the amount of time that future developers (including the future-self of the author of a lin) will spend much much more wall-clock time on any code snippet than the CPU spends executing it.  **Unless it is a performance-critical part of the run-loop**, prefer easy to understand code over obscure and optimized code.  If you come back to a code you wrote 6 months later, it is effectively the same as someone else going back to that code.

# File formatting
## Handling line breaks
```cpp

// In order to keep the code on this page
// compact, a smaller line length is
// simulated
//                                        line
//                                       break
// ........................................|
//
// In a **header** file
//

// Functions:
// Return value + function + parameter fits
ReturnType function(int parameter) const;

// Second argument does not fit in the same
// line.
// Solution: Keep as compact as possible
// with following lines indented by 4
// spaces
ReturnType function(int parameter1,
    int parameter2, int param3) const;

// Only a final const or override does not
// fit in the same line.
// Solution: The last parameter or function
// name moves together with the last
// qualified
ReturnType function(int parameter1,
    int parameter2, int parameter3,
    int p) const;

// Due to a very long function name, even
// the first parameter does not fit on the
// first line.
// Solution: Same as above, but even the
// first parameter is on the next line
// indented by 4 spaces.
ReturnType veryLongFunctionFame(
    int parameter1, int parameter2);

// A long return type and long function
// name cause the function name not to fit
// on the same line
// Solution: Return type gets its own line
VeryLongAndComplexReturnType
veryLongFunctionFame(int parameter1);

//
// In a **source** file
//
// ........................................|

// Same rules as for the header with two
// exceptions:
// 1. If the declaration, for any reason,
//    turns into multiple lines, the
//    opening { gets its own line
VeryLongAndComplexReturnType
veryLongFunctionFame(int parameter1)
{

// 2. When parameters are split up, the
// following parameters are all aligned
// with the opening ( of the parameter list
// or right-aligned, if they don't fit
ReturnType function(int param1, int p2,
                    int p3, int p4,
                    int parameter2,
               int reallyLongParameterName)
{

//
// Function calls
//
// ........................................|

// Functions that don't fit in a single
// line have their parameters split into
// separate lines each. The closing );
// gets its own line

// Things that fit
int r = function(p1, p2);

// Things that don't fit all go on separate
// lines and do **not** compact and the
// lines should be broken as early as 
// possible
int result = function(
    secondFunction(parameter1),
    p3,
    parameter1 * parameter2 * abs(p3)
);

// An exception to this is the handling of
// parameters to the fmt::format function
// since this function is not supposed to
// take any complex, derived parameters.
// In this case, it is better to provide
// the arguments in a compact manner:
LINFO(fmt::format(
    "Foobar {} and barfoo {}", nBars, nFoos
));

//
// Operators
//
// ........................................|

// Chains of operators that don't fit into
// one line are split up on logical
// barriers and align with the first
// argument

int i = parameter1 * parameter2 * j +
        parameter2 * k;

```

## Constructor layout
The initialization of member variables should happen in the header file, if possible.  Remaining member variable initialization in the constructor should be organized as follows:
```cpp
// All initialization is on a separate line with the : or , starting the line
Classname::ClassName(int parameter, int parameter2)
    : _memberVar(parameter)
    , _memberVar2(parameter + parameter2)
```     
If a member variable initialization takes more than one line, it follows the rules for functions:
```cpp
// ........................................|
Classname::ClassName(int parameter1,
                     int parameter2)
    : _memberVariableTakingParameters(
        parameter1,
        Enum::Yes
    )
    , _memberParam2(parameter2)
{
```
