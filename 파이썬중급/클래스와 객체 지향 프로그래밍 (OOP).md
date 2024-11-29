클래스와 객체 지향 프로그래밍 (OOP: Object-Oriented Programming)
**객체 지향 프로그래밍(OOP)**은 프로그램을 객체(object)라는 개념을 중심으로 구성하는 프로그래밍 패러다임입니다. 객체는 데이터(속성)와 이 데이터를 처리하는 코드(메서드)를 묶어 캡슐화합니다. 이를 통해 코드를 재사용하기 쉽고, 유지보수를 용이하게 만듭니다.

1. 클래스와 객체
클래스(Class)
객체를 만들기 위한 청사진 또는 설계도입니다.
객체가 가져야 할 속성과 동작을 정의합니다.
객체(Object)
클래스를 기반으로 생성된 실제 인스턴스입니다.
객체는 클래스에서 정의한 속성과 메서드를 가지고 있습니다.
클래스와 객체의 관계
개념	설명
클래스	설계도, 틀 (예: 자동차 설계도)
객체	설계도를 기반으로 만들어진 실체 (예: 특정 자동차)
2. 클래스 정의와 객체 생성

클래스 정의

class Car:
    # 클래스 속성 (모든 객체에 공유됨)
    wheels = 4
    
    # 생성자 메서드 (객체 초기화)
    def __init__(self, color, model):
        # 인스턴스 속성 (각 객체마다 다름)
        self.color = color
        self.model = model
    
    # 메서드 (객체의 동작)
    def drive(self):
        print(f"{self.color} {self.model} is driving!")

# 객체 생성
my_car = Car("Red", "Sedan")
your_car = Car("Blue", "SUV")

# 속성 접근
print(my_car.color)  # 출력: Red
print(your_car.wheels)  # 출력: 4

# 메서드 호출
my_car.drive()  # 출력: Red Sedan is driving!
your_car.drive()  # 출력: Blue SUV is driving!
3. 객체 지향의 주요 개념
1. 캡슐화 (Encapsulation)
속성과 메서드를 하나의 객체에 묶는 것.
객체 내부의 데이터를 보호하고, 외부에는 필요한 인터페이스만 제공합니다.
접근 제어자를 사용하여 구현 (public, private 등).

class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # 비공개 속성 (private)
    
    def deposit(self, amount):
        self.__balance += amount
    
    def withdraw(self, amount):
        if self.__balance >= amount:
            self.__balance -= amount
        else:
            print("Insufficient funds!")
    
    def get_balance(self):
        return self.__balance

# 객체 생성
account = BankAccount(1000)
account.deposit(500)
print(account.get_balance())  # 출력: 1500

# 비공개 속성 접근 불가
# print(account.__balance)  # AttributeError 발생
2. 상속 (Inheritance)
기존 클래스(부모 클래스)의 속성과 메서드를 상속받아 새로운 클래스(자식 클래스)를 생성하는 것.
코드 재사용성을 높이고 중복을 줄임.

class Animal:
    def speak(self):
        print("Animal makes a sound")

class Dog(Animal):  # Animal을 상속받음
    def speak(self):
        print("Dog barks")

class Cat(Animal):  # Animal을 상속받음
    def speak(self):
        print("Cat meows")

# 객체 생성
dog = Dog()
cat = Cat()

dog.speak()  # 출력: Dog barks
cat.speak()  # 출력: Cat meows
3. 다형성 (Polymorphism)
같은 이름의 메서드가 다른 클래스에서 다르게 동작할 수 있는 것.
상속과 함께 사용되어 유연한 코드 작성이 가능.

class Shape:
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2

# 다형성 활용
shapes = [Rectangle(4, 5), Circle(3)]

for shape in shapes:
    print(shape.area())  # 출력: 20, 28.26

4. 추상화 (Abstraction)
중요한 정보만 표시하고 세부사항은 숨기는 것.
추상 클래스를 사용하여 구현.

from abc import ABC, abstractmethod

class Vehicle(ABC):  # 추상 클래스
    @abstractmethod
    def start(self):
        pass

class Car(Vehicle):
    def start(self):
        print("Car is starting")

class Bike(Vehicle):
    def start(self):
        print("Bike is starting")

# 객체 생성
car = Car()
bike = Bike()

car.start()  # 출력: Car is starting
bike.start()  # 출력: Bike is starting

4. 객체 지향 프로그래밍의 장점
재사용성: 기존 코드를 재사용하여 새로운 프로그램 개발 가능.
유지보수성: 코드가 구조화되어 있어 수정과 유지보수가 쉬움.
확장성: 새로운 기능을 추가하거나 기존 기능을 확장하기 용이.
유연성: 다형성을 통해 유연하고 일반화된 코드 작성 가능.

5. 객체 지향 프로그래밍의 단점
복잡성: 절차 지향 프로그래밍보다 구조가 복잡.
초기 개발 비용 증가: 설계와 클래스 작성에 더 많은 시간이 필요.
성능 저하: OOP의 일부 특징(예: 상속)은 런타임 성능에 영향을 줄 수 있음.

6. 객체 지향 프로그래밍과 절차 지향 프로그래밍 비교
특징	객체 지향 프로그래밍	절차 지향 프로그래밍
중심 개념	객체와 클래스	함수와 코드 블록
코드 재사용성	상속, 다형성을 통한 재사용성 높음	함수 호출로 재사용 가능
유지보수성	구조화된 설계로 유지보수 용이	코드가 길어지면 유지보수 어려움
적용 사례	복잡한 대규모 프로젝트	간단한 프로그램

7. OOP의 실제 예제

class Employee:
    def __init__(self, name, position, salary):
        self.name = name
        self.position = position
        self.salary = salary

    def work(self):
        print(f"{self.name} is working as a {self.position}.")

class Manager(Employee):
    def __init__(self, name, salary, team_size):
        super().__init__(name, "Manager", salary)
        self.team_size = team_size

    def manage(self):
        print(f"{self.name} is managing a team of {self.team_size} people.")

# 객체 생성
employee = Employee("Alice", "Developer", 50000)
manager = Manager("Bob", 70000, 10)

employee.work()  # 출력: Alice is working as a Developer.
manager.work()   # 출력: Bob is working as a Manager.
manager.manage() # 출력: Bob is managing a team of 10 people.
Python에서 객체 지향 프로그래밍을 잘 활용하면 유지보수성과 확장성이 뛰어난 프로그램을 작성할 수 있습니다! 🎉
