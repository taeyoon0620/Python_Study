데코레이터(Decorators)는 기존의 함수나 클래스에 추가적인 기능을 부여하는 일종의 함수입니다. 주로 Python에서 사용되지만, JavaScript, Java와 같은 언어에서도 유사한 개념으로 확장할 수 있습니다. 데코레이터는 원래 함수나 클래스의 코드를 수정하지 않고도 새로운 기능을 추가할 수 있기 때문에, 코드의 재사용성과 가독성을 높이는 데 유용합니다.

1. 데코레이터의 개념
데코레이터는 다른 함수를 인수로 받아서, 그 함수에 추가적인 기능을 적용한 후 다시 반환하는 함수입니다. 이를 통해 데코레이터는 원래 함수의 동작을 감싸거나 수정할 수 있습니다. 예를 들어, 함수의 실행 시간을 측정하거나, 접근 제어(권한 검사)와 같은 기능을 추가할 수 있습니다.

데코레이터의 기본 구조는 다음과 같습니다.

def decorator_function(original_function):
    def wrapper_function(*args, **kwargs):
        # 추가 기능 (ex: 로그 출력, 접근 권한 확인 등)
        return original_function(*args, **kwargs)  # 원래 함수 실행
    return wrapper_function
위의 wrapper_function은 original_function을 감싸는 역할을 하며, 원래 함수에 추가적인 처리를 수행합니다.

2. 데코레이터의 기본 사용법
Python에서 데코레이터를 적용할 때는 @데코레이터이름 구문을 사용합니다. @ 기호는 지정한 함수가 데코레이터로 사용된다는 의미입니다.

def my_decorator(func):
    def wrapper():
        print("함수 실행 전")
        func()
        print("함수 실행 후")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
출력 결과:

함수 실행 전
Hello!
함수 실행 후

위 코드에서 @my_decorator는 say_hello 함수에 my_decorator 데코레이터를 적용합니다. say_hello를 호출할 때 my_decorator의 wrapper 함수가 실행되고, 그 안에서 원래 say_hello 함수가 호출됩니다.

3. 여러 종류의 데코레이터
(1) 인자 전달이 가능한 데코레이터
데코레이터는 원래 함수에 전달되는 인수를 처리할 수 있습니다. *args와 **kwargs를 사용하여 가변 인수를 받을 수 있습니다.

def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Arguments passed:", args, kwargs)
        return func(*args, **kwargs)
    return wrapper

@my_decorator
def add(a, b):
    return a + b

print(add(3, 5))
출력 결과:

Arguments passed: (3, 5) {}
8

(2) 여러 데코레이터 사용
함수에 여러 데코레이터를 순차적으로 적용할 수도 있습니다. 이 경우, 아래에서 위로 차례로 적용됩니다.

def decorator1(func):
    def wrapper():
        print("Decorator 1")
        func()
    return wrapper

def decorator2(func):
    def wrapper():
        print("Decorator 2")
        func()
    return wrapper

@decorator1
@decorator2
def hello():
    print("Hello!")

hello()
출력 결과:

Decorator 1
Decorator 2
Hello!
위에서 @decorator1과 @decorator2를 적용하면 decorator1이 가장 먼저 적용됩니다.

(3) 클래스 메서드 데코레이터
클래스의 메서드에도 데코레이터를 사용할 수 있습니다. Python에서는 @classmethod와 @staticmethod 데코레이터를 통해 클래스 메서드와 정적 메서드를 정의합니다.

@classmethod: 첫 번째 인수로 클래스(cls)를 받는 메서드로, 클래스 자체에 속한 메서드를 정의합니다.
@staticmethod: 인수로 클래스나 인스턴스를 받지 않고, 독립적인 기능을 가진 메서드를 정의합니다.


class MyClass:
    @classmethod
    def class_method(cls):
        print("Class method called.")

    @staticmethod
    def static_method():
        print("Static method called.")

MyClass.class_method()  # "Class method called."
MyClass.static_method()  # "Static method called."
4. 데코레이터의 활용 예
(1) 접근 제어
사용자가 특정 조건을 만족해야 함수가 실행되도록 하는 데 사용할 수 있습니다. 예를 들어 로그인 여부를 확인하는 데코레이터:

def require_login(func):
    def wrapper(*args, **kwargs):
        if not user_logged_in():
            print("로그인이 필요합니다.")
            return
        return func(*args, **kwargs)
    return wrapper

@require_login
def view_profile():
    print("프로필 보기")

view_profile()  # 로그인 상태에 따라 다르게 동작
(2) 함수 실행 시간 측정
함수의 실행 시간을 측정해 성능을 확인할 때 유용합니다.

import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} 실행 시간: {end - start:.2f}초")
        return result
    return wrapper

@timer
def slow_function():
    time.sleep(2)

slow_function()  # "slow_function 실행 시간: 2.00초" 출력
(3) 로깅 기능 추가
함수의 입력과 출력을 로깅하여 디버깅에 활용할 수 있습니다.

def logger(func):
    def wrapper(*args, **kwargs):
        print(f"함수 {func.__name__} 호출됨 - args: {args}, kwargs: {kwargs}")
        result = func(*args, **kwargs)
        print(f"함수 {func.__name__} 결과: {result}")
        return result
    return wrapper

@logger
def add(a, b):
    return a + b

add(3, 4)

출력 결과:
csharp

함수 add 호출됨 - args: (3, 4), kwargs: {}
함수 add 결과: 7
요약
데코레이터는 코드 중복을 줄이고, 재사용 가능한 기능을 추가할 때 매우 유용합니다. 특히 로깅, 성능 측정, 접근 제어 등 다양한 경우에 활용할 수 있습니다.






