# Kakao Map React + Typescript에서 자유롭게 활용하기

## API KEY 발급 받기

[카카오맵 공식문서](https://apis.map.kakao.com/)

## API KEY 추가하기

- root에 `.env`파일 생성
- react 프로젝트에서 환경변수를 사용하려면 `REACT_APP` 키워드를 붙여야한다.

```env
REACT_APP_KAKAO_MAP_KEY=[JavaScript 키]
```

## API KEY 불러오기

`./public/index.html` 파일에 스크립트 태그 추가

```html
<script
  type="text/javascript"
  src="//dapi.kakao.com/v2/maps/sdk.js?appkey=%REACT_APP_KAKAO_MAP_KEY%"
></script>
```

## 지도 불러오기

`src/component/Map.tsx`

```js
import { useEffect } from 'react';

declare global {
  interface Window {
    kakao: any;
  }
}
export default function Map() {
  useEffect(() => {
    const container = document.getElementById('map');
    const options = {
      center: new window.kakao.maps.LatLng(33.450701, 126.570667),
    };
    const map = new window.kakao.maps.Map(container, options);
  }, []);

  return (
    <div id="map" style={{ width: '100%', height: '100vh', zIndex: 1 }}>
    </div>
  );
}
```

카카오맵은 `id=map`인 element를 찾아 렌더링 한다. 그리고 인라인 스타일로 `width, height`값을 설정해준다.

그리고 **kakao를 글로벌로 선언**해주어야 한다.

```js
declare global {
  interface Window {
    kakao: any;
  }
}
```
