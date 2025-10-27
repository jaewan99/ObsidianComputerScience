# 가비지 컬렉션 (Garbage Collection)

[48:01](https://www.youtube.com/watch?v=z-Vp5W1qHK8#t=48:01.70) 
- 가비지 컬렉션
    - 메모리 관리자는 언제 메모리를 해제할 수 있는지 어떻게 아는가?
        - 일반적으로 어떤 메모리가 미래에 사용될지는 알 수 없다. (조건문 등에 따라 다름)
        - 그러나 특정 블록에 포인터가 하나도 없다면, 해당 블록은 더 이상 사용되지 않는다고 판단할 수 있다.
    - 포인터에 대한 가정
        - 메모리 관리자는 포인터와 비포인터를 구분할 수 있다.
            - C 언어에서는 불가능하다. 포인터는 단순히 정수값이기 때문이다.
        - 모든 포인터는 블록의 시작을 가리킨다.
            - C에서는 항상 그런 것은 아니다. 포인터가 블록 중간을 가리킬 수도 있다.
        - 포인터를 숨길 수 없다. (예: int로 캐스팅 후 다시 포인터로 변환)

[50:20](https://www.youtube.com/watch?v=z-Vp5W1qHK8#t=50:20.78) 
- 고전적인 GC 알고리즘
    - Mark-and-sweep 수집 (McCarthy, 1960)
        - 블록을 이동시키지 않음 (단, "압축" 시에는 이동 가능)
    - Reference counting (Collins, 1960)
        - 블록을 이동시키지 않음
    - Copying collection (Minsky, 1963)
        - 블록을 이동시킴
    - Generational Collectors (Lieberman and Hewitt, 1983)
        - 수명에 따른 수집
            - 대부분의 할당은 금방 가비지가 됨
            - 따라서 최근에 할당된 메모리 영역에 집중
    - 참고: Jones and Lin, *Garbage Collection: Algorithms for Automatic Dynamic Memory*, John Wiley & Sons, 1996.

[51:08](https://www.youtube.com/watch?v=z-Vp5W1qHK8#t=51:08.33) 
- 메모리를 그래프로 보기
    - 메모리를 방향 그래프로 표현
        - 각 힙 블록은 그래프의 노드
        - 각 포인터는 엣지
        - 힙 외부에서 힙 내부를 가리키는 포인터는 루트 노드 (예: 레지스터, 스택, 전역 변수)
        - 루트에서 시작해 포인터를 따라갈 수 있는 모든 블록은 도달 가능
        - 도달할 수 없는 노드는 가비지임 (프로그램에서 더 이상 필요 없음)

- Mark and Sweep 수집
    - malloc/free 위에 구현 가능
        - malloc으로 할당하다가 공간이 부족해지면 GC 실행
    - 공간이 부족할 때:
        - 각 블록 헤더에 마크 비트를 사용
        - **Mark 단계**: 루트에서 시작해 모든 도달 가능한 블록에 마크 비트를 설정
        - **Sweep 단계**: 마크되지 않은 블록을 해제

[57:02](https://www.youtube.com/watch?v=z-Vp5W1qHK8#t=57:02.29) 
- 단순한 구현을 위한 가정
    - 애플리케이션
        - new(n): 크기 n의 새 블록을 생성하고 0으로 초기화
        - read(b, i): 블록 b의 i번째 위치 읽기
        - write(b, i, v): 블록 b의 i번째 위치에 값 v 쓰기
    - 각 블록에는 헤더 단어가 존재 (b[-1]로 접근)
    - 가비지 컬렉터가 사용하는 명령:
        - is_ptr(p): p가 포인터인지 판별
        - length(b): 블록 b의 길이 반환
        - get_roots(): 모든 루트 반환

[1:00:16](https://www.youtube.com/watch?v=z-Vp5W1qHK8#t=1:00:16.66) 
- C에서의 보수적(Conservative) Mark & Sweep
    - is_ptr()은 단어가 메모리 블록을 가리키는지 확인
    - 그러나 C 포인터는 블록 중간을 가리킬 수도 있음
    - 따라서 블록의 시작 주소를 균형 이진 트리로 관리

[1:02:03](https://www.youtube.com/watch?v=z-Vp5W1qHK8#t=1:02:03.45) 
- 메모리 관련 위험 및 함정
    - 잘못된 포인터 역참조
    - 초기화되지 않은 메모리 읽기
    - 메모리 덮어쓰기
    - 존재하지 않는 변수 참조
    - 중복 해제(double free)
    - 해제된 블록 참조
    - 블록 해제 실패

[1:04:05](https://www.youtube.com/watch?v=z-Vp5W1qHK8#t=1:04:05.65) 
- C 연산자 및 버그 예시
    - malloc은 0으로 초기화된 값을 반환하지 않음
    - int와 포인터 크기를 동일하게 가정하면 오류 발생
    - 버퍼 크기 확인 누락
    - 잘못된 포인터 산술 연산 (예: 4 대신 16 증가)
    - *(size--)와 같은 잘못된 사용

- 메모리 버그 해결
    - **디버거(gdb)**: 잘못된 포인터 역참조 탐지에 유용
    - **데이터 구조 일관성 검사기**: 오류 발생 시 메시지 출력
    - **valgrind**: 실행 시 모든 메모리 접근 검사
    - **glibc malloc 검사 코드**: 환경 변수 `MALLOC_LOC_CHECK=3` 설정 시 활성화
