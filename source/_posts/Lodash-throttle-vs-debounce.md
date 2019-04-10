---
title: lodash - throttle vs debounce
date: 2019-01-24 15:55:41
tags: 
- javascript
- lodash.js
- underscore.js
categories: Web
---
![lodash](/images/lodash.png)

# 들어가기 전에
자바스크립트를 특성상 이벤트는 연속적으로 발생한다. (eg. `scroll`, `resize`, `keydown`) 기본적으로 이 이벤트들의 발생량을 제어 할 수 없으며 심지어 엄청나게 많이 발생하는 경우도 있다.
(`window`에 `onresize`이벤트의 리스너에 `console.log()`를 걸고 화면을 줄였다 늘였다 해보자.)
만약 작업이 느리거나 무거운 경우 과도한 이벤트로인해 퍼포먼스가 심각하게 떨어지는것은 당연한 일이다, 따라서 많은 이벤트가 발생하더라도 퍼포먼스에 문제가 없도록 제어할 수있는 `Throttle`과 `Debounce`의 차이에 대하여 간략하게 정리해보고자 한다.

# Throttle
`Throttle`은 특정시간마다 이벤트 발생량을 일정하게 제어 할수 있는 기능이다.
만약 개발중인 사이트에서 스크롤을 올리거나 내릴때 혹은 뷰포트 사이즈가 변경 될 때마다 무겁거나 복잡한 작업을 한다면 이벤트의 발생량이 많기 때문에 퍼포먼스의 문제가 발생할 요지가 있다, 그럴 경우 `Throttle`을 사용하여 특정시간마다 한번씩 이벤트를 발생 하게 할 수 있다. 

아래 코드펜의 예제를 통해 쉽게 이해 할 수 있다. 이벤트가 1초마다 발생하고 2초 단위로 throttle을 설정 했을때를 가정하고 만들었다.
{% codepen bzNjEz result 600 100% anonymous dark %}

추가적으로 `Throttle`의 옵션인 `leading`과 `trailing`에 대해서도 쉽게 이해 할 수 있다. 
`lodash`의 경우 `leading`과 `trailing`의 기본값이 `true`이므로 원하는 옵션을 제어하자 

# Debounce
`Debounce`는 연속되는 이벤트가 더 이상 발생하지 않을경우 때 액션을 실행 하고자 할때 유용하다.
가장 익숙한 예로는 보통 회원 가입시 이메일의 중복 확인이나 검색 필드의 자동완성의 경우다, `input`의 `change` 이벤트가 발생 할때마다 매번 `Ajax Call`이 실행 되는 경우
불 필요한 통신과 BackEnd의 자원까지 낭비시키게 될 것이다. 이 경우 `Debounce`가 유용할 것이다.

{% codepen MLwLgV result 300 100% anonymous dark %}
# 정리

`Throttle` **특정시간마다 이벤트 발생량을 일정하게 제어해야 하는 경우 (eg. Scroll Event, Viewport Size Event)**
`Debounce` **연속적인 이벤트가 발생후 마지막 이벤트로 부터 특정시간 이후 작업을 실행하는 경우 (eg. Ajax Call)**

{% codepen RvNxQN result 500 100% anonymous dark %}