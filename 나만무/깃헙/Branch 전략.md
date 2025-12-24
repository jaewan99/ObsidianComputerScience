
### Git Flow vs GitHub Flow

**참고 자료:**

- [Git Branch 전략 개요](https://www.youtube.com/watch?v=Uszj_k0DGsg)
- [우아한형제들 기술블로그: Git Flow 실전 사용법](https://techblog.woowahan.com/2553/)

### Git Flow (전통적 접근법)

Git Flow는 5가지 브랜치를 사용합니다:
- Git Flow는 5가지 브랜치를 사용하는 복잡하지만 체계적인 전략입니다. 개발(develop)과 안정(main) 버전을 명확히 분리하여 관리합니다.
- ![[Pasted image 20251225005813.png]]
- **master** (main): 제품으로 출시될 수 있는 브랜치
- **develop**: 다음 출시 버전을 개발하는 브랜치
- **feature**: 기능을 개발하는 브랜치
- **release**: 이번 출시 버전을 준비하는 브랜치
- **hotfix**: 출시 버전에서 발생한 버그를 수정하는 브랜치

### GitHub Flow (단순화된 접근법)
- GitHub Flow는 main 브랜치에서 feature 브랜치를 생성하는 단순한 전략입니다. 간단하지만 main 브랜치가 개발(dev)과 안정(stable) 버전을 동시에 담당하여 위험할 수 있습니다.
- ![[Pasted image 20251225005747.png]]
- 간단한 브랜치 전략으로 2개의 메인 브랜치만 사용
- main에서 feature 브랜치만 생성
- **문제점**: main 브랜치가 개발(dev)과 안정(stable) 버전을 동시에 담당하여 위험할 수 있음

## 우리의 요구사항: Stable과 Dev 환경 분리

우리는 안정 버전과 개발 버전을 분리해야 합니다:

- 매주 데모를 위한 안정적인 버전 필요
- 개발 작업이 데모 기능을 망가뜨리면 안 됨
- 팀이 아직 학습 중이므로 안전망 필요

이는 Git Flow를 기반으로 사용해야 함을 의미하지만, 5가지 브랜치를 모두 사용해야 할까요?

## 우리 팀의 Git Branch 전략

### 수정된 Git Flow (Release와 Hotfix 제외)

우리는 Git Flow를 사용하지만 **release와 hotfix 브랜치는 제외**합니다.

#### Release 브랜치가 없는 이유

- **QA 팀 부재**: 별도의 릴리즈 준비 기간이 필요한 QA 팀이 없습니다
- **직접 검증**: main으로 병합하기 전 develop 브랜치에서 직접 테스트합니다

#### Hotfix 브랜치가 없는 이유

- **라이브 서비스 아님**: 실제 사용자가 있는 운영 서비스가 아닌 MVP를 개발 중입니다
- **직접 수정**: 문제 발견 시 해당 브랜치에서 직접 수정합니다
- **유연한 접근**: 긴급 수정이 필요하면 feature 브랜치를 사용합니다

### 우리의 브랜치 구조

``` JSON
damso (repository)
├── main (1개, 영구)
├── develop (1개, 영구)
└── feature (5개, 4주간 유지)
    ├── feature/보호자-대시보드
    ├── feature/AI-감정-분석
    ├── feature/영상-통화-녹화
    ├── feature/스토리북-생성
    └── feature/긴급-알림-시스템
```

**참고:** Feature 브랜치는 5가지 주요 기능을 병렬로 개발하므로 4주 개발 기간 동안 유지됩니다.