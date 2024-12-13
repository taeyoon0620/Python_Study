
타입 힌트와 애너테이션 (Type Hints and Annotations)

1. 정의
타입 힌트(Type Hints): Python 코드에서 변수, 함수 인자, 반환 값의 데이터 타입을 명시하는 방법.
Python은 동적 타이핑 언어로, 타입을 강제하지 않지만 코드의 가독성과 유지보수성을 높이기 위해 타입 힌트를 사용할 수 있습니다.

2. 기본 문법
변수에 타입 힌트 추가
변수의 데이터 타입을 명시합니다.

x: int = 10
y: str = "Hello"
z: list[int] = [1, 2, 3]
함수에 타입 힌트 추가
인자 타입과 반환 타입 지정

def add(a: int, b: int) -> int:
    return a + b
반환 타입이 없는 경우

def greet(name: str) -> None:
    print(f"Hello, {name}")
기본값과 타입 힌트

def increment(value: int, step: int = 1) -> int:
    return value + step
3. 복잡한 타입 표현
리스트, 튜플, 딕셔너리
typing 모듈을 활용해 복잡한 타입을 표현합니다.

from typing import List, Tuple, Dict

names: List[str] = ["Alice", "Bob"]
coordinates: Tuple[float, float] = (10.5, 20.3)
scores: Dict[str, int] = {"Alice": 90, "Bob": 85}
유니언 타입 (여러 타입 허용)
Union을 사용하여 인자가 여러 타입을 가질 수 있도록 설정합니다.

from typing import Union

def get_value(data: Union[int, str]) -> str:
    return str(data)
옵셔널 타입
값이 None일 수 있는 경우 Optional 사용.

from typing import Optional

def find_user(user_id: int) -> Optional[str]:
    if user_id == 1:
        return "Alice"
    return None

4. 애너테이션 접근
타입 힌트는 런타임에 영향을 주지 않지만, __annotations__ 속성을 통해 접근할 수 있습니다.

def add(a: int, b: int) -> int:
    return a + b

print(add.__annotations__)
# {'a': <class 'int'>, 'b': <class 'int'>, 'return': <class 'int'>}

5. 타입 힌트의 이점

코드 가독성 향상
함수와 변수가 어떤 타입을 기대하는지 명확히 알 수 있음.
IDE 및 도구 지원
코드 작성 시 IDE의 자동 완성 및 오류 감지 기능 강화.
유지보수성 향상
협업 환경에서 코드의 의도를 명확히 전달.
정적 분석 가능
mypy 같은 정적 타입 검사기를 사용해 런타임 이전에 타입 관련 오류 탐지.

6. 타입 검사 도구

mypy
Python 코드를 정적으로 분석하여 타입 힌트가 올바른지 확인.

pip install mypy
사용법


mypy your_script.py

7. Python 3.10 이후의 향상된 문법
유니언 연산자 (|)
Python 3.10부터는 Union 대신 |를 사용할 수 있습니다.

def get_value(data: int | str) -> str:
    return str(data)

TypeAlias
복잡한 타입 정의를 간단히 별칭으로 설정.

from typing import List, Tuple

Coordinates: TypeAlias = List[Tuple[float, float]]

points: Coordinates = [(10.5, 20.3), (15.0, 25.0)]

8. 주의사항
타입 힌트는 강제되지 않음 (Python의 특성상).
타입 힌트를 잘못 사용하면 오히려 혼란을 초래할 수 있으므로 일관성과 명확성이 중요.
성능에 영향을 주지 않음 (런타임에 제거).

9. 예제
간단한 함수와 타입 힌트

def multiply(a: int, b: int) -> int:
    return a * b

result: int = multiply(3, 4)
print(result)
타입 검사기로 정적 타입 검사

from typing import List

def average(values: List[int]) -> float:
    return sum(values) / len(values)

print(average([1, 2, 3]))

결론
타입 힌트는 가독성, 유지보수성, 오류 예방에 유용한 도구.
Python 3.5 이후부터 사용 가능하며, 최신 버전에서는 점점 더 간결하게 사용 가능.
적극적으로 활용하면 더 견고하고 협업에 적합한 코드를 작성할 수 있음.





