# 복합 컬럼 🔗

TOAST UI Grid는 컬럼들을 그룹 지어 부모 컬럼 헤더로 묶을 수 있다. `header.complexColumns` 옵션으로 여러 컬럼을 하나의 부모 헤더로 그룹 지어 트리 형태의 구조를 만들 수 있다. 부모 헤더 역시 또 다른 부모 헤더의 안으로 들어갈 수 있다.

`header.complexColumns` 옵션은 부모 컬럼을 정의한 데이터 객체의 배열을 사용한다. 일반 컬럼처럼 부모 컬럼은 `name` 속성과 `header` 속성을 가진다. 여기에 추가로 `childNames` 옵션을 가지는데, 이를 이용하여 부모 컬럼 밑에 들어갈 자식 컬럼의 목록을 설정할 수 있다.

다음 예제를 살펴보자.

```js
import Grid from 'tui-grid';

const grid = new Grid({
  el: document.getElementById('grid'),
  columns: [
    {
      header: 'col1',
      name: 'col1',
    },
    {
      header: 'col2',
      name: 'col2',
    },
    {
      header: 'col3',
      name: 'col3',
    },
  ],
  header: {
    complexColumns: [
      {
        header: 'col1 + col2',
        name: 'parent1',
        childNames: ['col1', 'col2'],
      },
      {
        header: 'col1 + col2 + col3',
        name: 'parent2',
        childNames: ['parent1', 'col3'],
      },
    ],
  },
});
```

`parent1` 컬럼은 이제 `col1` 과 `col2` 컬럼의 부모가 된다. 그리고 `parent1` 은 `col3` 컬럼을 포함하고 있는 `parent2` 컬럼의 자식이 된다.

복합 컬럼의 결과는 다음과 같다.

![그리드](https://user-images.githubusercontent.com/18183560/59605689-49023680-914a-11e9-99f9-25bb26316b04.png)

## 예제

Complex 컬럼을 사용하는 예제는 [여기](http://nhn.github.io/tui.grid/latest/tutorial-example02-complex-columns)서 확인할 수 있다.
