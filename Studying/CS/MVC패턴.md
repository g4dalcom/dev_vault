---
keyword : Spring
class : CS, Programming
---

## MVC?

-   `Model` `View` `Controller`
-   Model : 백그라운드에서 동작하는 logic을 처리한다.
-   View : 사용자가 보게 될 결과 화면을 출력한다.
-   Controller : 사용자의 입력처리와 흐름제어를 담당한다.

## MVC Pattern?

-   어플리케이션을 `Model` `View` `Controller` 세가지 역할로 구분한 개발 방법론이다.
-   사용자가 `Controller`를 조작하면 `Controller`는 `Model`을 통해서 데이터를 가져온다.
-   `Controller`는 받아온 정보를 바탕으로 시각적인 표현을 담당하는 `View`를 제어해서 사용자에게 전달한다.

[![test](https://user-images.githubusercontent.com/21440957/78374901-03dec080-7607-11ea-9de6-e9b2a8d2a7a2.png)](https://user-images.githubusercontent.com/21440957/78374901-03dec080-7607-11ea-9de6-e9b2a8d2a7a2.png)

## MVC Pattern을 Web에 적용한다면??

1.  사용자가 Web site에 접속한다.
2.  `Controller`는 사용자가 요청한 Web Page를 서비스하기 위해서 모델을 호출한다.
3.  `Model`은 데이터베이스나 파일과 같은 데이터 소스를 제어한 후에 결과를 반환한다.
4.  `Controller`는 `Model`이 반환한 결과를 `View`에 반영한다.
5.  데이터가 반영된 `View`는 사용자에게 보이게 된다.

## 장점

-   **유연**하고 **확장**에 용이하다.
-   **디자이너**와 **개발자**의 협업이 용이하다.
-   **유지보수 비용**을 절감할 수 있다.

## 단점

-   기본기능 설계를 위해 클래스들이 많이 필요하기 때문에 **복잡**할 수 있다.
-   **설계시간이 오래 걸리고** 숙련된 개발자가 필요하다.
-   Model과 View의 **완벽한 분리**가 어렵다.


## MVC 패턴 흐름


손님이 식당에 들어오면 메뉴판이 보여진다. 
= ( 사용자가 네이버 혹은 다음같은 홈페이지에 접속하면 뉴스, 웹툰 등 다양한 메뉴들이 보여진다.)

↓

손님이 먹고싶은 메뉴를 웨이터에게 주문한다.
= (홈페이지에서 보고싶은 메뉴를 클릭하면 컨트롤러에게 요청이 전달된다.)

↓

웨이터는 주방장에게 들어온 메뉴를 요청한다.
= (컨트롤러는 모델에 들어온 메뉴를 요청한다.)

↓

주방장은 메뉴를 요리한다.
= (모델은 들어온 요청에 관한 정보를 처리한다.)

↓

주방장이 완성된 요리를 웨이터에게 전달한다.
= (모델이 컨트롤러에 처리된 정보를 전달한다.)

↓

웨이터가 완성된 음식을 손님에게 가져다 준다.
=(컨트롤러가 뷰에 정보를 전달하면 뷰는 정보를 시각화하여 사용자에게 보여준다.)