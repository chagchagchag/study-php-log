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

> 문서 : [Controller](https://opentutorials.org/module/327/3829)

<br/>

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

> 문서 : [View](https://opentutorials.org/module/327/3826)

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

> 문서 : [Model](https://opentutorials.org/module/327/3827)

데이터 액새스 계층을 Model 이라고 이야기합니다. CodeIgniter 예제 프로젝트에서는 application/config/database.php 에 정의되어 있습니다.

- 링크 : https://github.com/egoing/codeigniter_codeingeverbody/blob/View/application/config/database.php

<br/>

```php
<?php  if ( ! defined('BASEPATH')) exit('No direct script access allowed');

# ...

$active_group = 'default';
$active_record = TRUE;

$db['default']['hostname'] = 'localhost';
$db['default']['username'] = '';
$db['default']['password'] = '';
$db['default']['database'] = '';
$db['default']['dbdriver'] = 'mysql';
$db['default']['dbprefix'] = '';
$db['default']['pconnect'] = TRUE;
$db['default']['db_debug'] = TRUE;
$db['default']['cache_on'] = FALSE;
$db['default']['cachedir'] = '';
$db['default']['char_set'] = 'utf8';
$db['default']['dbcollat'] = 'utf8_general_ci';
$db['default']['swap_pre'] = '';
$db['default']['autoinit'] = TRUE;
$db['default']['stricton'] = FALSE;


/* End of file database.php */
/* Location: ./application/config/database.php */
```

<br/>

- hostname : 데이터베이스 서버의 주소 (loahost 의 경우 PHP 가 돌아가고 있는 머신을 의미)
- username : 데이터베이스 username
- password : 데이터베이스 비밀번호
- database : 데이터베이스 명
- dbdriver : mysql 등과 같은 드라이버를 지정하는 변수

<br/>



### 데이터베이스 라이브러리 로딩

데이터베이스 라이브러리를 로딩하는 방법은 두가지 입니다.

- [application/config/autoload.php](https://github.com/egoing/codeigniter_codeingeverbody/blob/View/application/config/autoload.php) 파일 내의 `$autoload['libraries']` 배열에 `database` 를 추가합니다.
- controller 에서 `$this->load->database()` 를 호출합니다.

<br/>



### 쿼리 작성

```php
$this->db->query("SELECT * FROM topic")
```

결과값을 저장하려 할 때는 아래와 같은 형식으로 사용합니다.

```php
$this->db->query("SELECT * FROM topic")->result();
```

<br/>



#### result(), row(), result\_array()

- result() : 쿼리를 어떻게 불러올지를 결정해줄수 있는 함수. 아래와 같이 row(), result\_arry() 함수를 호출 가능
  - row() : 쿼리의 단건 결과
  - result\_array() : 여러 행의 결과를 가진 쿼리 수행 결과

<br/>



#### Active Record

Active Record 는 조금 더 프로그래밍 적으로 데이터베이스를 제어하는 방식입니다. <br/>

e.g. topic 테이블에서 id 값이 3 인행만 조회

```php
$this->db->get_where('topic', array('id'=>$topic_id))->row();
```

Active Record 를 사용하면 표준 SQL 을 이용할 수 있으면서 프로그래밍 적으로 쿼리를 생성할 수 잇게 되기에 SQL 문자열을 하드코딩 하는 것에 비해 유지보수성이 높습니다.<br/>



### 모델 클래스 사용방법

model 에서는 데이터를 가져오는 로직을 메서드로 정의합니다. 그리고 model 에서 정의한 메서드는 controller 를 통해서 호출합니다. <br/>



모델 로딩

- 형식 :  `$this->load->model('모델클래스명');`
- e.g.  `$this -> load -> model('topic_model');`

<br/>



모델 호출

정의한 모델은 아래와 같은 방식으로 호출 가능합니다.

- 형식 : `모델 클래스명 -> 메소드명`
- e.g. `$topics = $this -> topic_model -> gets();`

<br/>



### 예제

#### application/config/database.php

> 참고 : 일부 웹 호스팅 환경에서는 [pconnect](http://php.net/manual/en/function.mysql-pconnect.php) 를 지원하지 않는 경우가 있습니다. 

```php
<?php  if ( ! defined('BASEPATH')) exit('No direct script access allowed');
$active_group = 'default';
$active_record = TRUE;
$db['default']['hostname'] = 'localhost';
$db['default']['username'] = 'egoing';
$db['default']['password'] = '111111';
$db['default']['database'] = 'opentutorials';
$db['default']['dbdriver'] = 'mysql';
$db['default']['dbprefix'] = '';
$db['default']['pconnect'] = TRUE;
$db['default']['db_debug'] = TRUE;
$db['default']['cache_on'] = FALSE;
$db['default']['cachedir'] = '';
$db['default']['char_set'] = 'utf8';
$db['default']['dbcollat'] = 'utf8_general_ci';
$db['default']['swap_pre'] = '';
$db['default']['autoinit'] = TRUE;
$db['default']['stricton'] = FALSE;
```

<br/>



#### application/controllers/topic.php

```php
<?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
class Topic extends CI_Controller {
    function __construct()
    {       
        parent::__construct();
        $this->load->database(); ## (1)
        $this->load->model('topic_model');
    }
    function index(){        
        $this->load->view('head'); 
        $topics = $this->topic_model->gets(); ## (2)
        $this->load->view('topic_list', array('topics'=>$topics));
        $this->load->view('main');
        $this->load->view('footer');
    }
    function get($id){        
        $this->load->view('head');
        $topics = $this->topic_model->gets(); ## (2)
        $this->load->view('topic_list', array('topics'=>$topics));
        $topic = $this->topic_model->get($id); ## (3)
        $this->load->view('get', array('topic'=>$topic));
        $this->load->view('footer');
    }
}
?>
```

<br/>



(1)

- database() 모듈을 로딩합니다.

(2), (3)

- 로드해온 모듈을 사용하는 구문입니다.



<br/>



#### application/models/topic\_model.php

```php
<?php
class Topic_model extends CI_Model {
 
    function __construct()
    {       
        parent::__construct();
    }
 
    function gets(){
        return $this->db->query("SELECT * FROM topic")->result();
    }
 
    function get($topic_id){
        return $this->db->get_where('topic', array('id'=>$topic_id))->row();
    }
}
```





## CodeIgnite 에서의 MVC 패턴

![](https://s3.ap-northeast-2.amazonaws.com/opentutorials-user-file/module/327/1262.png)

MVC란 **M**odel **V**iew **C**ontroller의 약자로 에플리케이션을 세가지의 역할로 구분한 개발 방법론입니다.<br/>

- Controller : Controller 측으로 사용자의 데이터 접근 요청이 발생합니다.
- Model : Controller 는 데이터 저장소에 접근해야 한다면 Model 을 통해 접근해서 데이터 처리를 합니다.
- View : 접근을 통해 가져온 데이터를 통해 View 를 제어해서 시각적인 표현을 제어합니다.

<br/>



아래 그림은 CI(CodeIgnite) 에서 이야기하는 Controller, Model, View 간의 관계입니다.

![](https://lh5.googleusercontent.com/-xAfIgOap9HI/UUcWtBm459I/AAAAAAAALvE/i6mJiOjIarg/s900/capture.gif)



