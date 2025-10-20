# My CSS Library

CSS 스타일과 레이아웃을 학습하고 정리하는 개인 라이브러리입니다.

## 프로젝트 목적

다양한 CSS 기법과 스타일을 실험하고, 재사용 가능한 형태로 정리하여 필요할 때 참고할 수 있는 라이브러리를 구축합니다.

## 폴더 구조

```
My_CSS/
├── README.md              # 프로젝트 문서
├── layouts/               # 레이아웃 예제
│   └── grid-responsive.html
├── components/            # UI 컴포넌트 (버튼, 카드, 폼 등)
├── animations/            # 애니메이션 효과
├── effects/               # 인터랙티브 효과 (호버, 트랜지션 등)
├── utilities/             # 유틸리티 클래스
└── assets/                # 공통 리소스
    ├── css/               # 공통 CSS 파일
    └── images/            # 이미지 리소스
```

## 카테고리별 설명

### layouts/
페이지 레이아웃과 관련된 CSS 기법을 정리합니다.
- Grid Layout
- Flexbox Layout
- 반응형 레이아웃
- Multi-column Layout

### components/
재사용 가능한 UI 컴포넌트를 정리합니다.
- 버튼 스타일
- 카드 컴포넌트
- 네비게이션 메뉴
- 폼 요소
- 모달/대화상자

### animations/
CSS 애니메이션과 키프레임을 정리합니다.
- Fade 애니메이션
- Slide 애니메이션
- Bounce 효과
- Loading 스피너

### effects/
인터랙티브한 시각 효과를 정리합니다.
- Hover 효과
- Transition 효과
- Transform 효과
- 그림자 효과

### utilities/
자주 사용하는 유틸리티 클래스를 정리합니다.
- Spacing (margin, padding)
- Typography
- Colors
- Display/Visibility

### assets/
프로젝트 전반에서 사용하는 공통 리소스를 저장합니다.
- 공통 CSS 변수
- 테마 파일
- 이미지 및 아이콘

## 파일 명명 규칙

각 HTML 파일은 다음과 같은 규칙으로 명명합니다:
- **설명적인 이름 사용**: 파일명만 봐도 내용을 알 수 있게
- **케밥 케이스 사용**: `grid-responsive.html`, `button-styles.html`
- **카테고리별 구분**: 각 폴더에 적절한 카테고리로 분류

## 파일 관리 방법

1. **새로운 스타일 추가 시**
   - 적절한 카테고리 폴더에 HTML 파일 생성
   - 파일 내부에 `<style>` 태그로 CSS 작성
   - 실제 동작을 확인할 수 있도록 HTML 마크업 포함

2. **공통 스타일**
   - 여러 파일에서 재사용되는 스타일은 `assets/css/`에 별도 파일로 분리
   - 각 HTML 파일에서 링크로 참조

3. **문서화**
   - 각 파일에 주석으로 스타일 설명 추가
   - 복잡한 기법은 사용법과 주의사항 명시

## 현재 포함된 예제

### layouts/grid-responsive.html
CSS Grid를 활용한 반응형 레이아웃 예제
- 데스크탑: 3열 그리드 레이아웃 (Header, Sidebar, Main, Section, Content, Footer)
- 모바일 (760px 이하): 1열 세로 스택 레이아웃
- `grid-template-areas`를 사용한 직관적인 레이아웃 정의

## 향후 계획

- [ ] Flexbox 레이아웃 예제 추가
- [ ] 다양한 버튼 스타일 컴포넌트 추가
- [ ] 애니메이션 효과 라이브러리 구축
- [ ] 공통 CSS 변수 파일 생성
- [ ] 각 카테고리별 인덱스 페이지 생성

## 사용 방법

각 HTML 파일을 브라우저에서 직접 열어 스타일과 동작을 확인할 수 있습니다.

```bash
# 예시: layouts/grid-responsive.html 열기
start layouts/grid-responsive.html
```

---

**Last Updated**: 2025-10-20
