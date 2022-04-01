# Kakao Map React + Typescript에서 자유롭게 활용하기

## API KEY 발급 받기

[카카오맵 공식문서](https://apis.map.kakao.com/)

## API KEY 추가하기

```html
<script
  type="text/javascript"
  src="//dapi.kakao.com/v2/maps/sdk.js?appkey={발급받은 키}&libraries=services,clusterer,drawing"
></script>
```

## 지도 불러오기

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
