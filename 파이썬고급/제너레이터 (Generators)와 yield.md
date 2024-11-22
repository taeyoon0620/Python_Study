제너레이터 (Generators)와 yield in Python
1. 제너레이터란?
제너레이터는 이터레이터(Iterator)를 생성하는 특별한 함수입니다. 일반 함수와 비슷하지만, 값을 반환할 때 return 대신 yield 키워드를 사용합니다. 제너레이터는 한 번에 하나씩 값을 반환하며, 필요한 순간까지 실행 상태를 유지하여 메모리를 효율적으로 사용합니다.

2. yield의 역할
yield는 함수 실행을 일시 중단하고 값을 호출자에게 반환합니다.
중단된 상태를 기억하고, 다시 호출하면 중단된 지점에서 실행을 재개합니다.
반복적으로 값을 생성할 수 있어 메모리 효율이 높습니다.
3. 제너레이터의 작동 방식
제너레이터 함수가 호출되면 제너레이터 객체를 반환합니다.
제너레이터 객체는 이터레이터로 동작하며, next() 또는 반복문에서 호출될 때마다 함수가 실행됩니다.
함수 실행 중 yield를 만나면 값을 반환하고, 실행이 멈춥니다.
다시 호출되면 이전 상태를 기억한 채 이어서 실행됩니다.
4. 제너레이터 예제

# 제너레이터 함수 정의
def count_up_to(maximum):
    count = 1
    while count <= maximum:
        yield count  # 값을 반환하고 멈춤
        count += 1

# 제너레이터 사용
counter = count_up_to(5)

# next()로 값 호출
print(next(counter))  # 출력: 1
print(next(counter))  # 출력: 2

# 반복문으로 사용
for number in counter:
    print(number)  # 출력: 3, 4, 5
5. 제너레이터의 장점
메모리 효율적:
한 번에 모든 값을 메모리에 로드하지 않고, 필요할 때만 값을 생성합니다.
큰 데이터 처리 시 유용합니다.

# 제너레이터 예제 (큰 데이터 처리)
def large_data():
    for i in range(1_000_000):
        yield i

data = large_data()
print(next(data))  # 0
print(next(data))  # 1
상태 저장:
yield는 함수의 실행 상태를 유지합니다.
재귀적인 로직을 반복문으로 간단히 대체할 수 있습니다.
6. 제너레이터 표현식
파이썬은 제너레이터를 더 간단히 만들기 위해 제너레이터 표현식을 제공합니다. 리스트 컴프리헨션과 유사하지만, 소괄호를 사용합니다.

# 리스트 컴프리헨션
squares_list = [x ** 2 for x in range(10)]  # 메모리에 모든 값을 저장

# 제너레이터 표현식
squares_gen = (x ** 2 for x in range(10))  # 값을 필요할 때 생성

print(next(squares_gen))  # 출력: 0
print(next(squares_gen))  # 출력: 1
7. 제너레이터와 이터레이터의 관계
제너레이터는 이터레이터의 한 종류입니다.
이터레이터는 __iter__()와 __next__() 메서드를 구현한 객체입니다.
제너레이터는 이 메서드들을 자동으로 구현해줍니다.

# 제너레이터로 이터레이터 동작 확인
gen = (x for x in range(3))
print(iter(gen))  # <generator object>
print(next(gen))  # 0
8. 실전 사용 예시
파일 읽기: 한 줄씩 파일을 읽으며 메모리를 절약.

def read_large_file(file_path):
    with open(file_path) as file:
        for line in file:
            yield line.strip()

for line in read_large_file("large_file.txt"):
    print(line)
무한 시퀀스 생성:

def infinite_counter():
    num = 0
    while True:
        yield num
        num += 1

counter = infinite_counter()
print(next(counter))  # 0
print(next(counter))  # 1
정리
yield는 함수 실행을 중단하고 값을 반환하며 상태를 저장합니다.
제너레이터는 메모리를 절약하면서 이터레이션 가능한 객체를 만듭니다.
대용량 데이터 처리나 무한 반복 작업에서 특히 유용합니다.
