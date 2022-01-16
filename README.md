# python pure

### Functions can be treated as objects
```
# Python program to illustrate functions
# can be treated as objects
def shout(text):
    return text.upper()
 
print(shout('Hello'))
 
yell = shout
 
print(yell('Hello'))
```
#### Output
```
HELLO
HELLO
```

### Functions can be passed as arguments to other functions
```
# Python program to illustrate functions
# can be passed as arguments to other functions
def shout(text):
    return text.upper()
 
def whisper(text):
    return text.lower()
 
def greet(func):
    # storing the function in a variable
    greeting = func("""Hi, I am created by a function passed as an argument.""")
    print (greeting)
 
greet(shout)
greet(whisper)
```
#### Output
```
HI, I AM CREATED BY A FUNCTION PASSED AS AN ARGUMENT.
hi, i am created by a function passed as an argument.
```
 ### Functions can return another function
 ```
# Python program to illustrate functions
# Functions can return another function
 
def create_adder(x):
    def adder(y):
        return x+y
 
    return adder
 
add_15 = create_adder(15)
 
print(add_15(10))
 ```
#### Output
```
25
```

# Decorators

## Decorators are used to modify the behaviour of function or class. In Decorators, functions are taken as the argument into another function and then called inside the wrapper function.

```
@gfg_decorator
def hello_decorator():
    print("Gfg")

'''Above code is equivalent to -

def hello_decorator():
    print("Gfg")
    
hello_decorator = gfg_decorator(hello_decorator)'''
```
## There is another example
```
# importing libraries
import time
import math
 
# decorator to calculate duration
# taken by any function.
def calculate_time(func):
     
    # added arguments inside the inner1,
    # if function takes any arguments,
    # can be added like this.
    def inner1(*args, **kwargs):
 
        # storing time before function execution
        begin = time.time()
         
        func(*args, **kwargs)
 
        # storing time after function execution
        end = time.time()
        print("Total time taken in : ", func.__name__, end - begin)
 
    return inner1
 
 
 
# this can be added to any function present,
# in this case to calculate a factorial
@calculate_time
def factorial(num):
 
    # sleep 2 seconds because it takes very less time
    # so that you can see the actual difference
    time.sleep(2)
    print(math.factorial(num))
 
# calling the function.
factorial(10)
```

#### Output
```
3628800
Total time taken in :  factorial 2.0061802864074707
```
## What if a function returns something or an argument is passed to the function?
### In all the above examples the functions didn’t return anything so there wasn’t any issue, but one may need the returned value.
```
def hello_decorator(func):
    def inner1(*args, **kwargs):
         
        print("before Execution")
         
        # getting the returned value
        returned_value = func(*args, **kwargs)
        print("after Execution")
         
        # returning the value to the original frame
        return returned_value
         
    return inner1
 
 
# adding decorator to the function
@hello_decorator
def sum_two_numbers(a, b):
    print("Inside the function")
    return a + b
 
a, b = 1, 2
 
# getting the value through return of the function
print("Sum =", sum_two_numbers(a, b))
```

#### Output
```
before Execution
Inside the function
after Execution
Sum = 3
```

## Chaining Decorators

### In simpler terms chaining decorators means decorating a function with multiple decorators.
### Example:
```
# code for testing decorator chaining
def decor1(func):
    def inner():
        x = func()
        return x * x
    return inner
 
def decor(func):
    def inner():
        x = func()
        return 2 * x
    return inner
 
@decor1
@decor
def num():
    return 10
 
print(num())
```
## Class decorator
```
import requests


class LimitQuery:

    def _init_(self, func):
        self.func = func
        self.count = 0

    def _call_(self, *args, **kwargs):
        self.limit = args[0]
        if self.count < self.limit:
            self.count += 1
            return self.func(*args, **kwargs)
        else:
            print(f'No queries left. All {self.count} queries used.')
            return

@LimitQuery
def get_coin_price(limit):
    '''View the Bitcoin Price Index (BPI)'''
    
    url = requests.get('https://api.coindesk.com/v1/bpi/currentprice.json')

    if url.status_code == 200:
        text = url.json()
        return f"${float(text['bpi']['USD']['rate_float']):.2f}"


print(get_coin_price(5))
print(get_coin_price(5))
print(get_coin_price(5))
print(get_coin_price(5))
print(get_coin_price(5))
print(get_coin_price(5))
```

### Output ---> decor1(decor(num))
```
400
```

# __ call __
```
class Example:
    def __init__(self):
        print("Instance Created")
      
    # Defining __call__ method
    def __call__(self):
        print("Instance is called via special method")
  
# Instance created
e = Example()
  
# __call__ method will be called
e()
```
## Output
```
Instance Created
Instance is called via special method
```

# publishing packages
```
pip install setuptools wheel twine
mkdir mamadpdf
cd mamadpdf
mkdir mamadpdf
mkdir tests
mkdir data
cd maamdpdf and create __init__, pdf2text.py and ... files with some methods
cd ..
create README.md file
create setup.py file 
inside of setup file :
  import seruptools
  from pathlib import Path
  
  setuptools.setup(
    name="mamadpdf",
    version=1.0,
    long_descriprion=Path("README.md").read_text(),
    packages=setuptools.find_packages(exclude=["tests","data"])
  )
  
 python3 setup.py sdist bdist_wheel
 twine upload dist/*
```
# python documetion
```
pydoc3 math

# My python file:
pydoc3 moshpdf.pdf2image
pydoc3 -w moshpdf.pdf2image

```






