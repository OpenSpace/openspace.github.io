---
title: Frequenty Asked Questions
layout: default

parent: Users
nav_order: 4
---

# Linux
## OpenSpace reports number errors when compiling shaders
Error:
```Error linking program object [LocalChunkedLodPatch Vertex]: 6(54) :
error C0000: syntax error, unexpected integer constant at token "<int-const>"
6(70) : error C0000: syntax error, unexpected integer constant at token "<int-const>"
```

Reason:  We use the operating system's locale to convert numeric values into text.  On some languages (Spanish and German, for example), a "," is used as the decimal separator, leading a `3` to be converted to `3,0` which the code does not understand.  If you are finding this, you can overwrite the locale by exporting it to your shell first:
```
# export LC_NUMERIC="en_US.UTF-8"
# ./OpenSpace
```
