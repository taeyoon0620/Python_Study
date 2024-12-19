Python 기초 문법
Python은 간결하고 읽기 쉬운 문법을 가진 고급 프로그래밍 언어입니다. 다음은 Python의 주요 기초 문법과 예제입니다.

1. 변수와 데이터 타입
Python은 변수 선언 시 자료형을 명시하지 않아도 됩니다. 변수의 자료형은 값에 따라 자동으로 결정됩니다.

1) 변수 선언과 할당

# 변수 선언 및 할당
x = 10         # 정수
y = 3.14       # 실수
name = "Alice" # 문자열
is_active = True  # 불리언
2) 데이터 타입 확인

print(type(x))        # <class 'int'>
print(type(name))     # <class 'str'>
print(type(is_active)) # <class 'bool'>
2. 기본 연산자
Python은 산술, 비교, 논리, 할당 연산자 등을 제공합니다.

1) 산술 연산자

a, b = 10, 3
print(a + b)  # 덧셈: 13
print(a - b)  # 뺄셈: 7
print(a * b)  # 곱셈: 30
print(a / b)  # 나눗셈: 3.333...
print(a % b)  # 나머지: 1
print(a ** b) # 거듭제곱: 1000
print(a // b) # 몫: 3
2) 비교 연산자

print(a > b)   # True
print(a < b)   # False
print(a == b)  # False
print(a != b)  # True
print(a >= b)  # True
print(a <= b)  # False
3) 논리 연산자

x, y = True, False
print(x and y)  # 논리 AND: False
print(x or y)   # 논리 OR: True
print(not x)    # 논리 NOT: False
3. 조건문
1) if-elif-else 구조

x = 10
if x > 10:
    print("x는 10보다 큽니다.")
elif x == 10:
    print("x는 10입니다.")
else:
    print("x는 10보다 작습니다.")
4. 반복문
1) for문

for i in range(5):  # 0부터 4까지 반복
    print(i)
2) while문

count = 0
while count < 5:
    print(count)
    count += 1
5. 함수
1) 함수 정의와 호출

def greet(name):
    return f"Hello, {name}!"

print(greet("Alice"))  # 출력: Hello, Alice!
2) 기본 매개변수

def greet(name="Guest"):
    return f"Hello, {name}!"

print(greet())  # 출력: Hello, Guest!
3) 가변 매개변수

def add(*args):
    return sum(args)

print(add(1, 2, 3, 4))  # 출력: 10
6. 리스트와 컬렉션
1) 리스트

fruits = ["apple", "banana", "cherry"]
print(fruits[0])      # 출력: apple
fruits.append("date") # 리스트 추가
print(fruits)         # 출력: ['apple', 'banana', 'cherry', 'date']
2) 딕셔너리

person = {"name": "Alice", "age": 25}
print(person["name"])       # 출력: Alice
person["city"] = "New York" # 값 추가
print(person)               # {'name': 'Alice', 'age': 25, 'city': 'New York'}
3) 세트

numbers = {1, 2, 3}
numbers.add(4)    # 값 추가
print(numbers)    # 출력: {1, 2, 3, 4}
7. 클래스와 객체
1) 클래스 정의

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        return f"Hello, my name is {self.name}!"

# 객체 생성 및 사용
person = Person("Alice", 25)
print(person.greet())  # 출력: Hello, my name is Alice!
8. 파일 I/O
1) 파일 쓰기

with open("example.txt", "w") as file:
    file.write("Hello, Python!")
2) 파일 읽기

with open("example.txt", "r") as file:
    content = file.read()
    print(content)
9. 예외 처리
1) try-except 사용

try:
    result = 10 / 0
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
finally:
    print("예외 처리 완료.")
10. 모듈과 패키지
Python은 모듈화를 통해 코드 재사용성을 높입니다.

1) 모듈 가져오기

import math

print(math.sqrt(16))  # 출력: 4.0
2) 사용자 정의 모듈
my_module.py 파일:

def add(a, b):
    return a + b
다른 파일에서 사용:

from my_module import add

print(add(2, 3))  # 출력: 5

요약
Python의 기초 문법은 간결하고 이해하기 쉬워 초보자도 빠르게 배우고 활용할 수 있습니다. 이를 기반으로 다양한 고급 기능을 학습하면 효율적인 프로그래밍이 가능합니다.
