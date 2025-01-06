# 연간 달력 개발 문서

## 1. 프로젝트 개요

이 프로젝트는 한 페이지에 1년 전체 달력을 표시하는 웹 애플리케이션입니다. PHP로 작성된 원본([Neatnik의 Calendar](https://neatnik.net/))을 순수 HTML/CSS/JavaScript로 변환하고, 한국어 지원과 공휴일 표시 기능을 추가했습니다.

### 주요 기능
- 1년 전체 달력을 한 페이지에 표시
- 자동 크기 조절 (반응형 디자인)
- 주말 강조 표시
- 공휴일 표시 및 툴팁
- 연도 변경 기능
- 인쇄 최적화

## 2. 기술 스택

- **Frontend**: HTML5, CSS3, JavaScript (Vanilla)
- **폰트**: 
  - Noto Sans KR (한글)
  - Inter, Oswald (영문)
- **공휴일 API**: holidays.hyunbin.page

## 3. 주요 구현 사항

### 3.1 반응형 디자인

CSS에서 `vmin` 단위를 사용하여 뷰포트 크기에 따라 자동으로 조절되도록 구현:

```css
td, th {
  padding: .3vmin .3vmin;
  font-size: .9vmin;
}
```

### 3.2 인쇄 최적화

인쇄 시 스타일 조정을 위한 미디어 쿼리 사용:

```css
@media print {
  @page {
    margin: 0;
    padding: 1em;
  }
  td {
    font-size: 8px !important;
  }
  .weekend {
    background: #d8d8d8 !important;
  }
}
```

### 3.3 공휴일 처리

공휴일 정보는 외부 API를 통해 가져옵니다:

```javascript
fetch('https://holidays.hyunbin.page/basic.json')
    .then(response => response.json())
    .then(holidaysData => {
        const holidays = holidaysData[year] || {};
        createCalendarWithHolidays(year, layout, holidays);
    });
```

공휴일 스타일링:
```css
.holiday {
  background: #ffcccc50;
  font-weight: bold;
}
```

### 3.4 날짜 계산

달력 생성에 필요한 핵심 함수들:

```javascript
function getDaysInMonth(year, month) {
    return new Date(year, month, 0).getDate();
}

function getFirstDayOfMonth(year, month) {
    return new Date(year, month - 1, 1).getDay();
}
```

## 4. URL 파라미터

달력은 다음 URL 파라미터를 지원합니다:

- `year`: 표시할 연도 (예: `?year=2025`)
- `layout`: 레이아웃 형식
  - `aligned-weekdays`: 요일 정렬 모드
  - 기본값: 일반 모드

## 5. 알려진 제한사항

1. 공휴일 API가 사용 불가능할 경우 공휴일 표시가 되지 않음
2. JavaScript가 비활성화된 환경에서는 작동하지 않음
3. 매우 작은 화면에서는 가독성이 떨어질 수 있음

## 6. 향후 개선 사항

1. 공휴일 데이터의 로컬 캐싱 구현
2. 오프라인 지원 (PWA)
3. 다크 모드 지원
4. 사용자 정의 일정 추가 기능

## 7. 개발자를 위한 팁

### 7.1 로컬 개발 환경 설정

1. 저장소 클론:
```bash
git clone https://github.com/jkf87/annual-calendar.git
cd annual-calendar
```

2. 로컬 서버 실행 (선택사항):
   - Python: `python -m http.server 8000`
   - Node.js: `npx serve`
   - PHP: `php -S localhost:8000`

### 7.2 코드 수정 시 주의사항

1. 날짜 계산 시 JavaScript의 Date 객체 특성 주의
   - 월은 0부터 시작 (0-11)
   - 요일도 0부터 시작 (0: 일요일)

2. 인쇄 스타일 테스트
   - 다양한 용지 크기로 테스트
   - 브라우저의 인쇄 미리보기 활용

3. 공휴일 API 사용 시
   - API 응답 형식: `{"YYYY-MM-DD": "공휴일명"}`
   - 오류 처리 필수
   - CORS 정책 확인

## 8. 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다. 자세한 내용은 LICENSE 파일을 참조하세요. 