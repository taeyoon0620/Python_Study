리스트(List)
리스트는 Python에서 가장 많이 사용되는 데이터 구조로, 변경 가능한(Mutable) 순서가 있는 데이터의 집합입니다.
리스트는 대괄호 []를 사용하며, 다양한 자료형을 함께 저장할 수 있습니다.

특징
변경 가능: 추가, 수정, 삭제가 가능.
순서 유지: 삽입 순서대로 요소를 관리.
중복 허용: 동일한 값이 여러 번 저장 가능.
다양한 데이터 타입 저장 가능.
리스트 생성

# 빈 리스트 생성
empty_list = []

# 요소가 있는 리스트
numbers = [1, 2, 3, 4]
mixed_list = [1, "hello", 3.14, True]

print(numbers)      # 출력: [1, 2, 3, 4]
print(mixed_list)   # 출력: [1, 'hello', 3.14, True]
리스트의 주요 연산
인덱싱
특정 위치의 요소 접근.
인덱스는 0부터 시작.

numbers = [10, 20, 30]
print(numbers[0])  # 출력: 10
print(numbers[-1]) # 출력: 30 (뒤에서 첫 번째)
슬라이싱
리스트의 일부를 가져옴.

numbers = [10, 20, 30, 40, 50]
print(numbers[1:4])  # 출력: [20, 30, 40]
추가
append(): 리스트 끝에 요소 추가.
insert(): 특정 위치에 요소 삽입.
extend(): 리스트 병합.

numbers = [1, 2, 3]
numbers.append(4)         # [1, 2, 3, 4]
numbers.insert(1, 10)     # [1, 10, 2, 3, 4]
numbers.extend([5, 6])    # [1, 10, 2, 3, 4, 5, 6]
삭제
remove(): 특정 값을 삭제.
pop(): 특정 인덱스의 값을 제거 후 반환.
clear(): 리스트의 모든 요소 삭제.

numbers = [1, 2, 3, 4]
numbers.remove(2)   # [1, 3, 4]
numbers.pop(1)      # [1, 4]
numbers.clear()     # []
정렬 및 뒤집기
sort(): 오름차순 정렬.
reverse(): 요소 순서 뒤집기.

numbers = [3, 1, 4, 2]
numbers.sort()        # [1, 2, 3, 4]
numbers.reverse()     # [4, 3, 2, 1]
활용 예
리스트 내포 (Comprehension)
간결하게 리스트를 생성.

squares = [x**2 for x in range(5)]  # [0, 1, 4, 9, 16]
반복문과 함께 사용

numbers = [1, 2, 3, 4]
for num in numbers:
    print(num)  # 1, 2, 3, 4 출력
리스트는 데이터의 저장, 조작, 반복 처리에 유용한 자료형입니다
