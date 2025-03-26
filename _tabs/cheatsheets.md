---
# the default layout is 'page'
icon: fa-solid fa-file-code
order: 6
---
A basic reference sheet of common syntax and functions for Python, C++, C# & C
## Python

#### Data Types & Declarations
```python
myInt = 1 # Integer: Whole dayss
myFloat = 1.5 # Decimal Values
myBoole = False # Boolean: True or false 
myString = "いいです" # String: Series of characters

#  Printing statements
print("これがいいです！")

# This is a comment
''' This is a doc-string '''

```

#### Strings
```python

# Strings — A string of alphanumeric characters
first_name = "Test"
last_name = "Code"
food = "Yum"
email = "fakemail@mail.com"
print(first_name + " " + last_name) # Printing & concatenating string variables
print(f"Hello {first_name}.") # String formatting or f-string


```
#### Type Casting
```python

#   vars
myInt = 100
string = "foo"
myFloat = 1.25
myBool = True

# Converting a float to an int truncates the decimal value
myFloat = int(myFloat)
print(int(myFloat))

# Converting an int to a float adds a decimal value of .0 at the end.
myInt =  float(myInt)
print(myInt)

# Converting the previous variable from a float to a string should look the same but be aware of type conversion.
myInt = str(myInt)
print(myInt)
print(type(myInt))

# += an int value increments the existing int
age = 100
age += 1  # Same as age ＝ age + 1
print(age)

# += on a str concatenates the value to the existing string
age = str(age)
age += "1"  # Same as age ＝ age + 1
print(age)

# Typecasting a string to a bool will always return True
string = bool(string)
print(string)

# Typecasting an empty string to a bool will always return False
name = ""
name = bool(name)
print(name)

```

#### Numbers
```python
import math # Imports native math module
days = 25 # Integers — Whole dayss
price = 10.99 # Float - Decimal dayss
print(-2.0987) # Prints a basic given days
days = days + 2 # Incrementing a days
days += 1 #Addition
days -= 1 #Subtraction
days *= 2 # Multiplication 
days /= 2 # Division
days **= 2 # Returns the result of an exponent
days %= 2 # Divides two given values & returns the remainder. Useful to determine if a number is even or odd

```

#### Booleans
```python
# Boolean — True or false
is_student = True
for_sale = False
is_online = False
print(f"Are you a student?: {is_student}")
```

#### User Input
```python
# input() - Prompts the user to enter some data and returns it as a string.
name = input("Greetings, please enter your name: ") # Asking the user’s name
age = int(input("What is your age: ")) # Number value has to be type converted before incrementing else it will be treated as a str.

```

#### Statements
```python

# Strings — A string of alphanumeric characters
first_name = "Test"
last_name = "Code"
food = "Yum"
email = "fakemail@mail.com"
print(first_name + " " + last_name) # Printing & concatenating string variables
print(f"Hello {first_name}.") # String formatting or f-string
```


## C++

#### Main Function & Printing
``` cpp
int main()
 {
  /** Printing a string to the console. \n starts a new line.*/  
  std::cout << "Hello world" << '\n';
  std::cin.get();
  return 0;
 } 

```

#### Data Types

``` cpp

char myCharacter = 'Y';
int myInt = 10;
float myFloat = 1.0f;
bool myBool = true;

// Retrieving the size of a variable
std::cout << sizeof (variable) << '\n';

```

#### If Statements

``` cpp

/** Showcasing different methods of declaring variables & a basic If statement */
int a(1);
int b = 13;
if (b < a)
{
  std::cout << "a in less than b" << '\n';
}

```

#### If Else Statements
``` cpp

/** Example of using an if values to compare values. if (Variable); is the same as writing if (Variable == True) */
int X = myBool;
if (X)
  Log("True");
else
{
  Log("NOT true");
}
```


<!-- 
## C




## C# -->
