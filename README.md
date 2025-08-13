# 프로젝트 자동 설정 도구

이 저장소는 Claude Code를 사용한 풀스택 웹 애플리케이션 개발을 위한 자동화된 프로젝트 설정 도구입니다.

## 🚀 빠른 시작

### 새 프로젝트 생성
```bash
# 이 저장소를 원하는 프로젝트 이름으로 복사
cp -r /path/to/setup /path/to/your-new-project
cd /path/to/your-new-project

# setup.md를 기반으로 프로젝트 초기화
# Claude Code에서 다음 명령어 실행:
# "setup.md를 토대로, [앱 설명] 하는 앱을 만들려고 한다. 해당 내용을 실행"
```

## 📁 프로젝트 구조

```
setup/
├── .claude/                 # Claude Code 설정
│   └── commands/
├── CLAUDE.md               # 개발 가이드 및 규칙
├── setup.md                # 프로젝트 자동화 설정 가이드
└── README.md               # 이 파일
```

## 📋 포함된 기능

### 개발 프레임워크
- **Clean Architecture** 기반 설계
- **TDD (Test-Driven Development)** 필수 프로세스
- **SOLID 원칙** 엄격 적용
- **MVVM 패턴** (프론트엔드)

### 기술 스택
- **Frontend**: Next.js 14+ (App Router), TypeScript, Tailwind CSS
- **Backend**: NestJS, TypeScript, Raw SQL
- **Database**: PostgreSQL/Supabase
- **Testing**: Jest, Testing Library, Playwright
- **Deployment**: Vercel/Netlify (Frontend), Railway/Render (Backend)

### 자동화 기능
- 프로젝트 구조 생성
- 기술 스택 초기화
- 환경 설정 파일 생성
- Docker 설정
- Git 초기화 및 커밋 전략
- 문서 템플릿 생성 (PRD, 설계, 작업 계획)

## 🛠️ 사용 방법

### 1. 기본 설정
```bash
# Claude Code에서 실행
setup.md를 토대로, [당신의 앱 설명] 하는 앱을 만들려고 한다. 해당 내용을 실행
```

### 2. 생성되는 문서들
- **docs/prd.md**: 제품 요구사항 명세서 (기획)
- **docs/design.md**: 아키텍처 및 시스템 설계
- **docs/tasks.md**: 개발 작업 분할 및 우선순위

### 3. 개발 프로세스
1. **문서 기반 개발**: prd.md → design.md → tasks.md 순서로 진행
2. **TDD 사이클**: Red → Green → Refactor
3. **품질 보증**: 테스트 커버리지 95% 이상 유지
4. **지속적 통합**: Git 커밋 후 tasks.md 업데이트 필수

## 📖 주요 문서

### CLAUDE.md
전체 개발 가이드라인과 규칙이 포함된 핵심 문서:
- 개발 원칙 및 아키텍처 패턴
- 코딩 컨벤션 및 네이밍 규칙
- TDD 프로세스 및 테스트 전략
- 프로젝트 구조 및 워크플로우
- 환경 설정 및 배포 가이드

### setup.md
프로젝트 자동화를 위한 상세 가이드:
- 단계별 설정 스크립트
- 기술 스택별 초기화 방법
- 환경 변수 및 설정 파일 템플릿
- Docker 및 배포 설정

## 🎯 개발 원칙

### 필수 규칙
- **TDD 필수**: 테스트 코드 우선 작성
- **문서 우선**: prd.md → design.md → tasks.md 순서 준수
- **SOLID 원칙**: 모든 클래스와 인터페이스에서 엄격 적용
- **Clean Architecture**: 계층별 의존성 방향 준수
- **품질 보증**: 테스트 커버리지 95% 이상

### 워크플로우
1. tasks.md에서 우선순위 확인
2. 테스트 케이스 작성 (Red)
3. 최소 구현 (Green)
4. 리팩토링 (Refactor)
5. Git 커밋
6. tasks.md 업데이트

## 🤖 Claude Code 통합

이 프로젝트는 Claude Code의 고급 기능들을 활용합니다:

### SuperClaude 프레임워크
- **MCP 서버 통합**: Context7, Sequential, Magic, Playwright
- **페르소나 시스템**: 11개 전문 도메인 페르소나
- **인텔리전트 라우팅**: 자동 도구 선택 및 최적화
- **웨이브 오케스트레이션**: 복잡한 다단계 작업 관리

### 자동화된 명령어
- `/build`: 프로젝트 빌더
- `/implement`: 기능 구현
- `/analyze`: 시스템 분석
- `/improve`: 코드 개선
- `/test`: 테스트 실행

## 📝 라이선스

이 프로젝트는 MIT 라이선스 하에 있습니다.

## 🤝 기여하기

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

**참고**: 이 도구는 Claude Code와 함께 사용할 때 최적의 성능을 발휘합니다. 모든 개발 과정에서 TDD와 Clean Architecture 원칙을 준수해주세요.