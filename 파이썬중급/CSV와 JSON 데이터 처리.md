CSV와 JSON 데이터 처리
1. CSV 데이터 처리
1) CSV란?
Comma-Separated Values의 약자로, 데이터를 쉼표(,)로 구분하여 저장하는 파일 형식.
행은 줄바꿈으로 구분되고, 열은 쉼표로 구분됩니다.
데이터 분석 및 데이터 교환에 자주 사용됩니다.
2) Python에서 CSV 처리
Python은 csv 모듈을 통해 CSV 파일을 읽고 쓸 수 있습니다.

a. CSV 파일 읽기

import csv

# CSV 파일 읽기
with open('data.csv', mode='r', encoding='utf-8') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
csv.reader: CSV 파일을 읽어 각 행을 리스트로 반환.
b. CSV 파일 쓰기

import csv

data = [
    ['Name', 'Age', 'City'],
    ['Alice', 25, 'New York'],
    ['Bob', 30, 'San Francisco']
]

# CSV 파일 쓰기
with open('data.csv', mode='w', encoding='utf-8', newline='') as file:
    writer = csv.writer(file)
    writer.writerows(data)
csv.writer: 데이터를 CSV 형식으로 작성.
writerows: 여러 행을 한 번에 작성.
c. CSV 파일을 딕셔너리 형태로 읽기

import csv

with open('data.csv', mode='r', encoding='utf-8') as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row)  # {'Name': 'Alice', 'Age': '25', 'City': 'New York'}
DictReader: 각 행을 딕셔너리로 변환. CSV의 첫 번째 행(헤더)이 키로 사용됩니다.
d. CSV 파일을 딕셔너리 형태로 쓰기

import csv

data = [
    {'Name': 'Alice', 'Age': 25, 'City': 'New York'},
    {'Name': 'Bob', 'Age': 30, 'City': 'San Francisco'}
]

with open('data.csv', mode='w', encoding='utf-8', newline='') as file:
    writer = csv.DictWriter(file, fieldnames=['Name', 'Age', 'City'])
    writer.writeheader()  # 헤더 작성
    writer.writerows(data)
DictWriter: 딕셔너리를 CSV 형식으로 작성.
writeheader: 헤더(필드 이름) 작성.
2. JSON 데이터 처리
1) JSON이란?
JavaScript Object Notation의 약자로, 데이터를 키-값 쌍으로 표현하는 경량 데이터 형식.
사람이 읽기 쉽고, 기계가 파싱 및 생성하기 쉬움.
웹 애플리케이션에서 데이터 교환에 널리 사용됩니다.
JSON 예시

{
    "name": "Alice",
    "age": 25,
    "city": "New York",
    "skills": ["Python", "JavaScript"]
}
2) Python에서 JSON 처리
Python은 json 모듈을 통해 JSON 데이터를 다룰 수 있습니다.

a. JSON 파일 읽기

import json

# JSON 파일 읽기
with open('data.json', mode='r', encoding='utf-8') as file:
    data = json.load(file)
    print(data)  # 딕셔너리로 반환
json.load: JSON 파일을 읽어서 Python의 딕셔너리로 변환.
b. JSON 문자열 읽기

import json

json_string = '{"name": "Alice", "age": 25, "city": "New York"}'
data = json.loads(json_string)
print(data)  # {'name': 'Alice', 'age': 25, 'city': 'New York'}
json.loads: JSON 문자열을 Python의 딕셔너리로 변환.
c. JSON 파일 쓰기

import json

data = {
    "name": "Alice",
    "age": 25,
    "city": "New York",
    "skills": ["Python", "JavaScript"]
}

# JSON 파일 쓰기
with open('data.json', mode='w', encoding='utf-8') as file:
    json.dump(data, file, indent=4)  # 보기 좋은 형식으로 저장
json.dump: Python 객체를 JSON 파일로 저장.
indent: 보기 좋게 들여쓰기 설정.
d. JSON 문자열 쓰기

import json

data = {
    "name": "Alice",
    "age": 25,
    "city": "New York",
    "skills": ["Python", "JavaScript"]
}

# JSON 문자열로 변환
json_string = json.dumps(data, indent=4)
print(json_string)
json.dumps: Python 객체를 JSON 문자열로 변환.

3. CSV와 JSON 비교
특징	CSV	JSON
형식	단순 텍스트 (행과 열)	키-값 쌍, 중첩 가능
표현력	구조가 단순함	복잡한 계층 구조 표현 가능
사용 용도	테이블 형식 데이터	비정형 데이터, 객체 저장
파싱 난이도	비교적 쉬움	비교적 복잡함
데이터 크기	상대적으로 작음	상대적으로 큼
읽기/쓰기 도구	csv 모듈	json 모듈
4. CSV와 JSON 변환
CSV → JSON 변환

import csv
import json

# CSV 읽기
csv_file = 'data.csv'
json_file = 'data.json'

data = []
with open(csv_file, mode='r', encoding='utf-8') as file:
    reader = csv.DictReader(file)
    for row in reader:
        data.append(row)

# JSON 저장
with open(json_file, mode='w', encoding='utf-8') as file:
    json.dump(data, file, indent=4)
JSON → CSV 변환

import csv
import json

# JSON 읽기
json_file = 'data.json'
csv_file = 'data.csv'

with open(json_file, mode='r', encoding='utf-8') as file:
    data = json.load(file)

# CSV 저장
with open(csv_file, mode='w', encoding='utf-8', newline='') as file:
    writer = csv.DictWriter(file, fieldnames=data[0].keys())
    writer.writeheader()
    writer.writerows(data)

5. 요약
CSV: 테이블 형식의 데이터를 다룰 때 적합.
JSON: 계층 구조나 복잡한 데이터를 다룰 때 적합.
Python의 csv와 json 모듈을 사용하면 두 형식 간 변환이 용이.
