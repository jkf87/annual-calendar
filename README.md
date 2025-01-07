# Annual Calendar (연간 달력)

한 페이지에 전체 연도가 표시되는 간단한 인쇄용 달력입니다.

🌐 **[웹에서 바로 사용하기](https://jkf87.github.io/annual-calendar/)**

## 특징
- 한 페이지에 1년 전체 달력 표시
- 모든 용지 크기에 자동 맞춤
- 주말 표시 (토요일: 회색 배경, 일요일: 빨간색)
- 인쇄 최적화
- 반응형 디자인
- 순수 HTML/CSS/JavaScript로 구현
- 일반 달력(1월-12월)과 학년도 달력(3월-다음해 2월) 지원

## 사용 방법
1. [웹 버전](https://jkf87.github.io/annual-calendar/)을 사용하거나 `index.html` 파일을 브라우저에서 엽니다.
2. 기본적으로 현재 연도의 달력이 표시됩니다.
3. 다른 연도를 보려면 URL에 `?year=연도` 를 추가하세요. (예: `index.html?year=2025`)
4. 학년도 달력을 보려면 URL에 `teacher=true` 를 추가하세요. (예: `index.html?year=2024&teacher=true`)
5. 인쇄하려면:
   - 브라우저의 인쇄 기능을 사용 (Ctrl+P 또는 Cmd+P)
   - 가로 방향 선택
   - 머리글/바닥글 비활성화 권장

## 최근 업데이트
- 학년도 달력 기능 추가 (3월 시작, 다음해 2월 종료)
- 달력 모드 전환 기능 추가 (일반 ↔ 학년도)
- 2월 날짜 계산 버그 수정 (윤년 처리 포함)
- 학년도 표시 개선 (예: 2024학년도 (2024.3 - 2025.2))

## 라이선스
MIT License

## 크레딧
- 원본 제작: [Neatnik](https://neatnik.net/)
- 한글화 및 수정: [코난쌤](https://www.youtube.com/@conanssam)

## 기술 설명

### 달력 생성 알고리즘
달력은 순수 JavaScript를 사용하여 동적으로 생성됩니다. 주요 동작 방식은 다음과 같습니다:

1. **달력 모드**
   - 일반 달력 (1월-12월)
   - 학년도 달력 (3월-다음해 2월)

2. **URL 파라미터**
   - `year`: 표시할 연도 (예: `?year=2024`)
   - `teacher`: 학년도 달력 모드 (`?teacher=true`)
   - `layout`: 레이아웃 타입

3. **날짜 계산**
   ```javascript
   // 월의 총 일수 계산
   new Date(year, month, 0).getDate()
   
   // 월의 첫 날 요일 계산 (0: 일요일, 6: 토요일)
   new Date(year, month - 1, 1).getDay()
   ```

4. **특별 표시**
   - 주말: 토요일(회색 배경), 일요일(빨간색)
   - 공휴일: 외부 API에서 정보를 가져와 표시
   - 날짜와 요일 동시 표시

5. **반응형 디자인**
   - vmin 단위를 사용하여 모든 화면 크기에 자동 조정
   - 인쇄 시 최적화된 스타일 적용

---

A simple printable calendar that displays the entire year on a single page.

🌐 **[Use Online](https://jkf87.github.io/annual-calendar/)**

## Features
- Full year calendar on a single page
- Auto-fits to any paper size
- Weekend highlighting (Saturday: gray background, Sunday: red)
- Print optimized
- Responsive design
- Pure HTML/CSS/JavaScript implementation

## How to Use
1. Use the [online version](https://jkf87.github.io/annual-calendar/) or open `index.html` in a browser
2. Calendar shows current year by default
3. For different years, add `?year=YYYY` to URL (e.g., `index.html?year=2025`)
4. To print:
   - Use browser's print function (Ctrl+P or Cmd+P)
   - Select landscape orientation
   - Recommended to disable headers/footers

## License
MIT License

## Credits
- Original by [Neatnik](https://neatnik.net/)
- Korean version & modifications by [코난쌤](https://www.youtube.com/@conanssam)
