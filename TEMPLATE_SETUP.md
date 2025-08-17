# React 프로젝트 템플릿 설정 가이드

## 📁 보관해야 할 템플릿 파일들

### 1. `.vscode/tasks.json`

VS Code 작업 자동화 설정 파일

### 2. `.env.windows`

Windows 환경 설정 파일

```env
# Windows 환경 설정
VITE_USE_POLLING=false
CHOKIDAR_USEPOLLING=false
```

### 3. `.env.wsl`

WSL 환경 설정 파일

```env
# WSL 환경 설정
VITE_USE_POLLING=true
CHOKIDAR_USEPOLLING=true
```

### 4. `package.json` 수정 내용

다음 스크립트를 기존 package.json에 추가:

```json
"scripts": {
  "dev": "vite",
  "dev:wsl": "cross-env VITE_USE_POLLING=true CHOKIDAR_USEPOLLING=true vite",
  "dev:windows": "cross-env VITE_USE_POLLING=false CHOKIDAR_USEPOLLING=false vite",
  // ... 기존 스크립트들
}
```

## 🚀 사용 방법

### 새 프로젝트에 적용하기

1. `npm create vite@latest`로 새 React 프로젝트 생성
2. 프로젝트 폴더로 이동
3. 위의 템플릿 파일들을 복사:
   - `.vscode` 폴더 생성 후 `tasks.json` 복사
   - `.env.windows`, `.env.wsl` 파일 복사
   - `package.json`의 scripts 부분 수정
4. VS Code에서 프로젝트 열기
5. `Ctrl + Shift + P` → `Tasks: Run Task` → `환경 자동 감지 개발 서버` 실행

### 자동 기능

- **자동 패키지 설치**: 폴더를 열면 자동으로 npm install 실행
- **cross-env 자동 설치**: 없으면 자동으로 설치

## 파일 구조

```
프로젝트/
├── .vscode/
│   └── tasks.json        # VS Code 작업 설정
├── .env.windows         # Windows 환경변수
├── .env.wsl            # WSL 환경변수
└── package.json        # 수정된 스크립트 포함
```

## 주요 기능

- **Windows**: 파일 변경 감지 polling 비활성화 (성능 최적화)
- **WSL**: 파일 변경 감지 polling 활성화 (파일 시스템 호환성)
- **자동 의존성 관리**: 필요한 패키지 자동 설치
