---
layout:     post
title:      "AngularJS 스타일 가이드 소개"
date:       2016-11-11 00:00:00
categories: tech
summary:    이 글은 Francesco Iovine의 An Introduction to AngularJS Style Guides를 한국어로 번역한 것입니다.
---

같은 깃허브에 공유 되어 있는 글을 제가 쉽게 보기위해 남기는 글입니다. <br>
[HyunSeob](https://hyunseob.github.io/)님 블로그에서 번역글을 가져왔습니다. <br>
감사합니다.

---

이 글은 Francesco Iovine의 An Introduction to AngularJS Style Guides를 한국어로 번역한 것입니다. 오역 제보나 더 나은 번역 제안은 언제나 감사합니다!

스타일 가이드란 무엇일까? AngularJS 프로젝트는 스타일 가이드를 필요로 할까? 필요로 한다면 왜일까? 무엇이 가장 유명한 AngularJS 스타일 가이드일까? 어떻게 스타일 가이드를 개발팀에 도입할 수 있을까? 이 글은 이러한 질문에 대한 해답이 될 것이다. AngularJS 스타일 가이드를 다루기 전에, 스타일 가이드가 무엇인지, 그리고 왜 개발자들이 스타일 가이드를 필요로 하는지 알아보자.

---


## 왜 스타일 가이드를 사용해야 할까?

[위키피디아](https://en.wikipedia.org/wiki/Style_guide)에서 스타일 가이드가 왜 중요한 지에 대해 이해하고, AngularJS 스타일 가이드를 다루기 전에 큰 그림을 보는데에 도움이 될만한 일반적인 정의를 참고하자.

스타일 가이드는 특정 포맷, 조직, 혹은 분야에서 모두 쓰이는 문서를 작성하거나 설계하기 위해 쓰이는 표준의 집합이다. 스타일 가이드는 더 나은 커뮤니케이션을 위해 만들어지고 시행된다. 그러기 위해서는 하나의 문서 내에서, 혹은 여러 문서에 걸쳐 일관성을 보장해야 하고, 언어적 요소, 시각적 요소, 맞춤법 및 타이포그래피의 모범 사례(best practice)를 준수하도록 해야 한다. 또한 학술 및 기술 문서의 스타일 가이드는 윤리(저자나 연구 윤리 및 공개)와 교육학(설명방법 및 표현의 명확성) 및 기술적인 규제나 규정같은 것들도 준수하도록 해야한다.

위와 같이 코딩 스타일 가이드는 특정한 언어와 그 가이드를 사용하는 조직의 필요에 의해서 모범사례(best practice)를 준수하도록 해야한다.

### 프로젝트의 스타일 가이드

JavaScript 프로젝트가 스타일 가이드를 필요로 하는 이유는 정말 많다. 이 글에서는 모든 세부적인 내용을 다루지는 않을 것이지만, 그런 내용들은 보통 언어 자체의 스타일 가이드에 다음과 같은 주제를 더해 확장할 수 있다.

1. 모듈화: 단일 책임, IIFE(Immediately invoked function expression), 모듈 의존성
1. 어플리케이션 구조: 패턴화된 구조, 폴더 구조
1. 네이밍 컨벤션: 모듈, 컨트롤러, 설정 및 명세 파일의 네이밍 컨벤션
1. Linting: JavaScript 코드 체크 도구
1. 테스팅: 명세 작성에 대한 접근법
1. 주석: 문서화를 제공하기 위함
1. 실행시의 로직: 설정 및 실행 시 로직
1. 라우팅: 내비게이션 흐름, 뷰의 구성
1. 예외 처리: 데코레이터, Exception catcher, 라우팅 에러
1. 성능 및 보안: 압축, 난독화

### 기존의 JavaScript 스타일 가이드

범용적인, 혹은 특정 프로젝트에 특화된 다양한 JavaScript 스타일 가이드가 있다.

- [Google JavaScript Guide](https://google.github.io/styleguide/javascriptguide.xml)
- [MDN - Coding style](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Coding_Style)
- [더글라스 크록포드의 코드 컨벤션](http://javascript.crockford.com/code.html)
- [Waldron의 idiomatic.js](https://github.com/rwaldron/idiomatic.js/)
- [npm’s “funny” coding style](https://docs.npmjs.com/misc/coding-style)
- [jQuery’s JavaScript Style Guide](https://contribute.jquery.org/style-guide/js/)
- [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)

위 가이드들의 작성자가 모두 유명한 사람이나 회사지만, 언급한 스타일 가이드는 모두 범용적인 가이드이다. 내 생각에는 Airbnb의 스타일 가이드가 가장 최신이며 범용적이고, 코드 스타일을 체크할 수 있도록 ESLint 설정 파일까지 제공하고 있다. ESLint 설정파일은 내가 포트폴리오를 구현할 때 썼던 것처럼 확장 가능하다.

## AngularJS 프로젝트에 스타일 가이드가 필요한 이유

모든 JavaScript 프로젝트가 스타일 가이드를 필요로 하는 것과 같은 이유로, AngularJS 프로젝트도 스타일 가이드가 필요하다. 고려해야 할 만한 몇 가지 Angular 특정 주제들이 있다.

다음과 같은 Angular 특정 주제들을 생각해 볼 수 있다.

- ng 태그를 사용하는 법: AngularJS의 ng 디렉티브는 여러가지 방법으로 사용될 수 있으며, 다양한 문법으로도 사용할 수 있다. 예를 들면, W3C 표준에 맞춰 ng 대신 data-ng가 권장되는 것을 꼽을 수 있겠다. 스타일 가이드에 ng 디렉티브를 어떻게 써야할지 명세하면 HTML 파일의 일관성을 향상시키는데 도움이 될 것이다.
- 컴포넌트를 구현하는 여러가지 방법: AngularJS에서는 커스텀 디렉티브를 사용해서 웹 컴포넌트를 구현한다. 커스텀 디렉티브는 HTML 요소의 이름(name), 속성(attribute), 클래스 명이나 주석으로도 만들 수 있다. 스타일 가이드는 프로젝트 내에서 사용되는 디렉티브 구현방법에 대해서 한 가지 형태만 사용하도록 보장해야 할지도 모른다.
- 아키텍처 패턴 채택: AngularJS는 MV* (혹은 MVW) 아키텍처 패턴을 허용한다. JavaScript 개발자들에게 어플리케이션을 MVC 패턴으로 구현할지 MVVM 패턴으로 구현할지 선택권을 남기는 것이다. 이러한 접근 방법에 대한 가이드라인은 팀 전체를 같은 선상에 있도록 도와준다.

이제 스타일 가이드가 왜 필요한지 알았으니, 유명한 AngularJS 스타일 가이드를 배워보자.

## AngularJS 스타일 가이드

구글은 [공식 스타일](https://google.github.io/styleguide/angularjs-google-style.html) 가이드와 [모범사례](https://github.com/angular/angular.js/wiki/Best-Practices)를 제공한다. 그러나 AngularJS 커뮤니티에서 가장 유명하고 범용적인 스타일 가이드는 다음과 같다.


- [Minko Gechev의 AngularJS 스타일 가이드](https://github.com/mgechev/angularjs-style-guide)
- [Todd Motto의 AngularJS 스타일 가이드](https://github.com/toddmotto/angular-styleguide)
- [John Papa의 AngularJS 스타일 가이드](https://github.com/johnpapa/angular-styleguide)

모두 좋은 스타일 가이드라서 뭐가 최고라고 말하기 어렵다. John Papa의 가이드는 범용적이고 계속 개선되고 있으며, Todd Motto의 가이드는 간결하며 시작할 때 좋다. 그리고 Minko Gechev의 가이드는 여러 언어로 번역되었다. 하지만 John Papa의 스타일 가이드는 가장 최신이고 상세한 AngularJS 스타일 가이드로서 공식적으로 추천된 것으로 보인다.

새로운 AngularJS 프로젝트를 시작할 때 John Papa의 스타일 가이드에서 가장 중요하게 고려해봐야 할 점은 다음과 같다.

- LIFT 원칙
- controllerAs 문법
- 파일 템플릿과 스니펫(Snippet)
- 시드(Seed) 어플리케이션

### LIFT 원칙

LIFT 원칙은 어플리케이션 구조와 연관이 있으며, 다음과 같은 가이드라인으로 정의할 수 있다.

- Locate your code quickly: 빠르게 코드를 추적가능하게 하라
- Identify the code at a glance: 한 눈에 코드를 구분할 수 있게 하라
- keep the Flattest structure you can: 최대한 단순한 구조를 유지해라
- Try to stay DRY: 반복작업을 피하라

이 원칙은 어플리케이션 구조를 더 확장에 유연하게 만들어주고 코드를 더 빠르게 찾을 수 있기 때문에 개발자들이 더 효율적으로 일할 수 있다. 기능에 의한 폴더 구조를 사용하면 자연스럽게 이 원칙을 따르는 데 도움이 될 것이다.

### ControllerAs

`$scope`를 사용하는 컨트롤러에 controllerAs문법을 사용하면 뷰에서 코드의 가독성을 다음과 같이 향상 시킬 수 있다.

```html
<!-- avoid -->
<div ng-controller="CustomerController">
  {{ name }}
</div>
<!-- recommended -->
<div ng-controller="CustomerController as customer">
  {{ customer.name }}
</div>
```

```typescript
/* avoid */
function CustomerController($scope) {
  $scope.name = {};
  $scope.sendMessage = function() { };
}
/* better */
function CustomerController() {
  this.name = {};
  this.sendMessage = function() { };
}
```

더 나아가, `this`를 변수에 할당함으로써 컨트롤러 메소드에서도 `this`에 쉽게 접근할 수 있다.

```javascript
/* recommended */
function CustomerController() {
  var customerVM = this;
  customerVM.name = {};
  customerVM.sendMessage = function() {
    // customerVM을 통해 컨트롤러의 scope에 접근할 수 있다.
  };
}
```

### 파일 템플릿과 스니펫(Snippet)

John Papa의 가이드에는 다양한 에디터와 IDE를 위해 많은 파일 [템플릿과 스니펫](https://github.com/johnpapa/angular-styleguide/blob/master/a1%2Fi18n%2Fko-KR.md#file-templates-and-snippets)이 나열되어 있다. 파일 템플릿과 스니펫은 서로 다른 파일, 모듈, 서브시스템에 대해 일관성을 보장한다. 특히, 팀으로 일한다면 파일 템플릿과 스니펫을 사용함으로서 리팩토링하는 시간이나 새로운 개발자가 팀에 합류했을 때 많은 시간을 아낄 수 있을 것이다. 또한 프로젝트의 코드를 깔끔하게, 그리고 재사용성을 좋게 유지하는데에도 도움이 된다.

### 시드(Seed) 어플리케이션

새로운 AngularJS 프로젝트를 시작할 때, 좀 급하거나 완성된 예제에서 배우고자 한다면, [HotTowel](https://github.com/johnpapa/generator-hottowel)을 고려할만하다. 이 [Yeoman](http://yeoman.io) 제너레이터는 JohnPapa의 스타일 가이드를 따른 AngularJS 어플리케이션의 시작점을 제공한다. 생성된 어플리케이션의 환경은 npm 패키지, gulp 파일, JavaScript와 LESS hingting 도구 등으로 구성되어 있으므로, 특별히 다른 게 필요없다면 바로 새로운 기능 구현을 하면 된다! 나의 GitHub AngularJS 놀이터에 있는 [HotTowel을 사용해서 AngularJS 어플리케이션을 동작시키는 법](https://github.com/franciov/angularjs-sample-app/tree/styleguide/yeoman-generator/angular1/hottowel)도 참고하기 바란다.

### 실제 사례

스타일 가이드를 실제로 사용하고 있는 사례로 [GoCardless AngularJS Styleguide](https://github.com/gocardless/angularjs-style-guide)가 있다. 이 가이드에서는 좀 더 특수하게 발전된 코드 스니펫을 발견할 수 있다. 이 스타일 가이드는 HTML에 컨트롤러를 사용하는 것보다 디렉티브를 사용할 것을 권장한다. 디렉티브의 이름에 대한 가이드라인은 다음과 같다.

디렉티브 이름은 반드시 a-z만을 사용해야하고 최소한 하나 이상의 대시(-)를 포함해야한다. 커스텀 요소(element)는 네이티브 요소와 구분하기 위해서 반드시 대시(혹은 네임스페이스)를 포함해서 나중에 일어날 수 있는 컴포넌트 충돌을 예방해야 한다.

```html
<!-- Recommended -->
<dialog-box></dialog-box>
<button click-toggle="isActive"></button>
<!-- Avoid -->
<dialog></dialog>
<button toggle="isActive"></button>
```

GoCardless AngularJS 스타일 가이드는 앞서 언급했던 포괄적인 스타일 가이드를 팀이나 프로젝트의 요구에 맞게 확장하고 커스터마이징할 때 좋은 참고가 될 수 있다.

### 팀에서의 스타일 가이드 사용

대부분의 AngularJS 프로젝트에는 코드 스타일 가이드가 필요하다. 특히, 새로운 팀이거나 프로젝트가 빠르게 성장할 것으로 예측될 경우 더욱 그렇다. 또한, 코드 스타일 가이드는 프로젝트를 진행하는 동안 반드시 지켜져야 하고 새로운 요구나 새로운 부분이 발견될 경우 변경되거나 확장될 수 있어야 한다.

### 2016년, 그리고 그 이후

근미래에 모든 것들은 빠르게 변할 것이다. 다음 과제는 AngularJS2를 위한 스타일 가이드일 것이다. 특히, 웹 컴포넌트, ECMAScript 2015(ES6), ES2016 이후의 JavaScript와 함께 개발하는 것에 대해서 중점적으로 업데이트 할 것이다.

번역글 원문 링크 : [원문보기](https://hyunseob.github.io/2016/04/10/introduction-to-angularjs-style-guide/index.html)