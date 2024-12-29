클래스와 객체지향 프로그래밍 (OOP)
Python에서 클래스와 객체는 객체지향 프로그래밍(OOP, Object-Oriented Programming)의 기본 개념입니다. OOP는 코드의 재사용성, 유지보수성, 확장성을 높이는 데 유용합니다.

1. 클래스(Class)
정의: 클래스는 객체를 만들기 위한 설계도 또는 템플릿입니다.
구성 요소:
속성(Attributes): 클래스에서 정의된 데이터.
메서드(Methods): 클래스에서 정의된 함수, 객체의 동작을 정의.
클래스 선언

class 클래스이름:
    def __init__(self, 속성1, 속성2):  # 생성자 메서드
        self.속성1 = 속성1
        self.속성2 = 속성2

    def 메서드이름(self):
        print(f"{self.속성1}과 {self.속성2}")
2. 객체(Object)
정의: 클래스에서 생성된 실체.
특징: 클래스의 속성과 메서드를 상속받아 독립적으로 사용.
객체 생성

객체이름 = 클래스이름(속성1값, 속성2값)
3. 객체지향 프로그래밍(OOP) 특징
캡슐화(Encapsulation):

데이터를 은닉하고, 메서드를 통해서만 접근할 수 있도록 합니다.
접근 제어자(public, private)를 통해 구현:
public: 모든 곳에서 접근 가능.
_protected: 클래스와 서브클래스에서만 접근.
__private: 클래스 내부에서만 접근 가능.

class EncapsulationExample:
    def __init__(self):
        self.public_data = "Public"
        self._protected_data = "Protected"
        self.__private_data = "Private"

    def get_private_data(self):
        return self.__private_data

obj = EncapsulationExample()
print(obj.public_data)          # Public
print(obj._protected_data)      # Protected
print(obj.get_private_data())   # Private
상속(Inheritance):

기존 클래스를 기반으로 새로운 클래스를 생성.
코드 재사용성을 높이고 기능 확장이 가능.

class Parent:
    def greet(self):
        print("안녕하세요, 부모 클래스입니다.")

class Child(Parent):
    def greet(self):
        print("안녕하세요, 자식 클래스입니다.")

obj = Child()
obj.greet()  # 안녕하세요, 자식 클래스입니다.
다형성(Polymorphism):

같은 이름의 메서드가 상황에 따라 다르게 동작.
오버라이딩(Overriding)과 오버로딩(Overloading)으로 구현.

class Animal:
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        return "멍멍"

class Cat(Animal):
    def sound(self):
        return "야옹"

animals = [Dog(), Cat()]
for animal in animals:
    print(animal.sound())
추상화(Abstraction):

객체의 복잡성을 숨기고 필요한 기능만 노출.
Python에서는 abc 모듈로 구현 가능.

from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def sound(self):
        pass

class Dog(Animal):
    def sound(self):
        return "멍멍"

obj = Dog()
print(obj.sound())  # 멍멍
4. 예제: 클래스와 객체

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        print(f"안녕하세요, 제 이름은 {self.name}이고, 나이는 {self.age}살입니다.")

# 객체 생성
person1 = Person("홍길동", 25)
person1.introduce()  # 안녕하세요, 제 이름은 홍길동이고, 나이는 25살입니다.

5. OOP의 장점
코드 재사용성 증가: 상속과 다형성으로 코드 중복을 줄일 수 있습니다.
유지보수 용이: 코드를 모듈화하여 수정이 쉽습니다.
가독성 향상: 객체 중심 설계로 직관적인 코드 작성이 가능합니다.

6. 실제 활용
게임 개발: 캐릭터, 아이템 등을 객체로 정의.
웹 애플리케이션: 사용자, 데이터베이스 모델 등.
머신러닝: 데이터셋 및 모델을 객체로 정의.
객체지향 프로그래밍은 프로젝트가 커질수록 효율적인 코드 관리와 확장을 가능하게 합니다. 😊
