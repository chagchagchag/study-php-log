## php 기본 문법 정리 (1)

참고자료

- https://subin-0320.tistory.com/129



주석

```php
// 주석
/* 여러줄 주석 */
# 주석
```

<br/>



숫자

```php
<?php
echo 1;
?>
```

<br/>



echo

```php
<?php
echo 2+2; // 덧셈
echo 2-2; // 뺄셈
echo 2*2; // 곱셈
echo 2/2; // 나눗셈
?>
```

<br/>



var\_dump

```php
<?php
var_dump(6); # int 6
var_dump(6.5); # float 6.5
?>
```

<br/>



문자

- 쌍따옴표 (`""`), 작은 따옴표 (`''`)

```php
<?php
    echo "hello world"
?>
```

<br/>



문자와 문자를 결합할 때 (특이해요!!)

- `.` 을 사용해서 결합

```php
<?php
    echo "hello"." "."world"
?>
```

<br/>



문자 안에서 따옴표 기호를 사용

- `\` 으로 쿼팅을 합니다

```php
<?php
    echo '안녕하신가요. 오늘 읽을 책은 "우렁찬 함성"이에요';
	echo "안녕하신가요. 오늘 읽을 책은 \"우렁찬 함성\"이에요";
?>
```

<br/>



변수 

- `$변수명` 으로 선언합니다.

```php
<?php 
    $a = 10
    echo $a
?>
```

<br/>



중괄호 문법 (`{}`)

변수는 어떤 타입이든 대입 가능하며 변수값을 문자열 등에서 사용하기 위해서는 `{변수}` 를 사용합니다. 

```php 
<?php
    $a = 10
    echo "변수 \$a에 저장된 값은 $a 입니다. </br>";
	echo "변수 \$a에 저장된 값은 $a입니다. </br>";
	echo "변수 \$a에 저장된 값은 {$a}입니다.";
?>
```

<br/>



변수명 규칙

- 변수의 이름은 영문 대문자, 소문자, 언더스코어(\_) 로만 구성됩니다.
- 변수의 이름은 숫자와 구분을 빠르게 하기 위해 숫자로는 시작할 수 없습니다.
- 변수의 이름에는 공백이 포함되지 않습니다.
- 변수의 이름으로 php 에서 미리 정의한 $this 는 사용불가합니다.
- 변수의 이름은 대소문자를 구분합니다.

<br/>



php 의 자료형

- boolean : true/false
- integer (정수) : 부호를 가지는 소수점 없는 수. 표현 범위는 OS 에 따라 달라지며 64비트 운영체제는 -2^63 \~ (2^63 -1)
- float (실수) : 소수, 지수를 가지는 수. 정수보다 더 넓은 범위의 표현범위를 가지며 OS 에 따라 표현범위가 달라짐. 미리 정의된 상수인 INF 는 무한이라는 의미이며 실수의 최대범위라고 함
- string (문자열) : 연속된 문자 (character) 들의 집합. 큰따옴표 또는 작은 따옴표로 감싸서 표현
- array (배열) : 한쌍의 키, 값으로 이뤄지는 순서가 있는 집합
- object (객체) : 클래스의 인스턴스를 저장하기 위한 타입. 프로퍼티(properties)와 메서드(methods) 를 포함할 수 있음
- resource (리소스) : php 외부 자원. 데이터베이스 함수 등에서 데이터베이스 연결등을 반환할 때 사용
- NULL : NULL데이터

<br/>



변수의 기본 초기값

> 초기화하지 않을 경우 기본할당되는 값

- boolean : false
- integer : 0
- float : 0.0
- string : 빈 문자열
- array : 빈 배열

<br/>



변수 데이터 타입 체크, 데이터 타입 변경

- php 에서 변수에 담긴 데이터 타입을 검사할 때는 gettype 과 settype 을 사용

```php
<?php
    $a = 10;
	echo gettype($a); // integer

	settype($a, 'double');
	echo('<br/>');
	echo gettype($a); // double
?>
```

<br/>



가변변수

다른 변수안에 있는 값을 변수명으로 해서 동적으로 할당하는 방식

예제를 봐야 이해가 감

```php
<?php
    $a = 'hello';
	$$a = 'world';
	echo $a; // hello
	echo '<br/>';
	echo $hello; // world
?>
```



상수

- define() 함수를 사용
- 마법 상수(magic constants) 를 사용

<br/>



define() 을 사용하는 방식

```php
<?php
    define("TITLE", "PHP Tutorial");
	echo TITLE; # PHP Tutorial

	define("TITLE", "JAVA Tutorial"); ### (1)
	echo TITLE; # PHP Tutorial
?>
```

- (1) 에서 에러가 발생한다.

<br/>



마법 상수 (magic constants)

마법 상수는 대소문자를 구분하지 않는다.

- `__LINE__` : 파일의 줄 번호를 반환
- `__FILE__` : 파일의 전체 경로, 이름을 반환함. include 내부에서 사용할 경우 include 된 파일명을 반환
- `__DIR__` : 파일의 디렉터리를 반환합니다. 포함된 파일 내에서 사용할 경우 포함된 파일의 디렉터리를 반환합니다. `dirname(__FILE__)` 과 같은 결과를 반환합니다.
- `__FUNCTION__` : 함수의 이름을 반환
- `__CLASS__` : 클래스의 이름을 반환합니다. 클래스 이름은 대소문자를 구분합니다.
- `__TRAIT__` : 트레이트(TRAIT) 의 이름을 반환합니다. 트레이트의 이름은 트레이트를 선언한 네임스페이스를 포함합니다. 트레이트는 여러개의 클래스를 상속받을 수 있는 형태입니다. 
- `__METHOD__` : 클래스의 메서드 명을 반환합니다.
- `__NAMESPACE__` : 현재 네임스페이스의 이름을 반환합니다.



