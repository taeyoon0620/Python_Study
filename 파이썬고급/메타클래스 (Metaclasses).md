메타클래스 (Metaclasses)
메타클래스는 클래스를 생성하거나 수정하기 위한 클래스입니다. 즉, 클래스를 만드는 클래스라고 할 수 있습니다. 일반적으로 Python에서 클래스는 객체를 생성하는 데 사용되지만, 메타클래스는 클래스 자체를 정의하거나 동작을 제어하는 데 사용됩니다.

기본 개념
클래스는 객체다:

Python에서 클래스도 객체입니다. 모든 클래스는 메타클래스의 인스턴스입니다.
기본적으로 Python에서 모든 클래스는 type이라는 메타클래스의 인스턴스입니다.

class MyClass:
    pass

print(type(MyClass))  # 출력: <class 'type'>
type은 기본 메타클래스:

type은 메타클래스 역할을 하며, 클래스를 동적으로 생성할 수 있습니다.

# 동적으로 클래스 생성
MyClass = type('MyClass', (object,), {'x': 42})
obj = MyClass()
print(obj.x)  # 출력: 42
메타클래스를 사용하면:

클래스를 생성하는 과정에서 동작을 커스터마이징할 수 있습니다.
메타클래스 정의
사용자 정의 메타클래스는 type을 상속하여 정의합니다. 그리고 클래스를 정의할 때 metaclass 키워드를 사용해 메타클래스를 지정합니다.

기본 구조

class MyMeta(type):
    def __new__(cls, name, bases, dct):
        print(f"Creating class: {name}")
        return super().__new__(cls, name, bases, dct)

class MyClass(metaclass=MyMeta):
    pass
    
출력:
Creating class: MyClass

메타클래스의 주요 메서드
__new__(cls, name, bases, dct):

클래스를 생성하기 전에 호출됩니다.
클래스의 정의를 수정하거나 새 클래스를 반환할 수 있습니다.
매개변수:
cls: 메타클래스 자체.
name: 생성하려는 클래스의 이름.
bases: 클래스가 상속받는 부모 클래스들.
dct: 클래스의 속성 사전.
__init__(cls, name, bases, dct):

클래스가 생성된 후 초기화 단계에서 호출됩니다.
매개변수:

cls: 생성된 클래스.
name: 생성된 클래스의 이름.
bases: 상속받은 부모 클래스들.
dct: 클래스의 속성 사전.
__call__(cls, *args, **kwargs):

클래스가 호출될 때 동작을 커스터마이징할 수 있습니다.

class MyMeta(type):
    def __call__(cls, *args, **kwargs):
        print(f"Creating instance of {cls.__name__}")
        return super().__call__(*args, **kwargs)

class MyClass(metaclass=MyMeta):
    pass

obj = MyClass()
# 출력: Creating instance of MyClass
실제 사용 예시
1. 클래스 속성 검증
메타클래스를 사용하여 클래스 속성을 강제로 특정 이름으로 정의하도록 요구할 수 있습니다.

class AttributeValidator(type):
    def __new__(cls, name, bases, dct):
        if 'required_attribute' not in dct:
            raise TypeError(f"Class {name} must define 'required_attribute'")
        return super().__new__(cls, name, bases, dct)

class MyClass(metaclass=AttributeValidator):
    required_attribute = True

# 아래 코드는 TypeError 발생
# class InvalidClass(metaclass=AttributeValidator):
#     pass
2. 싱글톤 패턴 구현
싱글톤(Singleton)은 객체를 하나만 생성하도록 강제하는 디자인 패턴입니다.

class SingletonMeta(type):
    _instances = {}

    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class SingletonClass(metaclass=SingletonMeta):
    pass

obj1 = SingletonClass()
obj2 = SingletonClass()

print(obj1 is obj2)  # 출력: True
3. 클래스 생성 로깅
클래스가 생성될 때마다 로깅하는 기능을 추가할 수 있습니다.

class LoggingMeta(type):
    def __new__(cls, name, bases, dct):
        print(f"Defining class: {name}")
        return super().__new__(cls, name, bases, dct)

class MyClass(metaclass=LoggingMeta):
    pass

# 출력: Defining class: MyClass
장점
클래스 생성 과정 제어:
클래스의 동작을 정의하거나 검증할 수 있습니다.
코드 재사용성 향상:
클래스의 공통적인 동작을 메타클래스에서 처리하여 중복을 줄일 수 있습니다.
유연성 제공:
동적 클래스 생성, 속성 추가, 검증 등의 작업이 가능합니다.
단점
복잡성 증가:
메타클래스는 이해하고 디버깅하기 어렵습니다.
과도한 사용 주의:
메타클래스는 매우 강력하지만, 과도하게 사용하면 코드가 유지보수하기 어려워질 수 있습니다.
결론
메타클래스는 고급 기능이며, 클래스 생성 및 동작을 세밀하게 제어할 필요가 있을 때 사용됩니다. 일반적인 프로젝트에서는 자주 사용되지 않지만, 프레임워크나 라이브러리 개발에서 중요한 역할을 합니다. Python의 기본 메타클래스는 type이지만, 사용자 정의 메타클래스를 통해 더 복잡한 동작을 구현할 수 있습니다.
