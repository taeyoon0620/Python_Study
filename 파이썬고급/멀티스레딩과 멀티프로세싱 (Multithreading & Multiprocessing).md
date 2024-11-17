멀티스레딩(Multithreading)과 멀티프로세싱(Multiprocessing)은 프로그램의 병렬성과 동시성을 구현하기 위한 두 가지 주요 방식입니다. 두 방법 모두 작업을 동시에 실행하여 성능을 향상시키는 것을 목표로 하지만, 작동 방식과 사용 사례는 다릅니다.

멀티스레딩 (Multithreading)
멀티스레딩은 **하나의 프로세스 내에서 여러 스레드(Thread)**를 실행하는 방식입니다. 스레드는 프로세스 내의 경량 실행 단위로, 메모리를 공유하며 독립적으로 실행됩니다.

<hr>

특징
공유 메모리:
모든 스레드는 동일한 프로세스의 메모리를 공유합니다.
전역 변수나 객체를 쉽게 공유할 수 있어 데이터 교환이 빠릅니다.
경량 실행 단위:
스레드는 프로세스보다 생성 및 관리 비용이 적습니다.
병렬성 제한:
Python에서는 Global Interpreter Lock (GIL) 때문에 멀티스레딩이 완전한 병렬 실행이 아니라 동시성만 제공됩니다.

장점
빠른 스위칭: 스레드 간 전환이 상대적으로 빠릅니다.
메모리 효율적: 같은 메모리를 공유하므로 메모리 사용량이 적습니다.
I/O 바운드 작업에 유리: 파일 입출력, 네트워크 요청 등 대기 시간이 긴 작업에 적합합니다.

단점
GIL 문제(Python): Python의 GIL로 인해 멀티스레딩은 CPU 바운드 작업에서 효율적이지 못합니다.
동기화 문제: 공유 메모리를 사용하는 만큼, Race Condition이나 Deadlock 같은 문제가 발생할 수 있습니다.

코드 예제: 멀티스레딩

import threading
import time

def task(name):
    for i in range(5):
        print(f"Thread {name} is running...")
        time.sleep(1)

thread1 = threading.Thread(target=task, args=("A",))
thread2 = threading.Thread(target=task, args=("B",))

thread1.start()
thread2.start()

thread1.join()
thread2.join()
print("All threads completed.")
멀티프로세싱 (Multiprocessing)
멀티프로세싱은 **여러 프로세스(Process)**를 실행하는 방식입니다. 각 프로세스는 독립적인 메모리 공간을 가지고 실행됩니다.

특징
독립 메모리:
각 프로세스는 자신만의 메모리를 가지고 실행되므로 데이터 공유가 어렵습니다.

진정한 병렬성:
GIL의 영향을 받지 않으며, 여러 CPU 코어를 활용해 병렬 실행이 가능합니다.

프로세스 간 통신 필요:
데이터를 공유하려면 Queue나 Pipe 같은 통신 메커니즘을 사용해야 합니다.

장점
CPU 바운드 작업에 유리: 여러 프로세스를 통해 병렬 처리가 가능하여 CPU 집약적인 작업에서 효율적입니다.
안정성: 각 프로세스가 독립적이므로 하나의 프로세스가 실패해도 다른 프로세스에는 영향을 주지 않습니다.

단점
메모리 소비: 각 프로세스가 독립적인 메모리를 사용하므로 메모리 사용량이 많습니다.
프로세스 생성 비용: 프로세스 생성과 관리가 스레드보다 비용이 더 큽니다.
데이터 공유 어려움: 프로세스 간 통신이 추가적인 복잡성을 초래합니다.

코드 예제: 멀티프로세싱

import multiprocessing
import time

def task(name):
    for i in range(5):
        print(f"Process {name} is running...")
        time.sleep(1)

process1 = multiprocessing.Process(target=task, args=("A",))
process2 = multiprocessing.Process(target=task, args=("B",))

process1.start()
process2.start()

process1.join()
process2.join()
print("All processes completed.")

멀티스레딩과 멀티프로세싱 비교
특성	멀티스레딩	멀티프로세싱
메모리 공유	동일한 프로세스 메모리 공유	각 프로세스는 독립적인 메모리 사용
병렬성	GIL로 인해 제한적	진정한 병렬성 제공
성능	I/O 바운드 작업에 유리	CPU 바운드 작업에 적합
생성 비용	상대적으로 적음	상대적으로 큼
안정성	하나의 스레드 문제로 전체 프로세스 영향	독립적이므로 안정성이 높음
데이터 공유	간단 (전역 변수 사용)	복잡 (Queue, Pipe 등 필요)

사용 사례
멀티스레딩:
네트워크 서버: 동시 접속 처리
파일 다운로드: 여러 파일을 동시에 다운로드
웹 스크래핑: 여러 URL을 동시에 처리
멀티프로세싱:
이미지 처리: 여러 이미지를 동시에 필터링
데이터 분석: 대규모 데이터 처리
머신 러닝: 모델 학습 시 여러 코어 활용

결론
I/O 바운드 작업: 멀티스레딩이 효율적입니다.
CPU 바운드 작업: 멀티프로세싱이 적합합니다.
GIL의 제약이 없는 언어(JAVA, C++)에서는 멀티스레딩으로 병렬성을 쉽게 구현할 수 있지만, Python에서는 작업의 특성과 병렬성 요구 사항에 따라 멀티스레딩과 멀티프로세싱을 적절히 선택해야 합니다.
