컨텍스트 관리자 (Context Managers)와 with 구문
Python에서 **컨텍스트 관리자(Context Manager)**는 리소스의 사용(열기, 사용, 닫기 등)을 관리하기 위한 프로그래밍 구조입니다. 일반적으로 with 구문과 함께 사용되며, 리소스의 생성과 정리를 자동으로 처리합니다.

컨텍스트 관리자란?
파일, 네트워크 연결, 데이터베이스 연결 등 리소스를 사용한 후에는 반드시 닫아야 합니다.
컨텍스트 관리자를 사용하면 리소스를 안전하게 열고 닫는 작업을 자동화할 수 있습니다.
try...finally 구문의 반복적인 코드를 줄이고 가독성을 높이는 데 유용합니다.
with 구문의 기본 구조
컨텍스트 관리자는 주로 with 구문을 통해 사용됩니다.


with expression [as variable]:
    # 실행 블록
expression: 컨텍스트 관리자를 반환하는 객체.
as variable: 선택적으로 컨텍스트 관리자의 반환 값을 변수로 바인딩.
# 실행 블록: 컨텍스트 관리자에서 리소스를 사용할 코드.
컨텍스트 관리자 예시
1. 파일 읽기
일반적인 파일 열기와 닫기의 코드:

# 파일 열기와 닫기 수동 처리
file = open('example.txt', 'r')
try:
    content = file.read()
    print(content)
finally:
    file.close()  # 반드시 닫아야 함
컨텍스트 관리자를 사용한 코드:

# with 구문으로 파일 자동 닫기
with open('example.txt', 'r') as file:
    content = file.read()
    print(content)
# 파일은 블록 종료 시 자동으로 닫힘
2. 데이터베이스 연결
데이터베이스 연결 및 종료도 컨텍스트 관리자를 사용하여 안전하게 처리할 수 있습니다.

컨텍스트 관리자의 작동 원리
컨텍스트 관리자 객체는 __enter__와 __exit__ 메서드를 정의하여 동작합니다.

__enter__():

with 블록이 시작될 때 호출됩니다.
리소스를 초기화하거나 설정하는 역할을 합니다.
선택적으로 리소스나 객체를 반환할 수 있습니다.
__exit__(exc_type, exc_value, traceback):

with 블록이 끝날 때 호출됩니다.
리소스를 정리하고 필요한 경우 예외를 처리합니다.
매개변수:
exc_type: 발생한 예외의 클래스(예외가 없으면 None).
exc_value: 예외의 인스턴스.
traceback: 예외의 트레이스백 객체.
예외를 처리했다면 True를 반환하여 예외를 억제할 수 있습니다.
커스텀 컨텍스트 관리자 정의
클래스를 사용한 구현

class MyContextManager:
    def __enter__(self):
        print("Entering context")
        return self  # 선택적으로 반환할 값

    def __exit__(self, exc_type, exc_value, traceback):
        if exc_type:
            print(f"Exception occurred: {exc_value}")
        print("Exiting context")
        return True  # 예외를 억제

with MyContextManager() as cm:
    print("Inside context")
    raise ValueError("An error occurred")  # 예외 발생

# 출력:
# Entering context
# Inside context
# Exception occurred: An error occurred
# Exiting context
컨텍스트 관리자를 위한 데코레이터
Python 표준 라이브러리의 contextlib 모듈은 간단한 컨텍스트 관리자를 생성할 수 있는 데코레이터를 제공합니다.

contextlib.contextmanager 데코레이터
제너레이터를 사용하여 컨텍스트 관리자를 정의할 수 있습니다.

from contextlib import contextmanager

@contextmanager
def my_context_manager():
    print("Entering context")
    try:
        yield 42  # 블록에 전달될 값
    finally:
        print("Exiting context")

with my_context_manager() as value:
    print(f"Inside context with value {value}")
# 출력:
# Entering context
# Inside context with value 42
# Exiting context

장점
리소스 관리 자동화:
코드 블록 종료 시 리소스가 자동으로 정리됩니다.
코드 가독성 향상:
try...finally 블록의 중복된 코드를 제거하고 깔끔한 코드 작성.
예외 처리 간편화:
__exit__ 메서드를 통해 예외 처리를 중앙에서 관리.
활용 사례
파일 I/O: 파일 열기 및 닫기.
데이터베이스 연결: 세션 생성 및 종료.
네트워크 소켓: 소켓 연결 및 해제.
락 관리: 스레드 락(lock) 획득 및 해제.
임시 리소스: 임시 디렉터리 생성 및 삭제.
결론
컨텍스트 관리자와 with 구문은 Python의 강력한 리소스 관리 도구입니다. 커스텀 컨텍스트 관리자를 정의하면 복잡한 리소스 관리 작업을 단순화할 수 있으며, contextlib 모듈을 사용하면 더욱 편리하게 사용할 수 있습니다.
