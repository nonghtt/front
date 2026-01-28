# 상담사 대시보드 컨셉 개발 워크플로우

## 프로젝트 개요

여러 대시보드 레이아웃 컨셉을 빠르게 개발하고 비교하기 위한 프로토타입 프로젝트입니다.
각 컨셉은 URL 경로를 통해 쉽게 전환할 수 있으며, 컨셉별로 독립적인 UI 구성을 가집니다.

## URL 라우팅 전략

### 기본 구조
```
/concept/1  → 컨셉 1 (기본 레이아웃)
/concept/2  → 컨셉 2 (대안 레이아웃 A)
/concept/3  → 컨셉 3 (대안 레이아웃 B)
...
```

### 라우팅 구현
- 다이나믹 라우트 파라미터 사용: `/concept/:id`
- 컨셉 ID에 따라 해당하는 컴포넌트 세트를 동적으로 로드
- 존재하지 않는 컨셉 ID 접근 시 404 또는 기본 컨셉으로 리다이렉트

## 컨셉별 컴포넌트 구조

각 컨셉은 독립적인 UI 구성 요소를 가집니다:

```
src/
├── pages/
│   └── ConceptPage.vue           # 컨셉 페이지 컨테이너 (다이나믹 라우트)
├── concepts/
│   ├── concept1/
│   │   ├── Header.vue            # 컨셉 1 전용 헤더
│   │   ├── QuickMenu.vue         # 컨셉 1 전용 퀵메뉴
│   │   ├── Sidebar.vue           # 컨셉 1 전용 사이드바
│   │   └── MainContent.vue       # 컨셉 1 메인 콘텐츠
│   ├── concept2/
│   │   ├── Header.vue
│   │   ├── QuickMenu.vue
│   │   ├── Sidebar.vue
│   │   └── MainContent.vue
│   └── concept3/
│       ├── Header.vue
│       ├── QuickMenu.vue
│       ├── Sidebar.vue
│       └── MainContent.vue
└── composables/
    └── useConceptLoader.js       # 컨셉 로더 유틸리티
```

## 컴포넌트 역할

### 1. Header (헤더)
- 로고, 소프트폰, 로그아웃 버튼 등 상단 바
- 컨셉별로 배치, 색상, 기능이 다를 수 있음
- 위치: 상단 고정

### 2. QuickMenu (왼쪽 퀵메뉴)
- 주요 기능 바로가기 아이콘 메뉴
- 왼쪽 가장자리 고정 (데스크톱 전용)
- 컨셉별로 메뉴 항목과 아이콘이 다를 수 있음

### 3. Sidebar (왼쪽 사이드바)
- 메인 네비게이션 메뉴
- 토글 가능 (접기/펼치기)
- 컨셉별로 메뉴 구조, 깊이, 스타일이 다를 수 있음

### 4. MainContent (메인 콘텐츠)
- 상담사 대시보드 핵심 영역
- 민원인 정보, 상담이력, 대시보드 위젯 포함
- 컨셉별로 레이아웃과 정보 계층이 다름

## 컨셉 로더 로직

### useConceptLoader.js 예시
```javascript
import { computed } from 'vue'
import { useRoute } from 'vue-router'

export function useConceptLoader() {
  const route = useRoute()
  const conceptId = computed(() => route.params.id || '1')

  const loadComponent = async (componentType) => {
    try {
      const component = await import(
        `@/concepts/concept${conceptId.value}/${componentType}.vue`
      )
      return component.default
    } catch (error) {
      console.warn(`Component not found: concept${conceptId.value}/${componentType}`)
      // 폴백: concept1 컴포넌트 로드
      const fallback = await import(`@/concepts/concept1/${componentType}.vue`)
      return fallback.default
    }
  }

  return {
    conceptId,
    loadComponent
  }
}
```

## 개발 워크플로우

### 새 컨셉 추가하기

1. **폴더 생성**
   ```bash
   mkdir -p src/concepts/concept{N}
   ```

2. **필수 컴포넌트 생성**
   - `Header.vue`
   - `QuickMenu.vue`
   - `Sidebar.vue`
   - `MainContent.vue`

3. **컴포넌트 구현**
   - 기존 컨셉을 템플릿으로 복사하거나
   - 완전히 새로운 디자인으로 작성

4. **테스트**
   ```
   브라우저에서 /concept/{N} 접속하여 확인
   ```

### 컨셉 개발 시 주의사항

#### 일관성 유지
- 디자인 토큰(`app.scss`) 활용
- Quasar 컴포넌트 우선 사용
- 반응형 디자인 고려

#### 필수 기능 포함
- **민원인 정보 섹션**: 고객 프로필, 기본정보, 기업별 특화 정보
- **상담이력 섹션**: 통화 기록, 상담 내용 관리
- **대시보드 위젯**: 업무 관련 통계 및 상태

#### 평가 기준
- 정보 접근성: 주요 정보를 빠르게 찾을 수 있는가?
- 시각적 계층: 중요도에 따라 요소가 시각적으로 구분되는가?
- 업무 효율성: 상담사의 주요 업무 흐름이 자연스러운가?
- 확장성: 향후 새로운 정보 추가 시 대응 가능한가?

## 라우터 설정 예시

```javascript
// router/routes.js
const routes = [
  {
    path: '/',
    redirect: '/concept/1'  // 기본 컨셉으로 리다이렉트
  },
  {
    path: '/concept/:id',
    component: () => import('pages/ConceptPage.vue'),
    props: true
  },
  // ... 기타 라우트
]
```

## 컨셉 비교 방법

### 1. 사이드바이사이드 비교
- 브라우저 창을 여러 개 열어 `/concept/1`, `/concept/2` 동시 확인

### 2. 빠른 전환
- URL 수정으로 빠르게 전환하며 비교

### 3. 스크린샷 캡처
- 각 컨셉별 주요 화면 캡처하여 문서화

## 베스트 프랙티스

### 1. 컴포넌트 독립성
- 각 컨셉의 컴포넌트는 독립적으로 동작
- 컨셉 간 의존성 최소화
- 공통 로직은 composables나 utils로 분리

### 2. 재사용 가능한 위젯
- 공통 위젯은 `src/components/widgets/`에 배치
- 컨셉별로 다른 조합으로 사용

### 3. 스타일 관리
- 컨셉별 SCSS 파일 분리 가능
- 디자인 토큰 우선 활용
- 컨셉별 CSS 변수 오버라이드

### 4. 데이터 모킹
- 각 컨셉에서 동일한 목 데이터 사용
- `src/mock/` 폴더에 공통 데이터 관리

## 다음 단계

1. **초기 컨셉 3개 개발**
   - Concept 1: 전통적인 대시보드 레이아웃
   - Concept 2: 카드 기반 레이아웃
   - Concept 3: 패널 분할 레이아웃

2. **내부 리뷰**
   - 각 컨셉의 장단점 문서화
   - 팀 피드백 수집

3. **최종 컨셉 선정**
   - 평가 기준에 따라 점수화
   - 하이브리드 접근 고려

4. **프로덕션 개발**
   - 선정된 컨셉을 기반으로 실제 개발 진행
