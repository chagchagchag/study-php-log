## Controller, View, Model

## 강의 링크

- [Controller](https://opentutorials.org/module/327/3829)
  - github : https://github.com/egoing/codeigniter_codeingeverbody/tree/Controller
  - 참고
    - [Controller 메뉴얼 (한글)](http://codeigniter-kr.org/user_guide_2.1.0/general/controllers.html)
    - [Controller 메뉴얼 (영문)](http://ellislab.com/codeigniter/user-guide/general/views.html)
- [View](https://opentutorials.org/module/327/3826)
  - github : https://github.com/egoing/codeigniter_codeingeverbody/tree/View
  - 참고
    - [view 메뉴얼 (한글)](http://codeigniter-kr.org/user_guide_2.1.0/general/views.html)
    - [View 메뉴얼 (영문)](http://ellislab.com/codeigniter/user-guide/general/views.html)
- [Model](https://opentutorials.org/module/327/3827)



<br/>



## Controller

**http://ooo2.org/index.php/topic**

- index.php 뒤에 topic 이라는 경로를 사용하고 싶다면, controllers 디렉터리 밑에 topic.php 라는 이름의 파일을 생성해야 합니다.
- 이 파일 내에 정의하는 클래스는 CI\_Controller 라는 이름의 클래스를 상속한 Topic 이라는 이름으로 정의해야 합니다.
- `class Topic extends CI_Controller{ ... }`

<br/>

```php+HTML
<?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
class Topic extends CI_Controller {
    function index(){
        echo '
        <!DOCTYPE html>
        <html>
            <head>
                <meta charset="utf-8"/>
            </head>
            <body>
                토픽 메인 페이지
            </body>
        </html>
        ';
    }
    # ...
}
?>
```

- **http://ooo2.org/index.php/topic** 을 접속했을 때 표현할 index 페이지는 위와 같이 `index()` 함수에 정의해줍니다.

<br/>



**http://ooo2.org/index.php/topic/get**

- topic 뒤에 get 이라는 경로를 추가하고 싶을 경우 `Topic` 클래스 내에 get() 이라는 함수를 추가해줍니다.

```php+HTML
<?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
class Topic extends CI_Controller {
    # ...
    function get($id){
        echo '
        <!DOCTYPE html>
        <html>
            <head>
                <meta charset="utf-8"/>
            </head>
            <body>
                토픽 '.$id.'
            </body>
        </html>
        ';
    }
}
?>
```

<br/>



**http://ooo2.org/index.php/topic/get/1**

- get 뒤에 3 이라는 숫자를 지정하는 방식의 Path Variable 을 처리가 가능하도록 하고 싶다면, get() 함수 내에 인자값을 지정하면 됩니다. 아래 코드에서 `(1) 로 표시한 부분입니다.

```php+HTML
<?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
class Topic extends CI_Controller {
    # ...
    function get($id){
        echo '
        <!DOCTYPE html>
        <html>
            <head>
                <meta charset="utf-8"/>
            </head>
            <body>
                토픽 '.$id.'
            </body>
        </html>
        ';
    }
}
?>
```

<br/>



## View

Controller 예제에서는 html 코드를 문자열로 만들어서 echo 하도록 했었습니다. 하지만 화면에서 처리해야 하는 비즈니스 요구사항이 많아지고 기획이 복잡해질 수록 이렇게 echo 로만 표현하는 데에는 무리가 있습니다. <br/>

이런 이유로 php 에서는 html 코드만을 담당하는 View 계층을 따로 두고 있습니다. 쉽게 설명하면 Java 의 JSP, 윈도우 닷넷의 ASP와 유사한 개념입니다.<br/>



### e.g. head.php

예제 리포지터리에서는 application/views/head.php 입니다.

- 링크 : https://github.com/egoing/codeigniter_codeingeverbody/blob/View/application/views/head.php

```php+HTML
<!DOCTYPE html>
        <html>
            <head>
                <meta charset="utf-8"/>
            </head>
            <body>
```

<br/>



### e.g. footer.php

예제 리포지터리에서는 application/views/footer.php 입니다.

- 링크 : https://github.com/egoing/codeigniter_codeingeverbody/blob/View/application/views/footer.php

```php+HTML
            </body>
        </html>
```

<br/>



### e.g. main.php

예제 리포지터리에서는 application/views/main.php 입니다.

- 링크 : https://github.com/egoing/codeigniter_codeingeverbody/blob/View/application/views/main.php

```php+HTML
토픽 페이지
```

<br/>



### e.g. get.php

예제 리포지터리에서는 application/views/get.php 입니다.

- 링크 : https://github.com/egoing/codeigniter_codeingeverbody/blob/View/application/views/get.php

```php+HTML
토픽 <?=$id?>
```

<br/>



### Controller 에서 view 를 조합

예제 리포지터리에서는 application/controllers/topic.php 입니다.

- 링크 : https://github.com/egoing/codeigniter_codeingeverbody/blob/View/application/controllers/topic.php

Controller 를 정의했던 topic.php 에서 위의 head,main,footer,get 뷰들을 조합해보겠습니다.

```php+HTML
<?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
class Topic extends CI_Controller {
    function index(){
        $this->load->view('head');
        $this->load->view('main');
        $this->load->view('footer');
    }
    function get($id){
        $this->load->view('head');
        $this->load->view('get', array('id'=>$id));
        $this->load->view('footer');
    }
}
?>
```

<br/>



## Model









