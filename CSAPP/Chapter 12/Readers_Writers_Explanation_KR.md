# Readers-Writers 문제: Reader 코드에서 P, V(&mutex)를 두 번 사용하는 이유

---

## 🧩 세마포어의 목적

- **`mutex`** — 공유 변수 `readcnt`의 접근을 보호하기 위해 사용됨.  
  (현재 읽고 있는 reader의 수를 추적함)
- **`w`** — **reader와 writer 간의 상호 배제(mutual exclusion)** 를 보장함.  
  즉, 여러 reader는 동시에 읽을 수 있지만, writer는 혼자만 접근해야 함.

---

## 🔒 왜 `mutex`를 두 번 사용하는가?

`P(&mutex)`와 `V(&mutex)`가 **읽기 전과 읽기 후**에 모두 등장합니다.  
이건 중복이 아니라, **각기 다른 목적의 `readcnt` 접근 보호**를 위한 것입니다.

아래 코드 부분을 단계별로 살펴봅시다.

---

### 1️⃣ 읽기 전 (Entry Section)

```c
P(&mutex);          // readcnt를 안전하게 수정하기 위해 잠금
readcnt++;
if (readcnt == 1)   // 첫 번째 reader라면
    P(&w);           // writer 차단
V(&mutex);          // readcnt 수정 완료, 잠금 해제
```

- 한 번에 한 reader만 `readcnt`를 수정할 수 있게 함.  
- 첫 번째 reader가 들어올 때 `w`를 잠가 writer가 접근하지 못하게 함.  
- 그 후 `mutex`를 해제해 다른 reader도 진입할 수 있도록 함.

👉 이렇게 하면 여러 reader가 동시에 읽을 수 있습니다.

---

### 2️⃣ 읽기 후 (Exit Section)

```c
P(&mutex);          // 다시 readcnt를 안전하게 수정하기 위해 잠금
readcnt--;
if (readcnt == 0)   // 마지막 reader라면
    V(&w);           // writer에게 접근 허용
V(&mutex);          // readcnt 수정 완료, 잠금 해제
```

- Reader가 읽기를 마치면, 다시 `readcnt`를 수정해야 하므로 `mutex`로 보호.  
- 마지막 reader가 나갈 때, `V(&w)`를 호출하여 writer가 접근할 수 있게 함.

---

### 💡 왜 읽는 동안 `mutex`를 계속 잠그지 않는가?

만약 읽기 전체 동안 `mutex`를 유지한다면, **하나의 reader만 읽을 수 있게 됩니다.**  
즉, 여러 reader가 동시에 읽는 병렬성을 잃게 됩니다.  

그래서 `readcnt` 수정 시에만 잠그고,  
읽기 자체는 잠금을 해제한 상태에서 수행합니다.

---

## ✅ 요약

| 구간 | `P/V(&mutex)`의 목적 | 필요한 이유 |
|------|-----------------------|--------------|
| **읽기 전** | `readcnt` 증가를 안전하게 보호, 첫 reader가 writer 차단 | `readcnt`를 올바르게 관리하고 첫 번째 reader를 식별 |
| **읽기 후** | `readcnt` 감소를 안전하게 보호, 마지막 reader가 writer 허용 | `readcnt`를 올바르게 관리하고 마지막 reader를 식별 |

결국 `mutex` 세마포어는 **두 번** 사용되지만,  
각각 **entry section**과 **exit section**에서 **서로 다른 시점의 보호**를 담당합니다.

---

## 🧠 요약 그림

![[pastedimage:readers-writers-diagram.png]]

---

## ✍️ 핵심 요약

- `mutex`는 `readcnt`를 보호하기 위한 **reader 간의 상호 배제**용.
- `w`는 **reader와 writer 간의 상호 배제**용.
- `mutex`는 읽기 전체를 잠그는 것이 아니라, **readcnt를 수정할 때만 잠금.**
- 덕분에 여러 reader가 동시에 읽을 수 있고, writer는 reader가 없을 때만 접근 가능.

---

## 📘 추가 설명: writer 코드 (참고)

```c
void writer(void) {
    while (1) {
        P(&w);           // writer는 reader와 상호 배제
        /* Writing happens here */
        V(&w);
    }
}
```

- writer는 `w` 세마포어 하나만 사용합니다.  
- reader가 하나라도 있으면 `w`가 잠겨 writer는 대기합니다.  
- reader가 모두 나가면 (`readcnt == 0` → `V(&w)`), writer가 실행됩니다.

---

이로써 `P,V(&mutex)`가 두 번 등장하는 이유는 명확합니다.  
**하나는 들어올 때의 `readcnt` 보호, 다른 하나는 나갈 때의 `readcnt` 보호**입니다.
