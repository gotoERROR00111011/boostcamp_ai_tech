# Week 1 - Day 04 - 파이썬 기초 문법 III

## Introduction

### Lecture

- Python Object Oriented Programming
- Module and Project

오늘 강의는 잘모르는 python 기능이 많아서 즐겁게 보았다.

## Class

### Declaration

python의 naming convention은 다음 두가지를 사용한다.

- snake_case : 변수, 함수
- UpperCamelCase : 클래스

```python
# class
class ClassName(object):
    def __init__(self, name):
        self.name = name
# instance
class_name = ClassName()
```

### Inheritance

```python
class Person(object):
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Employee(Person):
    def __init__(self, name, age, salary):
        super().__init__(name, age):
        self.salary = salary
```

### Polymorphism

```python
class Animal:
    def init(self, name):
        self.name = name
    def talk(self):
        raise NotImplementedError("Subclass must implement abstract method")

class Cat(Animal):
    def talk(self):
        return "Meow!"

class Dog(Animal):
    def talk(self):
        return "Woof!"
```

### Visibility

```python
class Inventory(object):
    def __init__(self):
        self.__items = []

    @property
    def items(self):
        return self.__items
```

## Decorate

### First-Class Object

python의 함수는 변수할당, 파라메터 전달, 리턴 값 으로 사용가능하다.

```python
def square(x):
    return x * x
f = square
f(5)
```

### Inner Function

```python
def print_msg(msg):
    def printer():
        print(msg)
    printer()
print_msg("Hello, Python")
```

### Closure

```python
def tag_func(tag, text):
    tag = tag
    text = text

    def inner_func():
        return "<{0}>{1}<{0}>".format(tag, text)

    return inner_func()
h1_func = tag_func("h1", "This is Python Class")
h1_func()
```

### Decorator Function

```python
def star(func):
    def inner(*args, **kwargs):
        print("*" * 30)
        func(*args, **kwargs)
        print("*" * 30)
    return inner

def percent(func):
    def inner(*args, **kwargs):
        print("%" * 30)
        func(*args, **kwargs)
        print("%" * 30)
    return inner

@star
@percent
def printer(msg):
    print(msg)
printer("Hello")
#******************************
#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#Hello
#%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
#******************************
```

```python
def generate_power(exponent):
    def wrapper(f):
        def inner(*args):
            result = f(*args)
            return exponent**result
        return inner
    return wrapper

@generate_power(2)
def raise_two(n):
    return n**2

print(raise_two(7))
# exponent <- 2
# f <- raise_two
# *args <- n
```

## Module

```python
# module_test.py

import test_module as tm
tm.test()

from test_module import test
test()

from test_module import *
test()
```

## Package

```
- game
    - __init__.py
    - image
        - __init_.py
        - character.py
    - sound
        - __init_.py
        - echo.py
        - bgm.py
    - stage
        - __init_.py
        - main.py
        - sub.py
```

```python
from game.sound.bgm import play
from ..sound.bgm import play
```

## Team

- 과제 코드리뷰
- 조교님 팀 면담 일정 확인
