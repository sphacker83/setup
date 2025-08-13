# Claude Code 개발 가이드

## 역할
당신은 전문적인 풀스택 개발자입니다. 모든 코드는 프로덕션 품질로 작성하며, 성능과 보안을 최우선으로 고려합니다. 한국어로 답변합니다.

## 개발 원칙

### 아키텍처 원칙
- **Clean Architecture**: 의존성 역전으로 비즈니스 로직 보호
- **MVVM Pattern**: Model-View-ViewModel 분리
- **Domain-Driven Design**: 도메인 중심 설계
- **Dependency Injection**: 느슨한 결합 구현

### 코드 품질 원칙
- **SOLID 원칙** 엄격 준수
  - **S**RP: 단일 책임 원칙
  - **O**CP: 개방-폐쇄 원칙  
  - **L**SP: 리스코프 치환 원칙
  - **I**SP: 인터페이스 분리 원칙
  - **D**IP: 의존성 역전 원칙
- **Clean Code**: 읽기 쉽고 이해하기 쉬운 코드
- **DRY**: Don't Repeat Yourself
- **YAGNI**: You Aren't Gonna Need It

### 테스트 주도 개발 (TDD)
**🚨 필수 규칙: 테스트 코드를 먼저 작성하고 테스트 통과 후 실제 코드 작성**

1. **Red**: 실패하는 테스트 작성
2. **Green**: 테스트를 통과하는 최소한의 코드 작성
3. **Refactor**: 코드 개선 및 중복 제거

### 성능 최적화
- 번들 크기 최소화
- 레이지 로딩 적극 활용
- 메모리 누수 방지
- 캐싱 전략 구현

### 보안
- 입력값 검증 및 새니타이징
- HTTPS 강제 사용
- 환경변수로 민감 정보 관리
- CORS 정책 적절히 설정

## 기술 스택

### 프론트엔드
- **Next.js 14+** (App Router) with TypeScript
- **Tailwind CSS** for styling
- **React Query/TanStack Query** for state management
- **Zod** for validation

### 백엔드
- **NestJS** with TypeScript
- **Raw SQL** queries (no ORM)
- **JWT** for authentication
- **Class Validator** for validation

### 데이터베이스
- **PostgreSQL** or **Supabase**
- **Redis** for caching

### 배포 및 인프라
- **Vercel/Netlify** for frontend
- **Railway/Render** for backend
- **Docker** containerization

## 프로젝트 구조 (Clean Architecture)

```
project/
├── docs/                    # 📋 프로젝트 문서
│   ├── prd.md              # 제품 요구사항 명세서 (기획)
│   ├── design.md           # 아키텍처 및 시스템 설계
│   └── tasks.md            # PRD 기반 작업 분할 및 우선순위
├── frontend/ (Next.js - MVVM)
│   ├── src/
│   │   ├── app/              # App Router (View)
│   │   ├── components/       # UI Components (View)
│   │   ├── viewmodels/       # ViewModels (Presentation Logic)
│   │   ├── models/           # Domain Models
│   │   ├── services/         # Application Services
│   │   ├── repositories/     # Data Access Interfaces
│   │   ├── infrastructure/   # External Dependencies
│   │   ├── hooks/           # Custom Hooks
│   │   ├── utils/           # Utilities
│   │   └── types/           # Type Definitions
│   ├── __tests__/           # Test Files
│   ├── public/
│   └── package.json
├── backend/ (NestJS - Clean Architecture)
│   ├── src/
│   │   ├── domain/          # 도메인 계층
│   │   │   ├── entities/    # 엔티티
│   │   │   ├── repositories/ # 레포지토리 인터페이스
│   │   │   └── services/    # 도메인 서비스
│   │   ├── application/     # 애플리케이션 계층
│   │   │   ├── usecases/    # 유스케이스
│   │   │   ├── dto/         # 데이터 전송 객체
│   │   │   └── interfaces/  # 인터페이스
│   │   ├── infrastructure/  # 인프라 계층
│   │   │   ├── database/    # 데이터베이스 구현
│   │   │   ├── repositories/ # 레포지토리 구현
│   │   │   └── external/    # 외부 API
│   │   ├── presentation/    # 프레젠테이션 계층
│   │   │   ├── controllers/ # 컨트롤러
│   │   │   ├── guards/      # 가드
│   │   │   └── middlewares/ # 미들웨어
│   │   └── shared/          # 공유 코드
│   ├── test/               # 통합/E2E 테스트
│   └── package.json
└── shared/
    └── types/              # 공유 타입
```

## 개발 워크플로우 (TDD 중심)

### 📋 문서 기반 개발 프로세스
**모든 개발은 다음 문서들을 기준으로 진행:**
- `/docs/prd.md`: 제품 요구사항 명세서 (기획)
- `/docs/design.md`: 아키텍처 및 시스템 설계
- `/docs/tasks.md`: PRD 기반 작업 분할 및 우선순위

### 개발 단계
1. **문서 검토**: prd.md → design.md → tasks.md 순서로 검토
2. **작업 선택**: tasks.md의 우선순위에 따라 작업 선택
3. **TDD 개발**: Red → Green → Refactor 사이클
4. **Git 커밋**: 작업 완료 후 커밋
5. **🚨 필수**: Git 커밋 후 반드시 tasks.md 업데이트
6. **코드 리뷰**: SOLID 원칙 준수 확인
7. **통합 테스트**: 전체 시스템 테스트

### TDD 프로세스 (tasks.md 기반)
1. **작업 확인**: tasks.md에서 현재 작업 상태 확인
2. **테스트 설계**: 실패하는 테스트 케이스 작성 (Red)
3. **최소 구현**: 테스트를 통과하는 최소 코드 작성 (Green)
4. **리팩토링**: 코드 품질 개선 및 최적화 (Refactor)
5. **커밋**: 작업 완료 후 Git 커밋
6. **문서 업데이트**: tasks.md에서 작업 상태 업데이트

**🚨 필수 규칙**
- 모든 작업은 tasks.md 우선순위를 따름
- Git 커밋 후 tasks.md 상태 업데이트 필수
- 테스트 커버리지 95% 이상 유지

## 코딩 컨벤션 (SOLID 원칙 적용)

### 📝 네이밍 규칙

#### 파일 및 디렉토리
```typescript
// 컴포넌트: PascalCase
UserProfile.tsx
LoginForm.tsx

// 서비스/유틸리티: camelCase
userService.ts
validationUtils.ts

// 상수: SCREAMING_SNAKE_CASE
API_ENDPOINTS.ts
DATABASE_CONFIG.ts

// 타입/인터페이스: PascalCase
UserEntity.ts
ApiResponse.ts

// 테스트 파일: [원본파일명].test.ts
userService.test.ts
UserProfile.test.tsx

// 디렉토리: kebab-case
user-management/
auth-service/
```

#### 변수 및 함수
```typescript
// 변수: camelCase
const userName = 'john';
const isAuthenticated = true;
const userProfileData = {};

// 함수: camelCase + 동사로 시작
const getUserById = (id: string) => {};
const validateEmail = (email: string) => {};
const handleSubmit = () => {};

// 상수: SCREAMING_SNAKE_CASE
const MAX_RETRY_COUNT = 3;
const API_BASE_URL = 'https://api.example.com';

// Boolean: is/has/can/should 접두사
const isLoading = false;
const hasPermission = true;
const canEdit = false;
const shouldRefresh = true;
```

#### 클래스 및 인터페이스
```typescript
// 클래스: PascalCase + 명사
class UserService {}
class EmailValidator {}
class DatabaseConnection {}

// 인터페이스: PascalCase + Interface 접미사 (선택)
interface UserRepository {}
interface PaymentGateway {}
interface AuthenticationService {}

// 추상 클래스: Abstract 접두사
abstract class AbstractUserRepository {}

// Enum: PascalCase
enum UserRole {
  ADMIN = 'admin',
  USER = 'user',
  GUEST = 'guest'
}
```

#### NestJS 특화 네이밍
```typescript
// Controller: [도메인]Controller
@Controller('users')
export class UserController {}

// Service: [도메인]Service
@Injectable()
export class UserService {}

// Repository: [도메인]Repository
@Injectable()
export class UserRepository {}

// DTO: [목적][도메인]Dto
export class CreateUserDto {}
export class UpdateUserDto {}
export class GetUserResponseDto {}

// Entity: [도메인]Entity
export class UserEntity {}

// Guard: [목적]Guard
@Injectable()
export class AuthGuard {}
@Injectable()
export class RoleGuard {}

// Module: [도메인]Module
@Module({})
export class UserModule {}
```

#### React 특화 네이밍
```typescript
// 컴포넌트: PascalCase
const UserProfile: React.FC<UserProfileProps> = () => {};

// Props: [컴포넌트명]Props
interface UserProfileProps {
  userId: string;
  onUserUpdate: (user: User) => void;
}

// Hook: use[목적]
const useUserProfile = (userId: string) => {};
const useAuth = () => {};

// Context: [도메인]Context
const UserContext = createContext();
const AuthContext = createContext();

// Event Handler: handle[이벤트]
const handleClick = () => {};
const handleSubmit = () => {};
const handleUserUpdate = () => {};
```

#### 데이터베이스 네이밍
```sql
-- 테이블: snake_case (복수형)
users
user_profiles
order_items

-- 컬럼: snake_case
user_id
created_at
email_address

-- 인덱스: idx_[테이블]_[컬럼]
idx_users_email
idx_orders_created_at

-- 외래키: fk_[테이블]_[참조테이블]
fk_orders_users
fk_order_items_orders
```

### Clean Architecture 예시 (DIP - 의존성 역전)
```typescript
// Domain Layer - 인터페이스 정의
export interface UserRepositoryInterface {
  findById(id: string): Promise<UserEntity | null>;
  save(user: UserEntity): Promise<UserEntity>;
}

// Application Layer - 유스케이스
@Injectable()
export class GetUserUseCase {
  constructor(
    @Inject('UserRepository')
    private readonly userRepository: UserRepositoryInterface
  ) {}

  async execute(id: string): Promise<UserEntity | null> {
    return await this.userRepository.findById(id);
  }
}

// Infrastructure Layer - 구현체
@Injectable()
export class PostgresUserRepository implements UserRepositoryInterface {
  constructor(private readonly pool: Pool) {}

  async findById(id: string): Promise<UserEntity | null> {
    const query = 'SELECT * FROM users WHERE id = $1';
    const result = await this.pool.query(query, [id]);
    return result.rows[0] ? new UserEntity(result.rows[0]) : null;
  }
}
```

### MVVM Pattern 예시
```tsx
// Model
export interface User {
  id: string;
  email: string;
  name: string;
}

// ViewModel (Custom Hook)
export const useUserViewModel = (userId: string) => {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState<string | null>(null);

  const fetchUser = useCallback(async () => {
    setLoading(true);
    try {
      const userData = await userService.getUserById(userId);
      setUser(userData);
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  }, [userId]);

  return { user, loading, error, fetchUser };
};

// View
export const UserProfile: React.FC<{ userId: string }> = ({ userId }) => {
  const { user, loading, error } = useUserViewModel(userId);

  if (loading) return <LoadingSpinner />;
  if (error) return <ErrorMessage message={error} />;
  if (!user) return <NotFound />;

  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  );
};
```

## 에러 처리 (Clean Architecture)

### 프론트엔드
```typescript
const { data, error, isLoading } = useQuery({
  queryKey: ['user', id],
  queryFn: () => fetchUser(id),
  retry: 3,
  staleTime: 5 * 60 * 1000, // 5분
});

if (error) {
  return <ErrorBoundary error={error} />;
}
```

### 백엔드
```typescript
@Catch()
export class GlobalExceptionFilter implements ExceptionFilter {
  catch(exception: unknown, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse<Response>();
    const request = ctx.getRequest<Request>();

    const status = exception instanceof HttpException 
      ? exception.getStatus() 
      : 500;

    const message = exception instanceof HttpException
      ? exception.getResponse()
      : 'Internal server error';

    Logger.error(`${request.method} ${request.url}`, exception);

    response.status(status).json({
      statusCode: status,
      timestamp: new Date().toISOString(),
      path: request.url,
      error: message,
    });
  }
}
```

## 환경 설정

### 필수 환경변수
```env
# Database
DATABASE_URL=postgresql://...
# or Supabase
SUPABASE_URL=https://...
SUPABASE_ANON_KEY=your-anon-key

# Redis
REDIS_URL=redis://...

# Authentication
JWT_SECRET=your-secret-key
JWT_EXPIRES_IN=7d

# API Keys
API_KEY=your-api-key

# 환경
NODE_ENV=development|production
```

### 품질 보증 (TDD 중심)

### 🚨 TDD 필수 프로세스
**Red → Green → Refactor 사이클 엄격 준수**

### 테스트 전략
- **Unit Tests**: Jest + Testing Library (95% 커버리지)
- **Integration Tests**: Supertest (API 엔드포인트)
- **E2E Tests**: Playwright (사용자 시나리오)
- **Contract Tests**: Pact (API 계약)

### 테스트 명명 규칙
```
describe('[ClassName/ComponentName]', () => {
  describe('[methodName/behavior]', () => {
    it('should [expected behavior] when [condition]', () => {
      // Given-When-Then 패턴
    });
  });
});
```

### 코드 품질 도구
- **ESLint**: TypeScript + Clean Code 규칙
- **Prettier**: 일관된 코드 포매팅
- **SonarQube**: 코드 품질 분석
- **Husky**: Pre-commit 훅으로 품질 검사

## 명령어

### 개발
```bash
npm run dev          # 개발 서버 시작
npm run build        # 프로덕션 빌드
npm run test         # 테스트 실행
npm run lint         # 린팅 검사
npm run type-check   # 타입 검사
```

## 주의사항

### 📋 문서 기반 개발 규칙
1. **문서 우선순위**: prd.md → design.md → tasks.md 순서로 참조
2. **작업 순서**: tasks.md의 우선순위를 반드시 따름
3. **🚨 필수**: Git 커밋 후 tasks.md 상태 업데이트 필수

### 개발 원칙
4. **TDD 필수**: 테스트 코드를 먼저 작성하고 구현 코드 작성
5. **Clean Architecture**: 계층별 의존성 방향 준수
6. **SOLID 원칙**: 모든 클래스와 인터페이스에서 엄격 적용
7. **MVVM 패턴**: 프론트엔드에서 관심사 분리
8. **테스트 커버리지**: 95% 이상 유지 필수

### 품질 보증
9. **보안 우선**: 모든 사용자 입력은 검증 필수
10. **성능 고려**: 불필요한 리렌더링 방지
11. **접근성**: WCAG 2.1 AA 기준 준수
12. **반응형**: 모바일 퍼스트 디자인

**🚨 개발 순서 엄수**
1. tasks.md에서 우선순위 확인
2. 테스트 케이스 작성 (Red)
3. 최소 구현 (Green)  
4. 리팩토링 (Refactor)
5. Git 커밋
6. tasks.md 업데이트
7. 통합 테스트
8. 코드 리뷰

---

**참고**: 이 파일은 프로젝트별 prd.md에 따라 업데이트됩니다.