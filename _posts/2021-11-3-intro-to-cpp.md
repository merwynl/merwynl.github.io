---
title: "Introduction to C++"
tags: [code, scripting, programming, cpp, c++, basics, 基本, 🔰初心者]
category: [code]
---

# Process

## 1. Overview

- C++ is a general purpose, statically-typed, object-oriented language built in the late 70's.
- Built as an extension of the C language.
- All C++ must utilize a compiler as it relies on a user to manage the memory & garbage collection
- Uses the concept of header or .h files to manage declarations.
- A header files is where you would declare any variables of properties that you might want to use in say a function. This is then called or referenced in the main .cpp file
- iostream is a pre-defined header file containing functions to read/write to standard input/output streams.
- The string header on the other hand, contains functions for dealing with string items

```c++

/*
 Skeletal structure of a basic basic C++ file
 */
#include <iostream>
#include <string>
using namespace std;

// Main function call that getx executed when running your program
int main()
{

  // 
    return 0;
}

```

- Using a namespace o standard namespace means you won't have to prefix your C++ method calls with std.
- However some consider using namespace std to be bad practice as it introduces complications when upgrading your codebase to a new version that includes new functions.

## 2. Printing

```c++
/*
Skeletal structure of a basic basic C++ file
*/
#include <iostream>
#include <string>
using namespace std;

// Main function call that getx executed when running your program
int main()
{ 
  /*
     P R I N T I N G / プリント
     Prints each of the individual strings below onto separate lines.
     以下の各文字列をそれぞれ別の行に表示します。
     */
    cout << "Hello" << endl;
    cout << "World" << endl;
    cout << "!" << endl;

  return 0;
}
```

- cout is used to declare that something is to be printed.
- endl indicates that the next string should be printed on a new line.
