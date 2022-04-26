---
layout: post
title: "[React] react-query 사용기"
date: 2022-04-20 08:00:00 +0530
categories: React
---

react-query의 장점과 react-query dev tools를 사용하기 위한 방법을 다루었습니다. react-query는 모자람이 없고 사용성이 좋습니다.

## React-query는 왜 쓸까?

1. 깔끔한 코드

> 코드의 간결화를 추구할 때에 react-query는 아주 훌륭합니다.

useState와 useEffect로 인한 부분들을 한 줄의 코드로 효과적으로 개선할 수 있습니다.

컴포넌트를 나누는 react의 특성상 api 호출과 render부분을 효율적으로 분리할 수 있습니다.

2. data의 호출에서 다양한 기능을 지원

> fetching, caching, synchronizing, updating

- fetching : 가져오는 것
- caching : `get 요청`과 비슷하게 캐싱을 해서 빠릅니다. 물론 get 요청도 똑같이 캐싱을 합니다만 get 요청보다 post 요청으로 데이터를 부르는 경우가 있을 시에는 캐싱을 하지 않습니다.
- synchronizing : 주기적으로 state 변화를 업데이트 할 수 있습니다. 직접 변화를 감지하는 것은 아니고 특정 조건이나 시간 조건을 걸어서 감지합니다.
- updating

3. react query dev tools
   > 상태값 조회에 사용됩니다. 한줄의 코드만 추가하면 redux의 logger 역할을 대신합니다.

오히려 훨씬 좋을 수도?...
logger는 좀 불편해요

<br>

### react-query의 사용성

<hr />

어떻게 사용하는지는 [React-query](https://react-query.tanstack.com/overview)에서 찾아보시면 됩니다.

```javascript
  const { state } = useLocation() as RouteState;
  const [loading, setLoading] = useState(true);
  const [info, setInfo] = useState<IInfoData>();
  const [priceInfo, setPriceInfo] = useState<IPriceData>();

useEffect(() => {
  (async () => {
    const infoData = await (
      await fetch(`https://api.coinpaprika.com/v1/coins/${coinId}`)
    ).json();
    const priceData = await (
      await fetch(`https://api.coinpaprika.com/v1/tickers/${coinId}`)
    ).json();
    setInfo(infoData);
    setPriceInfo(priceData);
    setLoading(false);
  })();
}, [coinId]);
```

이 분량의 코드를 놀랍게도

```javascript
    const { isLoading, data } = useQuery<ICoin[]>("allCoins", fetchCoinInfo);
    const { isLoading, data } = useQuery<ICoin[]>("allCoins", fetchCoinTickers);

    const { isLoading: infoLoading, data: infoData } = useQuery<IInfoData>(
        ["info", coinId],
        () => fetchCoinInfo(coinId!)
    );

    const { isLoading: tickerLoading, data: tickerData } = useQuery<IPriceData>(
        ["price", coinId],
        () => fetchCoinTickers(coinId!)
    );
```

로 줄일 수 있습니다.

<br>

### react-query dev tools

<hr>

> 당장 젹용할 수도 있습니다.

```javascript
import { ReactQueryDevtools } from "react-query/devtools";

<ReactQueryDevtools initialIsOpen={false} />;
```

참고링크
[Devtools for React Query](https://reactjsexample.com/devtools-for-react-query/)
