# Reflow 최적화
[Reflow](reflow_repaint.md)는 비용을 발생시키는 절차이므로 가능한 발생하지 않는 것이 성능 측면에서 유리합니다.
## Reflow 최적화 방법
1. **스타일을 변경할 경우 가장 하위노드의 스타일을 변경합니다.**<br />
DOM 노드의 크기 또는 위치가 변경되면 하위 노드와 상위 노드에도 영향을 미칠 수 있습니다. 이 때 가장 하위 노드의 스타일을 변경할 경우, 전체 노드가 아닌 일부 노드로 reflow 영향을 최소화할 수 있습니다.
2. **인라인 스타일을 사용하지 않습니다.**<br />
인라인 스타일은 HTML이 파싱될 때, 레이아웃에 영향을 미쳐 reflow를 발생시킵니다.
3. **애니메이션이 있는 노드는 position을 fixed 또는 absolute로 지정합니다.**<br />
애니메이션 효과는 많은 `reflow` 비용을 발생시킵니다. `position` 속성을 `fixed` 나 `absolute의` 값으로 지정하여 지정된 노드를 전체 노드에서 분리시켜 해당 노드에서만 reflow가 발생하도록 제한 시킬 수 있습니다.<br />
애니메이션 효과를 줘야 하는 노드에 `position` 속성이 적용이 되지 않았다면 애니메이션 시작 시 `position` 속성 값을 `fixed` 또는 `absolute로` 변경하였다가 애니메이션 종료 후 다시 원복시켜서 렌더링을 최적화 할 수 있다.
4. **table 레이아웃을 지양합니다.**<br />
`<table>` 태그는 점진적으로 렌더링되지 않고 모두 로드되고 테이블 너비가 계산된 후에 화면에 그려집니다. 테이블 안의 컨텐츠의 값에 따라 테이블 너비가 계산되므로 테이블 컨텐츠가 조금이라도 변경되면 테이블 너비가 다시 계산되고 테이블의 모든 노드들이 reflow됩니다. 이러한 이유로 `<table>`을 레이아웃 용도로 사용하는 일은 피해야 합니다.
5. **CSS 하위 선택자 사용을 최소화한다.**<br />
CSS 하위 선택자를 최소화하는 것은 reflow를 줄이는 방법이 아닌 렌더트리 계산을 최소화하는 방법입니다.<br />
    ```html
    <div class="reflow_box">
    <ul class="reflow_list">
        <li>
        <button type="button" class="btn">버튼</button>
        <li>
        <li>
        <button type="button" class="btn">버튼</button>
        <li>
    </ul>
    </div>
    ```
    ```css
    /* 잘못된 예 */
    .reflow_box .reflow_list li .btn{
    display:block;
    }
    /* 올바른 예 */
    .reflow_list .btn {
    display:block;
    }
    ```
    위의 코드와 같이 CSS 하위 선택자를 최소화 하는 것이 렌더링 성능에 더 좋다고 할 수있습니다.<br />
    렌더트리는 DOM 트리과 CSSOM트리가 합쳐져 만들어진 것인데, CSS하위 선택자가 많아지면 CSSOM 트리의 깊이(depth)가 깊어지게 되면서 렌더트리를 만드는 시간이 더 오래 걸리게 됩니다.
6. **숨겨진 노드의 스타일을 변경합니다.**<br />
`display: none` 으로 숨겨진 노드를 변경할 때는 reflow가 발생하지 않습니다. 숨겨진 노드를 표시하기 전에 노드의 컨텐츠를 먼저 변경한 후 화면에 나타내면 reflow를 줄일 수 있습니다.
7. **DOM 사용을 최소화합니다.**<br />
reflow 비용을 줄이기 위해서 DOM 노드 사용을 최소화 해야합니다. 한 가지 방법은 DOM Fragment를 사용하여 DOM을 추가할 때 마다 DOM 접근을 최소화 하는 방법입니다.
    ```javascript
        const frag = document.createDocumentFragment();
        const ul = frag.appendChild(document.createElement('ul'));

        for (let i = 1; i <= 3; i++) {
            li = ul.appendChild(document.createElement('li'));
            li.textContent = `item ${ i }`;
        }

        document.body.appendChild(frag);
    ```
    위의 코드와 같이 `createDocumentFragment` 를 사용하여 한 번에 DOM 을 추가하여 DOM 접근을 최소화 할 수 있습니다.
8. **캐시를 활용합니다**<br />
브라우저는 레이아웃 변경을 큐에 저장했다가 한 번에 실행하여 reflow를 최소화 합니다. 하지만 `offset`, `scrollTop` 과 같은 계산된 스타일 정보를 요청할 때마다 정확한 정보를 제공하기 위해 큐를 비우고 모든 변경사항을 적용합니다.
    ```javascript
        // 잘못된 예시
        for (let i = 0; i < len; i++) {
            el.style.top = `${ el.offsetTop + 10 }px`;
            el.style.left = `${ el.offsetLeft + 10 }px`;
        }

        // 좋은 예시
        let top = el.offsetTop, left = el.offsetLeft, elStyle = el.style;

        for (let i = 0; i < len; i++) {
            top += 10;
            left += 10;
            elStyle.top = `${ top }px`;
            elStyle.left = `${ left }px`;
        }
    ```
    이런 낭비를 해결하기 위해 위의 코드와 같이 스타일 정보를 변수에 저장하여 `offset`, `scrollTop` 등의 값 요청을 최소화해야 합니다.