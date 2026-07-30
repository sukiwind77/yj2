# 미니게임 연동 데모 (App-to-App Protocol Simulator)

메인 앱과 미니게임 간 URL Query Parameter를 사용한 상태 전달 및 `localStorage` 스탬프 수집 연동 원리를 실습하는 웹 애플리케이션입니다.

---

## 🚀 주요 기능 & 연동 원리

1. **나의 URL 생성 (Main App URL)**
   - 미니게임 이동 시 메인 앱 복귀 주소(`mainUrl`)를 함께 전달합니다.

2. **미니게임 성공 처리 & 복귀**
   - 미니게임 성공 시 `?game=practice-game&result=success` 파라미터를 부착하여 메인 앱으로 리다이렉트합니다.

3. **스탬프 저장 & URL 정화 ( 새로고침 중복 방지 )**
   - 성공 파라미터를 수신하면 `localStorage.stamps`에 미니게임 획득 상태를 저장합니다.
   - 저장 후 `window.history.replaceState`를 사용해 URL의 query parameter를 자동으로 제거하여 새로고침 시 중복 저장을 방지합니다.

---

## 🌐 GitHub Pages 배포 안내

이 프로젝트는 Vite 상대 경로(`base: './'`) 설정이 완료되어 있어, GitHub Pages에 쉽게 배포할 수 있습니다.

### 배포 순서
1. AI Studio 우측 상단 **GitHub Sync**로 코드 푸시
2. GitHub 레포지터리의 **Settings** -> **Pages** 탭 이동
3. **Build and deployment** -> **Source** 항목에서 **Deploy from a branch** 선택
4. (선택사항) GitHub Actions로 자동 배포를 원하시는 경우, GitHub 웹 인터페이스 상에서 **Actions** 탭 -> **New workflow** -> **Vite** 또는 **Static HTML / Node** Template을 직접 추가하실 수 있습니다.

---

## 🛠️ 개발 및 빌드 명령어

```bash
# 패키지 설치
npm install

# 개발 서버 실행 (localhost:3000)
npm run dev

# 빌드 검증 (TypeScript 검사)
npm run lint

# GitHub Pages용 정적 파일 빌드 (dist/ 생성)
npm run build
```

---

## 📁 프로젝트 구조

```
├── index.html                    # 메인 HTML 템플릿
├── vite.config.ts                # Vite 설정 (base: './' 상대 경로 설정)
├── src/
│   ├── main.tsx                  # React 엔트리 포인트
│   ├── App.tsx                   # 메인 라우터 및 상태 관리
│   ├── types.ts                  # 타입 정의
│   ├── utils/
│   │   └── storage.ts            # localStorage 수집 처리 유틸리티
│   └── components/
│       ├── MainApp.tsx           # 메인 앱 화면
│       ├── MiniGameApp.tsx       # 미니게임 화면
│       └── UrlFlowDiagram.tsx    # 연동 원리 흐름도 컴포넌트
└── package.json
```
