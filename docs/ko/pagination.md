# 페이지네이션 📖

TOAST UI Grid는 데이터를 페이지 별로 나누어 볼 수 있도록 페이지네이션 기능을 제공한다. 단, 페이지네이션 기능은 [tui-pagination](https://github.com/nhn/tui.pagination)에 의존성을 가지고 있기 때문에 번들 파일에 [tui-pagination](https://github.com/nhn/tui.pagination) 내용이 추가된다. CDN을 통해 사용하는 경우, 반드시 아래처럼 `tui-pagination` 의존성을 추가해야한다.

```js
<script
  type="text/javascript"
  src="https://uicdn.toast.com/tui.pagination/v3.4.0/tui-pagination.js"
></script>
```

## 스타일

tui-pagination 스타일을 그대로 적용하고 싶다면 css 파일을 추가한다.

```js
import 'tui-pagination/dist/tui-pagination.css';
```

## 데이터 소스 연동

일반적으로 페이지네이션 기능과 함께 벡엔드와의 통신을 통해 원격 데이터를 사용하는 경우가 많다. 이런 경우, TOAST UI Grid의 [데이터 소스](https://github.com/nhn/tui.grid/blob/master/packages/toast-ui.grid/docs/ko/data-source.md)와 페이지네이션 기능을 연동하여 사용할 수 있다. 옵션 설정은 아래 예제와 같다.

```js
const grid = new Grid({
  // ...,
  pageOptions: { perPage: 10 },
});
```

위 예제처럼 `pageOptions.perPage`에 한 페이지에 보여줄 데이터 수를 설정한 후, 요청 데이터와 응답 데이터의 규격만 데이터 소스에서 정의한 규격에 맞춘다면 연동하여 사용할 수 있다. 관련된 내용은 [여기](https://github.com/nhn/tui.grid/blob/master/packages/toast-ui.grid/docs/ko/data-source.md)서 더 자세하게 확인할 수 있다.

## 클라이언트 페이지네이션

TOAST UI Grid는 백엔드와의 연동없이 Grid내의 데이터를 페이지 별로 나누어 볼 수 있도록 클라이언트 페이지네이션 기능을 제공한다. 클라이언트 페이지네이션 기능을 사용하기 위해 `pageOptions.useClient` 옵션을 반드시 `true`로 설정해야 한다. 설정 방법은 아래 예제와 같다.

```js
const grid = new Grid({
  // ...,
  pageOptions: {
    useClient: true,
    perPage: 10,
  },
});
```

> **참조**
> 클라이언트 페이지네이션 기능은 `v4.5.0` 이상부터 사용할 수 있다.

## API 동작 비교

특정 API들은 클라이언트 페이지네이션 기능과 데이터 소스 연동 페이지네이션 기능에서 다르게 동작한다.

| API          | 클라이언트 페이지네이션                                                   | 데이터 소스 연동 페이지네이션                          |
| ------------ | ------------------------------------------------------------------------- | ------------------------------------------------------ |
| `appendRow`  | 현재 페이지 데이터가 아닌 전체 데이터를 기준으로 로우를 추가한다.         | 현재 페이지 데이터를 기준으로 로우를 추가한다.         |
| `prependRow` | 현재 페이지 데이터가 아닌 전체 데이터를 기준으로 첫 번째 로우를 추가한다. | 현재 페이지 데이터를 기준으로 첫 번째 로우를 추가한다. |
| `removeRow`  | 현재 페이지 데이터가 아닌 전체 데이터를 기준으로 로우를 삭제된다.         | 현재 페이지 데이터를 기준으로 로우를 삭제된다.         |

## 페이지네이션 API 사용하기

다음과 같이 페이지네이션과 관련된 메서드를 호출할 수 있다.

| 이름            | 설명                                                                                                                               |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| `getPagination` | Grid에서 사용하고 있는 `tui-pagination`의 인스턴스를 반환한다. <br>(_페이지네이션 기능을 사용하지 않는 경우는 `null`을 반환한다._) |
| `setPerPage`    | 한 페이지에 보여줄 데이터 수를 변경한다.                                                                                           |

```js
const pagination = grid.getPagination();
const currentPage = pagination.getCurrentPage();
console.log(currentPage);

grid.setPerPage(10);
```

## 예제

클라이언트 페이지네이션 기능 예제는 [여기](http://nhn.github.io/tui.grid/latest/tutorial-example23-client-pagination)서, 데이터 소스 연동 페이지네이션 기능 예제는 [여기](https://nhn.github.io/tui.grid/latest/tutorial-example10-data-source)서 확인해 볼 수 있다.
