# 코드 포맷팅 설정 가이드

담소 프로젝트의 코드 스타일 통일을 위한 설정 파일 모음

---

## 📂 파일 구조

각 저장소(backend, mobile-app, guardian-dashboard, rtc-services, ai-services)에 추가:
```
repo/
├── .editorconfig
├── .prettierrc
└── .vscode/
    ├── extensions.json
    └── settings.json
```

---

## 1️⃣ .prettierrc

**TypeScript/JavaScript 코드 자동 포맷팅 규칙**
```json
{
  "semi": true,
  "singleQuote": true,
  "trailingComma": "all",
  "printWidth": 80,
  "tabWidth": 2,
  "endOfLine": "lf",
  "bracketSpacing": true,
  "arrowParens": "avoid"
}
```

### 설정 의미

- `semi: true` → 세미콜론 사용 `;`
- `singleQuote: true` → 작은따옴표 사용 `'hello'`
- `trailingComma: "all"` → 마지막 쉼표 추가 `{ a, b, }`
- `printWidth: 80` → 한 줄 최대 80자
- `tabWidth: 2` → 들여쓰기 2칸
- `endOfLine: "lf"` → Unix 스타일 줄바꿈
- `arrowParens: "avoid"` → 화살표 함수 괄호 생략 `x => x`

---

## 2️⃣ .editorconfig

**모든 에디터에서 동작하는 기본 설정**
```editorconfig
# .editorconfig
root = true

[*]
end_of_line = lf
insert_final_newline = true
charset = utf-8
trim_trailing_whitespace = true

# JavaScript/TypeScript (Next.js, NestJS, React Native)
[*.{js,jsx,ts,tsx}]
indent_style = space
indent_size = 2

# Python (optional, for ai-services)
[*.py]
indent_style = space
indent_size = 4

# JSON/YAML
[*.{json,yml,yaml}]
indent_style = space
indent_size = 4

# Markdown (preserve trailing spaces for line breaks)
[*.md]
trim_trailing_whitespace = false
```

### 파일 타입별 설정

| 파일 타입 | 들여쓰기 | 비고 |
| --- | --- | --- |
| TypeScript/JavaScript | 스페이스 2칸 | - |
| Python | 스페이스 4칸 | PEP 8 표준 |
| JSON/YAML | 스페이스 4칸 | - |
| Markdown | - | 줄 끝 공백 유지 |

---

## 3️⃣ .vscode/extensions.json

**팀원에게 권장 확장 프로그램 자동 제안**

### TypeScript 저장소용 (backend, mobile-app, guardian-dashboard, rtc-services)
```json
{
  "recommendations": [
    "editorconfig.editorconfig",
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint"
  ]
}
```

### Python 저장소용 (ai-services)
```json
{
  "recommendations": [
    "editorconfig.editorconfig",
    "ms-python.python",
    "ms-python.black-formatter"
  ]
}
```

---

## 4️⃣ .vscode/settings.json

**VS Code 자동 포맷팅 설정**
```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "[python]": {
    "editor.defaultFormatter": "ms-python.black-formatter",
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
      "source.organizeImports": "explicit"
    }
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "files.eol": "\n"
}
```

### 주요 기능

✅ 저장 시 자동 포맷팅
✅ Prettier를 기본 포맷터로 사용
✅ ESLint 자동 수정
✅ 언어별 포맷터 지정

---

## 🚀 설치 방법

### 1단계: 저장소 클론
```bash
git clone <repo-url>
cd backend
```

### 2단계: 의존성 설치
```bash
npm install
```

### 3단계: VS Code 확장 프로그램 설치

VS Code를 열면 자동으로 권장 확장 프로그램 설치 팝업 표시됨

**수동 설치:**
1. `Ctrl+Shift+X` (확장 프로그램 탭)
2. 검색: "Prettier", "ESLint", "EditorConfig"
3. 설치 클릭

### 4단계: 완료! 🎉

파일 저장(`Ctrl+S`)하면 자동으로 포맷팅됩니다.

---

## 💻 사용 방법

### VS Code 사용자

**자동 포맷팅:**
```
코드 작성 → Ctrl+S (저장) → ✅ 자동 포맷팅
```

**수동 포맷팅:**
```
Shift+Alt+F
```

### 다른 에디터 사용자
```bash
npm run format
```

---

## 📝 네이밍 컨벤션

### PascalCase
**사용:** React 컴포넌트, 인터페이스, 클래스
```typescript
const VideoCallScreen = () => { ... }
interface UserData { ... }
class DatabaseConnection { ... }
```

### camelCase
**사용:** 변수, 함수, props
```typescript
const userName = '재완';
function getUserProfile() { ... }
<Button onClick={handleClick} />
```

### kebab-case
**사용:** 파일명, URL, CSS 클래스
```typescript
// 파일명
video-call-screen.tsx

// URL
/api/user-profile

// CSS
.video-call-container
```

### SCREAMING_SNAKE_CASE
**사용:** 상수
```typescript
const MAX_RETRY_COUNT = 3;
const API_BASE_URL = 'https://api.damso.com';
```

---

## 📊 저장소별 파일 체크리스트

### TypeScript 저장소 (backend, mobile-app, guardian-dashboard, rtc-services)

- [ ] `.editorconfig`
- [ ] `.prettierrc`
- [ ] `.vscode/extensions.json` (TypeScript용)
- [ ] `.vscode/settings.json`

### Python 저장소 (ai-services)

- [ ] `.editorconfig`
- [ ] `pyproject.toml` (Black 설정)
- [ ] `.vscode/extensions.json` (Python용)
- [ ] `.vscode/settings.json`

---

## ✨ 효과

✅ 팀원 간 일관된 코드 스타일
✅ Merge conflict 최소화
✅ 저장만 하면 자동 포맷팅
✅ 코드 리뷰 시 스타일 논쟁 제거
✅ 신규 팀원 온보딩 간소화

---

## 🔧 문제 해결

### Prettier가 작동하지 않을 때

1. 확장 프로그램 설치 확인 (`Ctrl+Shift+X`)
2. 기본 포맷터 확인 (파일 우클릭 → Format Document With...)
3. VS Code 재시작

### ESLint 에러가 계속 나올 때
```bash
rm -rf node_modules/.cache
npm install
```

---

## 👥 팀원 정보

| 이름 | 담당 | 저장소 |
| --- | --- | --- |
| 권동민 | Backend & DevOps | backend/ |
| 김상연 | AI/ML Services | ai-services/ |
| 문성수 | Frontend Mobile | mobile-app/ |
| 배재완 | Real-time Comm | rtc-services/ |
| 임익화 | Guardian Dashboard | guardian-dashboard/ |

---

**마지막 업데이트:** 2024-12-26