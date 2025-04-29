## 1-1


변수 a을 선언하였다. 데이터는 undefined이고 변수 영역에 저장된다.


## 1-2


변수 a 선언
변수 a가 변수 영역에 저장된다.

`var a; `

abc가 데이터 영역에 저장된다. 
변수영역의 a가 abc주소를 가리킨다.

`a='abc;`

변수 선언과 할당을 동시에 표현

`var a='abc';`


## 1-3

불변성을 설명하는 예제이다.

변수 a선언후 abc를 가리키게 한다.

`var a='abc';`

a가 abc가 아닌 새로운 문자열 abcdef를 가리키게 하고 문자열 abc는 아직 메모리에 남아있다.(primitive type의불변성)

`a=a+'def';`


변수 b는 5를 가리키고 변수 c도 5를 가리킵니다. 메모리에는 한개의 5만있고 b와 c가 동시에 가리킵니다.
이후 b가 7을 가리킵니다.
```
var b=5;
var c=5;
b=7;
```

## 1-4

객체 obj를 변수영역에 저장한다.

객체의 property또한 변수 영역에 저장되어있고 데이터 영역에 있는 1과 abc를 각각 가리키고있다.

이때 obj는 property를 직접 가리키지 않는다.

데이터 영역에서 property의 주소를 가지게 하는 영역을(reference type date) 만들고 객체는 그 데이터 영역을 가리킨다.

즉 객체 identifier->reference type data->perperty identifier->perperty의 data값으로 연결된다.

```
var obj ={
    a: 1,
    b: 'bbb'
};
```


## 1-5

객체 obj의 property a가 가리키는 data를 2로 바꾼다.

1은 불변성을 가지므로 1은 메모리에 남아있고 2를 데이터 영역에 새로 만들고 a가 그것을 가리키게 한다.

새로운 객체가 아닌 객체의 내부값만 바뀌었다=obj가 보는 주소는 그대로 유지된다가 요점이다.

```
var obj ={
    a: 1,
    b: 'bbb'
};
obj.a=2;
```


## 1-6

예제 1-4와 같이 객체 obj가 별도의 data를 가리키고 그 data는 property의 주소를 가리킨다.

먼저 property x는 3을 가리킨다.

arr는 또다른 참조형 data이므로 arr은 또다른 data를 가리키고 그 data는 배열의 identifier들의 주소를 가리킨다.

배열의 identifier는 각각 3,4,5를 가리키는데 3은 이미 메모리에 있으므로 새로 만들지 않고 기존의 3을 가리키게된다.


```
var obj={
    x:3,
    arr:[3,4,5]
};
```


## 1-7

변수 a는 10을 가리킨다.

변수 b는 a가 가지고 있는는 주소 즉 10의 주소를 받으므로 같은 10을 가리키게된다.

```
var a=10;
var b=a;
```

객체 obj1은 별도의 data를 가리키고 그 data는 객체의 property인 c, d의 주소를 가리키고 있다.

객체 a, d는 각각 10, ddd를 가리킨다. 

이때 10은 이미 메모리에 있으므로 새로 만들지 않고 기존에 있던 10을 가리킨다.

`var obj1={c:10,d:'ddd'};`


ob1이 가리키고 있는 주소를 obj2에게 복사했으므로 obj2도 객체의 property를 가리키고 있는 data를 가리킨다. 

즉 obj1과 obj2는 같은것을 가리킨다.
`var obj2=obj1;`



## 1-8

기본형 데이터와 참조형 데이터가 복사 이후 가리키는 값이 어떻게 되는지 알아보는 예제이다.

이전 예제와 같은 코드
```
var a=10;
var b=a;
var obj1={c:10,d:'ddd'};
var obj2=obj1;
```

기본형 data인 b는 가리키는 대상이 15로 바뀐다.

참조형 data인 obj2는 여전히 property의 주소를 가지고 있는 data를 가리키고 있고 property c가 가리키는 값만 20의 주소로 바뀌었다.
```
b=15;
obj2.c=20;
```
