# 테마 👨‍🎨

TOAST UI Grid는 `applyTheme()` 메서드를 이용하여 쉽게 Grid의 전체 스타일을 바꾸고 사용자가 원하는 대로 Grid를 꾸밀 수 있다.

### 내장 프리셋 사용하기

TOAST UI Grid에는 3가지(**default**, **striped**, **clean**) 내장 프리셋이 있다. 내장 프리셋을 적용하기 위해서 사용자는 단 한 줄의 코드만 입력하면 된다.

```js
import Grid from 'tui-grid';

Grid.applyTheme('default');
```

위 코드를 실행하거나 프리셋을 적용하지 않으면 **default** 프리셋이 적용된다. **default**를 적용한 결과는 다음과 같다.

![theme_default](https://user-images.githubusercontent.com/35371660/59335524-b3c10580-8d37-11e9-9ad6-a74e1f30896e.png)

**striped** 프리셋을 적용하면 테이블에 줄무늬가 추가된다.

```js
Grid.applyTheme('striped');
```

**striped**를 적용한 결과는 다음과 같다.

![theme_striped](https://user-images.githubusercontent.com/35371660/59335525-b3c10580-8d37-11e9-8d0a-4fc67c58cb6b.png)

좀 더 깔끔하고 기본적인 스타일을 원한다면 **clean** 프리셋을 사용한다.

```js
Grid.applyTheme('clean');
```

**clean**를 적용한 결과는 다음과 같다.

![theme_clean](https://user-images.githubusercontent.com/35371660/59335522-b3c10580-8d37-11e9-83aa-a7cd6e9bbdc6.png)

### 테마 커스터마이징

Grid에 자신만의 스타일을 적용하고 싶은 경우, 프리셋 테마에 옵션을 추가해 확장한다. `applyTheme()` 메서드의 두 번째 인자는 확장할 테마 옵션이다. 예를 들어 헤더 영역의 셀과 짝수 번째 셀의 배경색을 바꾼 **striped** 프리셋을 사용하고 싶다면 다음과 같이 적용할 수 있다.

```js
Grid.applyTheme('striped', {
  cell: {
    header: {
      background: '#eef',
    },
    evenRow: {
      background: '#fee',
    },
  },
});
```

위 코드를 적용한 결과는 다음과 같다.

![theme_custom](https://user-images.githubusercontent.com/35371660/59335763-321da780-8d38-11e9-89db-fbd0620ce9e2.png)

다음은 **default** 프리셋을 커스터마이징 한 예제다. 추가 설정할 수 있는 옵션은 **clean** 프리셋과 동일하다. 다음 결과로 **default**와 **clean** 프리셋을 비교할 수 있다.

```js
Grid.applyTheme('default', {
  cell: {
    normal: {
      background: '#fff',
      border: '#e0e0e0',
      showVerticalBorder: false,
      showHorizontalBorder: true,
    },
    header: {
      background: '#fff',
      border: '#e0e0e0',
    },
    selectedHeader: {
      background: '#e0e0e0',
    },
  },
});
```

모든 옵션은 [API 문서](http://nhn.github.io/tui.grid/latest)의 `Grid.applyTheme()` 부분에서 확인할 수 있다.

## 예제

[여기](http://nhn.github.io/tui.grid/latest/tutorial-example07-themes)서 예제 Grid에 프리셋 테마와 커스터마이즈 옵션을 덧붙여볼 수 있다.
