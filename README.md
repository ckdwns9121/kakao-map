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

## useEffect로 카카오맵 렌더링하기

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

![결과](https://user-images.githubusercontent.com/40492343/161256565-664f57dd-88cf-4a30-b175-fc205d2823b8.png)

## global Interface 생성

```js
declare global {
  interface Window {
    kakao: any;
  }
}
```

`window.kakao`를 사용하기 위해 **kakao를 글로벌로 선언**해주어야 한다.

## 클러스터 생성

```js
 import { useEffect , useRef } from 'react';

declare global {
  interface Window {
    kakao: any;
  }
}
export default function Map() {

  const cluster = useRef<any>(null);
  const kakaoMap = useRef<any>(null);

   const onCreateCluster = () => {

    const map = kakaoMap.current;

    cluster.current = new window.kakao.maps.MarkerClusterer({
      map: map, // 마커들을 클러스터로 관리하고 표시할 지도 객체
      averageCenter: true, // 클러스터에 포함된 마커들의 평균 위치를 클러스터 마커 위치로 설정
      minLevel: 1, // 클러스터 할 최소 지도 레벨
      disableClickZoom: true, // 클러스터 마커를 클릭했을 때 지도가 확대되지 않도록 설정한다
      styles: [
        {

          width: '40px',
          height: '40px',
          background: 'rgba(34, 34, 34, .8)',
          borderRadius: '30px',
          color: '#fff',
          boxSizing: 'border-box',
          fontSize: '15px',
          textAlign: 'center',
          fontWeight: 'bold',
          lineHeight: '40px',
          opacity: '0.95',
        },
      ],
    });

    /* 클러스터링 최소 하나 */
    cluster.current.setMinClusterSize(1);
    cluster.current.addMarkers(list);
  };

  useEffect(() => {
    const container = document.getElementById('map');
    const options = {
      center: new window.kakao.maps.LatLng(33.450701, 126.570667),
    };
    const map = new window.kakao.maps.Map(container, options);
    kakaoMap.current= map;
  }, []);

  useEffect(()=>{
    onCreateCluster();
  },[])

  return (
    <div id="map" style={{ width: '100%', height: '100vh', zIndex: 1 }}>
    </div>
  );
}
```

<span>
<img src="https://user-images.githubusercontent.com/40492343/161256603-8c43ddd2-9070-4452-b499-fb7434ee2b36.jpg">
</span>
