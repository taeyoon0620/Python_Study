예외 처리 (Exception Handling)
예외 처리는 프로그램 실행 중 발생하는 오류를 감지하고, 이를 처리하여 프로그램이 갑작스럽게 종료되지 않도록 하는 기법입니다. Python에서는 try-except 구문을 사용해 예외를 처리하며, 특정 상황에서 발생할 수 있는 오류를 예측하여 적절히 대응할 수 있습니다.

1. 기본 개념
예외(Exception): 프로그램 실행 중에 발생하는 오류를 뜻하며, 런타임(runtime) 오류라고도 합니다.
예외 처리의 목적:
프로그램의 비정상 종료 방지
오류에 대한 사용자 친화적인 메시지 제공
안정적인 시스템 운영 유지
2. Python의 예외 처리 구조
Python에서 예외를 처리하기 위해 사용하는 기본 구조는 다음과 같습니다.

try-except 구문

try:
    # 예외가 발생할 가능성이 있는 코드
except 예외_타입:
    # 예외 발생 시 실행할 코드
예제

try:
    result = 10 / 0  # ZeroDivisionError 발생
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")  # 예외 처리
3. 예외 처리의 구성 요소
1) try
예외 발생 가능성이 있는 코드를 작성하는 블록입니다.
오류가 발생하면 해당 블록의 실행을 중단하고 except로 이동합니다.
2) except
특정 예외가 발생했을 때 실행할 코드를 작성하는 블록입니다.
발생한 예외의 유형에 따라 다르게 처리할 수 있습니다.

try:
    value = int(input("숫자를 입력하세요: "))
    print(10 / value)
except ValueError:
    print("올바른 숫자를 입력하세요.")  # 숫자가 아닌 값을 입력한 경우 처리
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")   # 0을 입력한 경우 처리
3) else
예외가 발생하지 않은 경우 실행되는 블록입니다.

try:
    value = int(input("숫자를 입력하세요: "))
    print(10 / value)
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
else:
    print("정상적으로 나누기가 수행되었습니다.")  # 예외가 없을 경우 실행
4) finally
예외 발생 여부와 상관없이 항상 실행되는 블록입니다.
주로 자원 해제(파일 닫기, 데이터베이스 연결 종료 등)에 사용됩니다.

try:
    file = open("example.txt", "r")
    data = file.read()
except FileNotFoundError:
    print("파일을 찾을 수 없습니다.")
finally:
    print("파일을 닫습니다.")
    file.close()  # 파일 자원 해제
4. 예외의 종류
Python에서 제공하는 주요 내장 예외는 다음과 같습니다.

예외	설명
ZeroDivisionError	0으로 나누기를 시도할 때 발생
ValueError	데이터 타입이 잘못되었을 때 발생
TypeError	연산이나 함수의 데이터 타입이 잘못되었을 때
IndexError	리스트 등의 인덱스 범위를 벗어났을 때 발생
KeyError	딕셔너리에서 존재하지 않는 키를 참조할 때
FileNotFoundError	파일을 찾을 수 없을 때 발생
ImportError	모듈을 가져올 수 없을 때 발생
예제

try:
    data = [1, 2, 3]
    print(data[5])  # IndexError 발생
except IndexError:
    print("리스트 인덱스가 범위를 벗어났습니다.")
5. 사용자 정의 예외
Python에서는 기본 제공 예외 외에도 사용자 정의 예외를 만들 수 있습니다.

사용자 정의 예외 생성
예외 클래스는 반드시 Exception 클래스를 상속해야 합니다.
필요에 따라 __init__ 메서드를 오버라이딩하여 추가 정보를 포함할 수 있습니다.

class NegativeNumberError(Exception):
    def __init__(self, value):
        super().__init__(f"양수만 허용됩니다. 입력된 값: {value}")
        self.value = value

try:
    number = int(input("양수를 입력하세요: "))
    if number < 0:
        raise NegativeNumberError(number)  # 사용자 정의 예외 발생
except NegativeNumberError as e:
    print(e)  # 예외 메시지 출력
6. 다중 예외 처리
하나의 except 블록에서 여러 예외를 동시에 처리할 수도 있습니다.

try:
    x = int(input("숫자를 입력하세요: "))
    result = 10 / x
except (ValueError, ZeroDivisionError) as e:
    print(f"예외가 발생했습니다: {e}")
7. 예외 다시 발생시키기
이미 처리된 예외를 다시 발생시키고 싶을 때는 raise 키워드를 사용합니다.

try:
    raise ValueError("잘못된 값입니다.")
except ValueError as e:
    print("예외 처리 중...")
    raise  # 예외를 다시 발생시킴

8. 예외 처리의 좋은 활용 방법
예외 처리 남용 방지: 코드 논리로 해결 가능한 문제는 예외 처리로 해결하지 않음.
구체적인 예외 처리: 광범위한 예외(Exception) 대신 구체적인 예외를 처리.
파일/자원 정리: finally 블록에서 자원 정리를 반드시 수행.
로그 사용: 발생한 예외 정보를 로깅하여 문제 원인 파악.

9. 정리
예외 처리는 예상치 못한 오류로부터 프로그램을 보호하고 안정성을 높이는 도구입니다.
Python의 try-except 구문과 finally, else 블록을 활용하면 유연한 오류 처리가 가능합니다.
사용자 정의 예외를 통해 더 의미 있는 에러 처리를 설계할 수 있습니다.
