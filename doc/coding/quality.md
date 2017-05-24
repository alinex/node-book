# Quality Standards


## Goals

These are seen as goals meaning not every goal may be reached or completely reached.

### Functionality

Everything which is possible in the web should be allowed. The range should be kept wide but implemented a short range first.

Each function have to full fill the goals:
- all specific requirements have to be reached
- security issues have to be checked
- automatic tests should be integrated

### Universal usable

The system should run on most systems without problems. Special modules are always optional. No commercial code is used or integrated. General interfaces are used everywhere:
- easy to install
- works beside other software

For the user it should also be accessible with any client on any system from everywhere with ease:
- easy to understand
- easy to learn
- use as known from other systems
- optimized for office (shortcuts...)

### Stability

Clear control structures and optimal error management helps to work on problems. Unit Tests give the ability to find those early in the development process.

This is reached specifically by:
- complete checking of all external information
- one problem should not bring down the whole system

### Performance

The system's performance is optimized. But this is not the highest goals because
in contradicts the fast prototyping.
- low resource usage
- support for different caching systems
- clustering
- help for system optimization

### Extensibility

The system is complete class based with loose coupling and dependency injection to allow easy extension. Classes, libraries there is room and interfaces to add nearly anything.


## Step by Step

Technically spoken I will bring the modules through six different quality steps.
Each class is based on the previous ones and can only be reached one after another.
Hopefully a lot of my modules will reach class F but I am clear that this is not
possible for all of them.

But as with the goals I may use it as guideline which I try to follow but not need to.

### Class A

- Update file structure to new standard
- Restructure docs into doc folder
- short README in pure Github markdown
- create GitBook documentation and link it

### Class B

- base functionality working

### Class C

- use Debug with if debug.enabled
- Validate options if called using debug
- ES6 Code with partly imports

### Class D

- Add Travis CI with node v6
- release NodeJS package

### Class E

- Enhance test coverage over 80%
- complete documentation with examples

### Class F

- No more Features
