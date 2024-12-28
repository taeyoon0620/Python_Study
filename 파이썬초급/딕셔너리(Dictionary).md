딕셔너리(Dictionary)란?
딕셔너리는 키-값(key-value) 쌍으로 데이터를 저장하는 자료형입니다. Python에서 가장 자주 사용되는 데이터 구조 중 하나로, Key를 통해 Value를 효율적으로 조회, 추가, 수정, 삭제할 수 있습니다.

1. 딕셔너리의 특징
키-값 쌍(Key-Value Pair) 저장

Key는 고유해야 하며, 중복될 수 없습니다.
Value는 중복 가능하고, 다양한 데이터 타입을 가질 수 있습니다.
Key는 불변(Immutable)

문자열, 숫자, 튜플처럼 변경할 수 없는 데이터 타입만 Key로 사용할 수 있습니다.
가변 자료형(Mutable)

딕셔너리는 데이터를 추가, 수정, 삭제할 수 있습니다.
정렬되지 않은 데이터 구조

Python 3.7 이상에서는 입력 순서를 유지하지만, 내부적으로 정렬되지 않은 구조로 동작합니다.
2. 딕셔너리 생성

# 빈 딕셔너리 생성
my_dict = {}

# 초기 값과 함께 생성
my_dict = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}
3. 딕셔너리 주요 연산

연산	설명	예시	결과
조회	Key로 Value 가져오기	my_dict["name"]	"Alice"
추가	새로운 Key-Value 추가	my_dict["job"] = "Developer"	{"name": "Alice", "job": "Developer"}
수정	기존 Key의 Value 변경	my_dict["age"] = 26	{"age": 26}
삭제	Key-Value 제거	del my_dict["city"]	{"name": "Alice"}
Key 존재 확인	특정 Key가 있는지 확인	"name" in my_dict	True
모든 Key 조회	모든 Key 반환	my_dict.keys()	dict_keys(['name', 'age'])
모든 Value 조회	모든 Value 반환	my_dict.values()	dict_values(['Alice', 25])
모든 쌍 조회	모든 Key-Value 쌍 반환	my_dict.items()	dict_items([('name', 'Alice'), ('age', 25)])

4. 딕셔너리 활용 예시
학생 점수 관리

scores = {
    "Alice": 90,
    "Bob": 85,
    "Charlie": 88
}
print(scores["Alice"])  # 90
scores["Bob"] = 95      # 수정
scores["David"] = 80    # 추가
del scores["Charlie"]   # 삭제
카운팅

문자열에서 각 문자의 등장 횟수를 세는 프로그램.

word = "hello"
counter = {}
for char in word:
    counter[char] = counter.get(char, 0) + 1
print(counter)  # {'h': 1, 'e': 1, 'l': 2, 'o': 1}
JSON과의 연계

딕셔너리는 JSON 데이터를 다룰 때 주로 사용됩니다.

import json
data = '{"name": "Alice", "age": 25, "city": "New York"}'
dict_data = json.loads(data)  # JSON 문자열 -> 딕셔너리
print(dict_data["name"])      # Alice

5. 딕셔너리 관련 함수
함수	설명	예시
dict.get(key, default)	Key에 해당하는 Value 반환 (없으면 기본값)	my_dict.get("job", "Not Found")
dict.update(other_dict)	다른 딕셔너리를 병합	my_dict.update({"age": 30})
dict.pop(key, default)	Key의 Value 반환 후 삭제	my_dict.pop("name")
dict.clear()	딕셔너리 비우기	my_dict.clear()
dict.copy()	딕셔너리 복사	new_dict = my_dict.copy()

6. 주의 사항
Key는 고유해야 하며, 변경 가능한 타입(리스트, 딕셔너리)은 Key로 사용할 수 없습니다.
python
코드 복사
invalid_dict = {["key"]: "value"}  # 오류 발생
Value는 중복되거나 변경 가능해도 문제 없습니다.
