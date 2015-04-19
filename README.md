# vala-manual-vapi
Using a manually created VAPI for a C library with Vala.

An very basic example C library that provides a method to sum two numbers is below.

The C file source: **lib.c**
```c
#include <stdio.h>
#include "lib.h"

int add(int a, int b)
{
  printf("Adding numbers %d and %d\n", a, b);
  return a + b;
}
```

The header for the C file source: **lib.h**
```c
#ifndef WHATEVER_H_INCLUDED
#define WHATEVER_H_INCLUDED
    int add(int a, int b);
#endif
```

The hand-crafted VAPI file: **lib.vapi**

```vala
[CCode (cheader_filename = "lib.h")]
namespace MyMaths
{
    [CCode (cname = "add")]
    public int add (int a, int b);
}
```

Lastly, the vala file that will call the C library: **test.vala**

```vala
using MyMaths;

void main()
{
    int sum = add(5, 5);
    stdout.printf("Total: %d\n", sum);
}
```

Compile everything to generate a `./test` executable:

`valac test.vala lib.vapi lib.c`

Run it, and you'll see the output below.

```
Adding numbers 5 and 5
Total: 10
```


