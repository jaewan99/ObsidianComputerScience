commit convention
- https://www.conventionalcommits.org/ko/v1.0.0/#%ea%b7%9c%ea%b2%a9

git branch
- https://www.youtube.com/watch?v=Uszj_k0DGsg
 - git flow
	 - https://techblog.woowahan.com/2553/
	 - 깃 플로우가 쓰는 5섯가지 보조 브랜치들
	 - master : 제품으로 출시될 수 있는 브랜치
	- develop : 다음 출시 버전을 개발하는 브랜치
	- feature : 기능을 개발하는 브랜치
	- release : 이번 출시 버전을 준비하는 브랜치
	- hotfix : 출시 버전에서 발생한 버그를 수정 하는 브랜치


 - github flow
	 - 간단한 branch 전략
	 - 2개 메인 브렌치 - feature branch만 생성
	 - 문제는 main 브랜치가 dev랑 stable을 둘다 사용
 - 필수조건
	 - stable이랑 dev는 무조건 분리
		 - 그러면 gitflow을 써야함
			 - 하지만 굳이 다 써야할까?

우리 팀 깃 브랜치 전략
- git flow을 쓰지만 release랑 hotfix branch가 없다
	- why?
		- 일단 QA팀이 없어서 release을 따로 관리할 필요가 없다 - main 브랜치로 가기전 최종 확인 (버그있는지 등등)
		- 저희가 지금 live 서비스를 하는게 아니라 따로 hotfix도 할필요가 없다. - 사용중 문제가 있으면 해당 branch에 직접 변경 및 push
- 우리의 git branch

````JSON

damso (repository)
├── main (1개, 영구)
├── develop (1개, 영구)
└── feature (5개, 영구)
    ├── feature/보호자-대시보드
    ├── feature/AI-감정-분석
    ├── feature/영상-통화-녹화
    ├── feature/스토리북-생성
    └── feature/긴급-알림-시스템
    
a. feature에서 매번 push 할때
a.1 Lint 검사 - format 검사
a.2 Unit test
a.3 build 확인

화요일날에 저희가 했던 것들
b. develop으로 push 할때
b.1 Lint
b.2 유닛 테스트
b.3 통합 테스트
b.4 E2E 테스트
b.5 빌드
b.6 staging 환경 배포

````