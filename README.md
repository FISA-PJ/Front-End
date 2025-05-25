### 🛠️ 트러블슈팅
#### 🔍 문제 상황
- 챗봇 버튼이 **화면 우측 하단이 아닌 왼쪽 하단**에 표시됨
- 사이드바 **접기/펼치기 버튼이 작동하지 않음**
- CSS 스타일도 적용되지 않아 전체 UI가 깨져 보임

---

#### ❗ 원인 분석
- CSS와 JS 파일을 `static/` 폴더 안으로 이동했지만,
- HTML 파일 내에서는 여전히 기존의 상대경로(`css/style.css`, `js/script.js`)를 사용하고 있었음
- 이로 인해:
  - CSS가 로딩되지 않아 `position: fixed` 스타일이 무시됨 → 챗봇 위치 오류 발생
  - JS가 로딩되지 않아 `toggleSidebar()` 함수가 정의되지 않음

---

#### ✅ 해결 방법
1. `css/`, `js/` 폴더를 `static/` 폴더 안으로 이동한 후
2. HTML 파일 내 경로를 다음과 같이 수정함:

```html
<!-- CSS 경로 수정 -->
<link rel="stylesheet" href="../static/css/style.css" />

<!-- JS 경로 수정 -->
<script src="../static/js/script.js"></script>
```
---
#### ✅ 결과
CSS와 JS가 정상 적용
➡️ 챗봇 버튼이 화면 우측 하단에 고정됨
➡️ 사이드바 접기/펼치기 버튼이 정상 작동

---
#### 💡 TIP
개발자 도구(F12) → Console / Network 탭에서 CSS/JS 파일이 404 오류인지 꼭 확인!
link나 script 태그에 잘못된 경로가 입력되면 로딩되지 않음
