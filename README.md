# Starbucks

FASTCAMPUS 강의를 바탕으로 제작된 웹 어플리케이션 입니다. <br />
순수 HTML, CSS, Javascript 를 이용하였습니다. <br />
아래부터는 학습 내용을 정리한 문서로 주로 몰랐거나, 앞으로 자주 사용할 내용을 바탕으로 작성하였습니다.

<br />

## throttle (lodash 라이브러리)

스크롤 입력이 들어올 때 마다 'Scroll!'를 출력하는 코드가 있다.

```javascript
window.addEventListener("scroll", () => {
  console.log("Scroll!");
});
```

- 페이지를 쭉 아래로 내리면 생각보다 상당히 많은 Scroll! 문자가 출력된다.
- 입력 간에 익명의 함수가 너무 많이 호출되지 않도록 제어를 하려 한다.
  - 이 때 사용하는 것이 `throttle` 이다.

우선 lodash 라이브러리를 가져온다. <br />
[lodash cdn 페이지](https://cdnjs.com/libraries/lodash.js)

```html
<script
  src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.21/lodash.min.js"
  integrity="sha512-WFN04846sdKMIP5LKNphMaWzU7YpMyCU245etK3g/2ARYbPK9Ub18eG+ljU96qKRCWh+quCY7yefSmlkQw1ANQ=="
  crossorigin="anonymous"
  referrerpolicy="no-referrer"
></script>
```

위 스크립트 태그를 index.html 의 head 태그 안에 붙여넣기 한다.

성공적으로 lodash 라이브러리를 가져왔다면 아래와 같이 throttle 함수를 사용할 수 있게 된다.

```javascript
window.addEventListener(
  "scroll",
  _.throttle(function () {
    console.log("Scroll !");
  }, 300)
);
// 0.3초에 한 번 scroll event 에 대한 함수를 실행하도록 한다.
// _.throttle(함수, 시간)
```

<br />

## 스크롤 위치에 따른 스타일 변화

현재 윈도우의 Y 축에 대한 값은 아래와 같이 구할 수 있음.

```javascript
window.scrollY;
```

이를 바탕으로 아래와 같이 특정 위치 아래로 스크롤이 되면 요소의 스타일이 변하도록 할 수 있다.

```javascript
const badgeEl = document.querySelector("header .badges");
window.addEventListener(
  "scroll",
  _.throttle(function () {
    if (window.scrollY > 500) {
      badgeEl.style.display = "none";
    } else {
      badgeEl.style.display = "block";
    }
  })
);
```

<br />

### GSAP 라이브러리를 이용한 애니메이션 제어

라이브러리를 가져오자. <br />
[GSAP cdn](https://cdnjs.com/libraries/gsap)

```html
<script
  src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.21/lodash.min.js"
  integrity="sha512-WFN04846sdKMIP5LKNphMaWzU7YpMyCU245etK3g/2ARYbPK9Ub18eG+ljU96qKRCWh+quCY7yefSmlkQw1ANQ=="
  crossorigin="anonymous"
  referrerpolicy="no-referrer"
></script>
```

위 태그를 헤드 태그에 붙혀넣기 해준다.

`to()` 라는 메서드를 이용해본다.

기본적인 사용법은 아래와 같다.

`gsap.to(요소, 지속시간, 옵션)`

```javascript
window.addEventListener('scroll', ._throttle(function() {
  if (window.scrollY > 500) {
    gsap.to(badgeEl, .6, {
      opacity: 0,
      display: 'none'
    })
  } else {
    gsap.to(badgeEl, .6, {
      opacity: 1,
      display: 'block'
    })
  }
})
```
