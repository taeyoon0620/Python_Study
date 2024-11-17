함수형 프로그래밍 (Functional Programming)
함수형 프로그래밍은 함수를 일급 객체로 간주하며, 상태 변화와 부수 효과를 최소화하는 것을 강조하는 프로그래밍 패러다임입니다. 파이썬은 엄격한 함수형 언어는 아니지만, 함수형 프로그래밍을 지원하는 기능을 많이 제공합니다.

<hr>

함수형 프로그래밍의 특징
함수는 일급 객체:

함수는 변수에 할당하거나, 다른 함수의 인자로 전달하거나, 함수에서 반환될 수 있습니다.

def add(a, b):
    return a + b

func = add  # 함수 할당
print(func(2, 3))  # 출력: 5

불변성:
함수형 프로그래밍에서는 데이터가 변경되지 않고, 항상 새로운 값을 반환합니다.

numbers = [1, 2, 3]

# 기존 리스트를 변경하지 않음
squared_numbers = list(map(lambda x: x ** 2, numbers))
print(numbers)  # 출력: [1, 2, 3]
print(squared_numbers)  # 출력: [1, 4, 9]
순수 함수 (Pure Function):

같은 입력에 대해 항상 같은 출력을 반환하며, 외부 상태를 변경하지 않는 함수입니다.

def pure_function(x):
    return x * 2  # 외부 상태 변경 없음
고차 함수 (Higher-order Function):

함수를 인자로 받거나 함수를 반환하는 함수입니다.

def higher_order(func, value):
    return func(value)

print(higher_order(lambda x: x ** 2, 5))  # 출력: 25

부수 효과 최소화:

함수 내부에서 외부 상태를 변경하지 않으며, 전역 변수 사용을 지양합니다.
파이썬에서 함수형 프로그래밍을 지원하는 주요 기능
람다 함수 (lambda):

익명 함수(이름이 없는 함수)를 생성합니다.

square = lambda x: x ** 2
print(square(5))  # 출력: 25
고차 함수:

대표적인 예는 map(), filter(), reduce()입니다.

map(): 모든 요소에 함수를 적용.

numbers = [1, 2, 3, 4]
squared = map(lambda x: x ** 2, numbers)
print(list(squared))  # 출력: [1, 4, 9, 16]
filter(): 조건을 만족하는 요소만 반환.

numbers = [1, 2, 3, 4]
evens = filter(lambda x: x % 2 == 0, numbers)
print(list(evens))  # 출력: [2, 4]
reduce(): 모든 요소를 하나로 축소.

from functools import reduce
numbers = [1, 2, 3, 4]
product = reduce(lambda x, y: x * y, numbers)
print(product)  # 출력: 24
리스트 내포 (List Comprehension):

함수를 사용하지 않고도 함수형 스타일로 작성할 수 있습니다.

numbers = [1, 2, 3, 4]
squared = [x ** 2 for x in numbers]
print(squared)  # 출력: [1, 4, 9, 16]
재귀 함수:

반복문 대신 재귀 호출로 작업을 수행합니다.

def factorial(n):
    return 1 if n == 0 else n * factorial(n - 1)

print(factorial(5))  # 출력: 120

장점
가독성: 순수 함수는 독립적으로 동작하므로 읽고 이해하기 쉽습니다.
디버깅 용이: 상태 변화가 없으므로 코드의 버그를 추적하기 쉽습니다.
병렬 처리에 적합: 불변 데이터를 사용하므로 병렬 프로그래밍에서 동기화 문제가 적습니다.

단점
복잡성 증가: 함수형 스타일이 익숙하지 않은 경우 코드가 어려워 보일 수 있습니다.
성능: 반복문에 비해 재귀 호출은 오버헤드가 있을 수 있습니다.

파이썬의 제약:
Python은 완전한 함수형 언어가 아니며, 상태 변화와 부수 효과를 피하기 어렵습니다.
함수형 프로그래밍 vs 객체지향 프로그래밍
특성	함수형 프로그래밍	객체지향 프로그래밍
데이터	불변 데이터 사용	가변 데이터 사용
구조	함수와 표현식	클래스와 객체
초점	"무엇을 해야 하는가"에 중점	"어떻게 해야 하는가"에 중점
부수 효과	최소화	상태 변경 가능

결론
파이썬의 함수형 프로그래밍은 I/O 작업, 데이터 변환, 병렬 처리와 같은 특정 작업에서 유용합니다. 그러나 파이썬은 객체지향과 절차적 프로그래밍도 지원하므로, 프로젝트의 요구 사항에 따라 적절한 프로그래밍 패러다임을 선택해야 합니다.






