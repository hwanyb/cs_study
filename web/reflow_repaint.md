# 📌 Reflow & Repaint
![이미지](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9960C33359A5059D09)
![이미지](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9988D33359A5059D1B)
## ✅ Reflow 란 무엇인가요?
렌더링 엔진에서 요소를 배치하는 과정을 의미합니다. `렌더 트리 구축`단계에서 DOM트리와 CSSOM 트리를 합쳐 렌더 트리를 만들고 여기에서 reflow를 통해 각각의 요소들의 레이아웃을 위치시킵니다.<br />
여기서 렌더 트리는 DOM요소 기반으로 만들어 지지만, 완전히 대응되지는 않습니다. DOM트리가 문서의 구조를 나타낸다면 렌더 트리는 문서의 시각적 구조를 나타냅니다. 예를들어 스타일에 `display: none` 속성이 있다면 DOM에서는 존재하지만 시각적으로는 없기에 트리에는 할당되지 않습니다.
### ✔ reflow가 발생하는 경우
- DOM 노드의 추가, 제거
- DOM 노드의 위치변경
- DOM 노드의 크기변경 (`margin`, `padding`, `border`, `width`, `height` 등)
- CSS3 애니메이션과 트랜지션
- 폰트 변경, 텍스트 내용 변경
- 이미지 크기 변경
- `offset`, `srollTop`, `scrollLeft와` 같은 계산된 스타일 정보 요청
- 페이지 초기 렌더링
- 윈도우 리사이징

## ✅ Repaint 란 무엇인가요?
**렌더 트리가 탐색되고 paint 메서드가 호출되어 UI기반의 구성요소를 사용해서 그리는 과정입니다.**

repaint가 이루어지기 위해서는 reflow 작업으로 만들어진 렌더트리가 있어야 합니다.

화면의 구조가 변경될 때는 reflow와 repaint가 모두 발생합니다.

repaint가 발생할 때에 항상 reflow가 발생하는 것은 아닙니다. repaint만 발생하는 경우는 레이아웃에 영향을 주지 않는 엘리먼트 개별이 변경되었을 때 입니다.
예를들어 `color`, `background-color`, `visibility` 같은 속성이 있습니다.