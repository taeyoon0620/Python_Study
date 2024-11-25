파일 I/O (Input/Output)란?
파일 I/O는 파일을 읽고 쓰는 작업을 말합니다. Python은 간단하고 강력한 파일 처리 기능을 제공합니다.
파일을 읽거나 쓰기 위해 주로 open() 함수를 사용하며, 파일의 모드에 따라 다양한 작업을 수행할 수 있습니다.

1. 파일 열기 (open() 함수)
   
문법
file = open(file_name, mode)
file_name: 파일 경로(파일명 포함)
mode: 파일을 여는 모드 (읽기, 쓰기 등)
주요 모드
모드	설명
'r'	읽기 모드 (기본값). 파일이 존재해야 함.
'w'	쓰기 모드. 파일이 존재하면 덮어씀.
'x'	쓰기 모드. 파일이 존재하면 예외 발생.
'a'	추가 모드. 파일 끝에 내용 추가.
'b'	바이너리 모드. (예: 'rb', 'wb')
't'	텍스트 모드. (기본값, 예: 'rt', 'wt')
'+'	읽기 및 쓰기 모드.

파일 읽기
파일을 읽을 때는 'r' 모드를 사용합니다.

예제 1: 파일 전체 읽기

with open('example.txt', 'r') as file:
    content = file.read()
    print(content)
    
with 블록을 사용하면 파일이 자동으로 닫힙니다.
file.read()는 파일 전체를 문자열로 읽습니다.

예제 2: 파일 줄 단위 읽기

with open('example.txt', 'r') as file:
    for line in file:
        print(line.strip())  # 각 줄의 공백 제거
        
예제 3: 특정 길이만 읽기

with open('example.txt', 'r') as file:
    content = file.read(10)  # 10바이트 읽기
    print(content)
3. 파일 쓰기

파일에 데이터를 쓸 때는 'w', 'a', 'x' 모드를 사용합니다.

예제 1: 파일 덮어쓰기

with open('example.txt', 'w') as file:
    file.write("Hello, World!\n")
    file.write("This is Python.")
기존 내용은 삭제되고 새로운 내용으로 덮어씌워집니다.

예제 2: 파일 내용 추가

with open('example.txt', 'a') as file:
    file.write("\nAppending new content.")
기존 내용 뒤에 추가로 작성됩니다.

4. 파일 읽기 및 쓰기 ('r+' 모드)
예제: 읽고 쓰기

with open('example.txt', 'r+') as file:
    content = file.read()
    print("Original Content:", content)
    file.write("\nNew line added.")
    
5. 파일 존재 여부 확인
파일 작업 전, 파일이 존재하는지 확인하려면 os 모듈을 사용합니다.

import os

if os.path.exists("example.txt"):
    print("File exists.")
else:
    print("File does not exist.")
    
6. 바이너리 파일 작업
이미지, 오디오 파일 등 바이너리 파일은 'b' 모드를 사용해 처리합니다.

예제: 바이너리 파일 읽기

with open('image.png', 'rb') as file:
    data = file.read()
    print(data[:10])  # 첫 10바이트 출력
예제: 바이너리 파일 쓰기

with open('copy_image.png', 'wb') as file:
    file.write(data)  # 기존 데이터를 새로운 파일에 쓰기
7. 파일 작업에서 예외 처리
파일 작업 중 에러를 방지하려면 예외 처리를 추가합니다.

try:
    with open('example.txt', 'r') as file:
        content = file.read()
        print(content)
except FileNotFoundError:
    print("File not found.")
except IOError:
    print("An IOError occurred.")
    
8. 파일 객체의 주요 메서드
메서드	설명
read()	파일 내용 전체 또는 일부를 읽음.
readline()	한 줄씩 읽음.
readlines()	파일 전체를 읽고 각 줄을 리스트로 반환.
write(string)	문자열을 파일에 씀.
writelines(list)	리스트의 문자열을 파일에 씀.
close()	파일을 닫음 (with 블록 사용 시 자동 닫힘).

10. 파일 I/O 주의사항
파일 닫기: 파일 작업 후 반드시 닫아야 함. (자동 닫기를 위해 with 사용 권장)
데이터 덮어쓰기 주의: 'w' 모드는 기존 데이터를 삭제하므로 신중하게 사용.
파일 인코딩: 텍스트 파일 작업 시, 파일의 인코딩을 명시하는 것이 좋음.

with open('example.txt', 'r', encoding='utf-8') as file:
    content = file.read()
    
11. 결론
Python의 파일 I/O는 쉽고 강력하며, with 문을 사용하면 안전하게 작업할 수 있습니다.
텍스트 파일과 바이너리 파일 모두 효율적으로 처리할 수 있으며, os 모듈과 함께 사용하면 더 유용한 기능을 제공합니다.
