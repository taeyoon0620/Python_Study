모듈과 패키지 (Modules & Packages)
Python에서 **모듈(module)**과 **패키지(package)**는 코드를 조직화하고 재사용성을 높이는 데 사용됩니다.
큰 프로그램을 작은 단위로 나누어 유지보수를 쉽게 하고, 코드 중복을 줄이는 데 도움을 줍니다.

1. 모듈 (Module)
모듈이란?
Python에서 하나의 .py 파일이 모듈입니다.
모듈에는 함수, 변수, 클래스 등 Python 코드가 포함됩니다.
코드 재사용과 구조화를 위해 사용됩니다.
모듈 사용법
모듈 생성 파일 이름: my_module.py

def greet(name):
    return f"Hello, {name}!"

PI = 3.14159
모듈 가져오기 모듈 파일을 import해서 사용합니다.

import my_module

print(my_module.greet("Alice"))  # 출력: Hello, Alice!
print(my_module.PI)              # 출력: 3.14159
별칭 사용

import my_module as mm

print(mm.greet("Bob"))  # 출력: Hello, Bob!
특정 요소만 가져오기

from my_module import greet, PI

print(greet("Charlie"))  # 출력: Hello, Charlie!
print(PI)                # 출력: 3.14159
모든 요소 가져오기

from my_module import *

print(greet("Dave"))  # 출력: Hello, Dave!
print(PI)             # 출력: 3.14159
내장 모듈 사용
Python에는 이미 제공되는 많은 내장 모듈이 있습니다.

math 모듈

import math

print(math.sqrt(16))  # 출력: 4.0
print(math.pi)        # 출력: 3.141592653589793
random 모듈

import random

print(random.randint(1, 10))  # 1~10 사이의 랜덤 정수

2. 패키지 (Package)
패키지란?
여러 모듈을 묶어 놓은 디렉토리입니다.
디렉토리 안에 __init__.py 파일을 포함해 패키지로 인식되게 만듭니다.
복잡한 프로젝트를 체계적으로 관리하는 데 사용됩니다.
패키지 구조
다음과 같은 디렉토리 구조로 패키지를 생성할 수 있습니다.

mypackage/
    __init__.py
    module1.py
    module2.py
__init__.py 파일

패키지를 초기화하는 데 사용됩니다.
패키지에서 사용할 모듈이나 설정을 정의할 수 있습니다.
Python 3.3 이후에는 파일이 없어도 패키지로 인식됩니다.
모듈 내용

module1.py

def add(a, b):
    return a + b
module2.py
python
코드 복사
def subtract(a, b):
    return a - b
패키지 가져오기

패키지를 사용하려면 import를 사용합니다.

import mypackage.module1
import mypackage.module2

print(mypackage.module1.add(5, 3))      # 출력: 8
print(mypackage.module2.subtract(5, 3))  # 출력: 2
특정 모듈 가져오기

from mypackage.module1 import add

print(add(10, 20))  # 출력: 30
패키지 전체 가져오기

from mypackage import module1, module2

print(module1.add(1, 2))         # 출력: 3
print(module2.subtract(10, 3))  # 출력: 7

3. 모듈과 패키지의 차이
   
구분	모듈	패키지
정의	하나의 .py 파일	여러 모듈을 포함한 디렉토리
사용 목적	코드 재사용 및 단순화	대규모 프로젝트의 코드 구조화
구성 요소	변수, 함수, 클래스	__init__.py, 여러 .py 파일
예제	math, random	os, collections

5. 장점
모듈
코드 재사용성을 높임.
코드 관리와 유지보수를 용이하게 함.
패키지
대규모 프로젝트에서 코드 구조를 체계적으로 구성.
서로 다른 모듈 간의 충돌을 방지.
6. 예제: 사용자 정의 패키지
디렉토리 구조

calculator/
    __init__.py
    basic.py
    advanced.py
코드
basic.py

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b
advanced.py

def multiply(a, b):
    return a * b

def divide(a, b):
    if b != 0:
        return a / b
    return "Division by zero!"
사용

from calculator.basic import add, subtract
from calculator.advanced import multiply, divide

print(add(5, 3))        # 출력: 8
print(subtract(10, 4))  # 출력: 6
print(multiply(2, 3))   # 출력: 6
print(divide(10, 2))    # 출력: 5.0
모듈과 패키지를 잘 활용하면 코드의 재사용성, 가독성, 유지보수성이 크게 향상됩니다! 🎉
