# 커스텀 컬럼 헤더 🔧

TOAST UI Grid는 컬럼 헤더의 UI를 커스터마이징할 수 있는 기능을 제공한다.

[커스텀 렌더러](./custom-renderer.md)와 유사하게 `HeaderRenderer` 생성자 함수의 인터페이스를 기반으로 컬럼 헤더를 커스터마이징 할 수 있다. TOAST UI Grid는 사용자가 등록한 `HeaderRenderer` 생성자 함수를 이용하여 내부적으로 인스턴스를 생성한 후, 반환된 엘리먼트를 DOM에 추가한다. 커스텀 컬럼 헤더는 `class` 키워드를 사용하여 선언하는 것을 권장하지만, 사용할 수 없는 경우 `function`과 `prototype`을 사용해도 무방하다.

`HeaderRenderer` 인터페이스는 다음과 같다.(`HeaderRenderer`의 인터페이스 구조는 [types/renderer/types.d.ts](https://github.com/nhn/tui.grid/blob/master/packages/toast-ui.grid/types/renderer/index.d.ts)을 참고한다.)

- `constructor`
  생성자 함수는 컬럼 헤더(`<th>`)가 DOM에 추가될 때 호출된다. 일반적으로 루트 엘리먼트를 인스턴스 멤버로 저장하는 작업을 수행한다. 이렇게 생성된 엘리먼트는 `getElement()` 메서드를 통해 접근할 수 있다. 생성자 함수의 인자로 넘어오는 객체의 인터페이스는 아래와 같다.

  | 속성         | 타입               | 반환 타입                                                                                                                                                                                                           |
  | ------------ | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
  | `grid`       | `Grid`             | `grid` 속성은 Grid 인스턴스를 참조하고 있다. Grid의 특정 데이터를 얻거나 직접 조작할 때 유용하게 사용할 수 있다.                                                                                                    |
  | `columnInfo` | `ColumnHeaderInfo` | `columnInfo` 속성은 해당 컬럼 헤더의 모든 정보를 담고 있다. `ColumnHeaderInfo`의 인터페이스는 [여기](https://github.com/nhn/tui.grid/blob/master/packages/toast-ui.grid/types/renderer/index.d.ts)에 정의되어 있다. |

- `getElement`
  컬럼 헤더의 루트 DOM 엘리먼트를 반환한다. 컬럼 헤더(`<th>` 엘리먼트)가 추가될 때, 반환된 엘리먼트가 자식으로 삽입된다.
- `mounted`
  `optional`이며, 인풋 엘리먼트를 초기화하는 데 사용한다. 이 메서드는 `getElement()`에서 반환되는 루트 엘리먼트가 DOM에 추가된 직후 호출된다.
- `render`
  컬럼 헤더의 상태을 동기화하는 데 사용된다.
- `beforeDestory`
  `optional`이며, 인풋 엘리먼트를 삭제할 때 사용할 수 있다. `getElement()` 로 반환된 엘리먼트가 DOM에서 제거되기 직전 실행된다.

다음은 커스텀 컬럼 헤더의 예제 코드이다.

```javascript
class CustomColumnHeader {
  constructor(props) {
    const columnInfo = props.columnInfo;
    const el = document.createElement('div');
    el.className = 'custom';
    el.textContent = `custom_${columnInfo.header}`;
    this.el = el;
  }

  getElement() {
    return this.el;
  }

  render(props) {
    this.el.textContent = `custom_${props.columnInfo.header}`;
  }
}
```

위 코드에서 정의한 `CustomColumnHeader`를 적용하기 위해서 `header` 옵션의 `columns` 배열에 제공되는 컬럼 정보 객체에 추가 설정을 해야 한다. 컬럼 정보 객체의 `name` 속성에는 커스터마이징을 원하는 헤더의 `name` 을 설정하고, `renderer` 속성에는 정의한 커스텀 컬럼 헤더를 설정한다. 또한 [복합 컬럼](./complex-columns.md)에 커스텀 컬럼 헤더를 적용하고 싶은 경우, `header` 옵션의 `complexColumns` 배열내에 동일하게 적용 가능하다.

```javascript
import Grid from 'tui-grid';

const grid = new Grid({
  // ...,
  header: {
    height: 100,
    complexColumns: [
      {
        header: 'info',
        name: 'mergeColumn1',
        childNames: ['id', 'name'],
        renderer: CustomColumnHeader,
      },
    ],
    columns: [
      {
        name: 'id',
        renderer: CustomColumnHeader,
      },
    ],
  },
});
```

> **참조**
>
> - 커스텀 컬럼 헤더는 `v4.7.0` 이상부터 사용할 수 있다.
> - 컬럼의 **sortable**, **filter** 옵션은 커스텀 컬럼 헤더에서는 무시된다.
