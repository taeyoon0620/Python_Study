**제너레이터(Generators)**는 반복 가능한 값을 하나씩 생성하며 반환하는 Python의 특별한 함수입니다. 제너레이터는 일반 함수와 비슷하게 정의되지만, 값을 반환할 때 return 대신 yield 키워드를 사용합니다. yield는 일시적으로 함수의 상태를 저장하면서 값을 반환하고, 다음 호출 시에는 이전 상태에서 이어서 실행할 수 있도록 해줍니다.

이러한 특성 덕분에 제너레이터는 메모리를 효율적으로 사용할 수 있으며, 대량의 데이터 처리가 필요한 상황에서 성능을 개선하는 데 유리합니다.

1. 제너레이터와 yield의 기본 개념
제너레이터 함수는 일반 함수와 달리 호출해도 즉시 실행되지 않으며, 제너레이터 객체를 반환합니다. 제너레이터 객체는 반복 가능한 객체(iterable)이며, next() 함수를 통해 다음 값을 요청할 수 있습니다.

예제: 기본 제너레이터 함수
def my_generator():
    yield 1
    yield 2
    yield 3

gen = my_generator()
print(next(gen))  # 1 출력
print(next(gen))  # 2 출력
print(next(gen))  # 3 출력
출력 결과:

1
2
3
yield는 값을 반환하고 함수의 실행을 일시 중지한 후, 호출자가 요청할 때마다 멈춘 지점부터 이어서 실행합니다.

2. 제너레이터의 장점
(1) 메모리 효율성
제너레이터는 한 번에 하나의 값만 메모리에 올리므로, 큰 데이터셋을 처리할 때 메모리를 효율적으로 사용할 수 있습니다. 예를 들어, 리스트를 반환하는 함수와 비교할 때 제너레이터는 모든 값을 한꺼번에 메모리에 저장하지 않기 때문에 메모리 사용량이 크게 줄어듭니다.

(2) 무한 반복 가능
제너레이터는 모든 값을 미리 계산하지 않고 필요할 때마다 계산하여 반환하기 때문에, 무한한 개수의 값을 생성하는 것도 가능합니다.

예제: 무한 제너레이터
def infinite_counter():
    n = 1
    while True:
        yield n
        n += 1

counter = infinite_counter()
print(next(counter))  # 1 출력
print(next(counter))  # 2 출력

# 계속 호출 가능, 메모리에 무한히 큰 리스트를 할당하지 않음

3. yield의 동작 방식
yield는 값을 반환하면서 함수의 실행을 멈춥니다. 제너레이터를 다시 호출하면 이전 yield 지점에서 멈춘 부분부터 계속 실행됩니다. 이를 통해 yield는 함수 내부의 로컬 상태를 유지할 수 있습니다.

예제: yield의 로컬 상태 유지
def stateful_generator():
    n = 0
    while n < 3:
        n += 1
        yield n

gen = stateful_generator()
print(next(gen))  # 1 출력
print(next(gen))  # 2 출력
print(next(gen))  # 3 출력

# n 값이 계속 유지됨

출력 결과:

1
2
3

yield는 단순한 값을 반환하는 것 이상의 역할을 하며, 상태를 유지하면서 값을 반환하기 때문에 제너레이터가 재개될 때 상태가 초기화되지 않고 이어집니다.

4. yield from 사용법
yield from은 중첩된 제너레이터를 다룰 때 유용하며, 다른 제너레이터 또는 반복 가능한 객체를 위임해서 처리할 수 있도록 해줍니다.

예제: yield from 사용
def generator1():
    yield from [1, 2, 3]

for value in generator1():
    print(value)
    
출력 결과:

1
2
3

위의 예제에서 yield from [1, 2, 3]은 리스트의 각 요소를 차례로 반환하도록 합니다. 이를 통해 복잡한 반복 구조를 간단하게 표현할 수 있습니다.

5. 제너레이터 표현식
제너레이터 표현식은 리스트 컴프리헨션과 비슷한 문법을 사용해 간단한 제너레이터를 만들 수 있습니다. 제너레이터 표현식은 ()를 사용하며, 리스트 컴프리헨션과 달리 메모리에 모든 요소를 저장하지 않습니다.

예제: 제너레이터 표현식
gen_expr = (x * x for x in range(5))

for num in gen_expr:
    print(num)
출력 결과:

0
1
4
9
16

제너레이터 표현식은 메모리 사용이 최소화된 상태에서 값을 하나씩 생성할 수 있습니다.

6. 제너레이터 활용 예시
(1) 대량 데이터 처리
제너레이터는 대량의 데이터 또는 파일을 읽고 처리할 때 유용합니다. 파일을 한 줄씩 읽어 처리하는 경우 제너레이터를 사용하면 메모리 절약에 효과적입니다.

def read_large_file(file_path):
    with open(file_path, 'r') as file:
        for line in file:
            yield line

for line in read_large_file('large_file.txt'):
    print(line.strip())
    
(2) 시퀀스 생성
피보나치 수열이나 소수와 같은 수열을 생성하는 데 제너레이터를 사용할 수 있습니다.

def fibonacci_sequence():
    a, b = 0, 1
    while True:
        yield a
        a, b = b, a + b

fib = fibonacci_sequence()
for _ in range(10):
    print(next(fib))
    
출력 결과:

0
1
1
2
3
5
8
13
21
34

요약
제너레이터는 yield를 사용해 값을 하나씩 생성하며, 필요할 때마다 값을 반환하는 함수입니다.
yield는 함수의 상태를 저장하고, 호출될 때마다 이어서 실행을 재개할 수 있습니다.
메모리를 절약할 수 있어 대용량 데이터 처리에 유용하며, 무한 반복 생성과 같은 시나리오에서 매우 유용합니다.
yield from을 통해 다른 반복 가능한 객체에 위임할 수 있고, 제너레이터 표현식을 사용하면 간단하게 생성할 수도 있습니다.
