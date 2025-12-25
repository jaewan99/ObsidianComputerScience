https://shipixen.com/blog/nextjs-file-naming-best-practices
| 패턴             | 사용 사례                    | 장점                                                       | 단점                                             |
| -------------- | ------------------------ | -------------------------------------------------------- | ---------------------------------------------- |
| **PascalCase** | React 컴포넌트명, 인터페이스, 클래스명 | • React 컴포넌트를 쉽게 식별  <br>• React 규칙과 일치  <br>• 시각적으로 구분됨 | • 입력이 약간 번거로움  <br>• 특정 빌드 시스템과 충돌 가능          |
| **camelCase**  | JavaScript 변수, 함수, props | • JavaScript 표준  <br>• 작성과 읽기가 쉬움  <br>• 객체 속성에 자연스러움    | • 긴 단어는 읽기 어려움  <br>• 단어 경계가 모호할 수 있음          |
| **kebab-case** | 파일명, URL, CSS 클래스        | • URL 친화적  <br>• 가독성이 높음  <br>• 모든 시스템과 호환               | • JavaScript에서 변환 필요  <br>• import 시 추가 처리 필요  |
| **snake_case** | 상수                       | • 단어를 명확히 구분  <br>• 긴 식별자에 적합  <br>• 플랫폼 독립적             | • React 프로젝트에서 거의 사용 안 됨  <br>• 시각적으로 공간을 더 차지 |


# 네이밍 컨벤션 예시

## PascalCase


```tsx
// React 컴포넌트
const UserProfile = () => { ... }

// 인터페이스
interface UserData {
  name: string;
  age: number;
}

// 클래스
class DatabaseConnection { ... }
```

## camelCase


```tsx
// 변수
const userName = "재완";
const isLoggedIn = true;

// 함수
function getUserProfile() { ... }
const handleSubmit = () => { ... }

// Props
<Button onClick={handleClick} isDisabled={false} />
```

## kebab-case


```tsx
// 파일명
user-profile.tsx
auth-service.ts
video-call-screen.tsx

// URL
/api/user-profile
/dashboard/call-history

// CSS 클래스
.button-primary
.video-call-container
```

## snake_case

```tsx
// 상수
const MAX_RETRY_COUNT = 3;
const API_BASE_URL = "https://api.damso.com";
const DEFAULT_TIMEOUT_MS = 5000;

// 환경 변수
process.env.DATABASE_URL
process.env.AWS_REGION
```