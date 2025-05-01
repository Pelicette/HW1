## 1-1


변수 a을 선언하였다. 데이터는 undefined이고 변수 영역에 저장된다.


## 1-2

`var a; `

변수 a 선언
변수 a가 변수 영역에 저장된다.

`a='abc;`

abc가 데이터 영역에 저장된다. 
변수영역의 a가 abc주소를 가리킨다.

`var a='abc';`

변수 선언과 할당을 동시에 표현



## 1-3

불변성을 설명하는 예제이다.

`var a='abc';`

변수 a선언후 abc를 가리키게 한다.

`a=a+'def';`

a가 abc가 아닌 새로운 문자열 abcdef를 가리키게 하고 문자열 abc는 아직 메모리에 남아있다.(primitive type의불변성)

```
var b=5;
var c=5;
b=7;
```

변수 b는 5를 가리키고 변수 c도 5를 가리킵니다. 메모리에는 한개의 5만있고 b와 c가 동시에 가리킵니다.
이후 b가 7을 가리킵니다.


## 1-4

```
var obj ={
    a: 1,
    b: 'bbb'
};
```

객체 obj를 변수영역에 저장한다.

객체의 property또한 변수 영역에 저장되어있고 데이터 영역에 있는 1과 abc를 각각 가리키고있다.

이때 obj는 property를 직접 가리키지 않는다.

데이터 영역에서 property의 주소를 가지게 하는 영역을(reference type date) 만들고 객체는 그 데이터 영역을 가리킨다.

즉 객체 identifier->reference type data->perperty identifier->perperty의 data값으로 연결된다.



## 1-5

```
var obj ={
    a: 1,
    b: 'bbb'
};
obj.a=2;
```

객체 obj의 property a가 가리키는 data를 2로 바꾼다.

1은 불변성을 가지므로 1은 메모리에 남아있고 2를 데이터 영역에 새로 만들고 a가 그것을 가리키게 한다.

새로운 객체가 아닌 객체의 내부값만 바뀌었다=obj가 보는 주소는 그대로 유지된다가 요점이다.




## 1-6

```
var obj={
    x:3,
    arr:[3,4,5]
};
```

예제 1-4와 같이 객체 obj가 별도의 data를 가리키고 그 data는 property의 주소를 가리킨다.

먼저 property x는 3을 가리킨다.

arr는 또다른 참조형 data이므로 arr은 또다른 data를 가리키고 그 data는 배열의 identifier들의 주소를 가리킨다.

배열의 identifier는 각각 3,4,5를 가리키는데 3은 이미 메모리에 있으므로 새로 만들지 않고 기존의 3을 가리키게된다.




## 1-7


```
var a=10;
var b=a;
```
변수 a는 10을 가리킨다.

변수 b는 a가 가지고 있는는 주소 즉 10의 주소를 받으므로 같은 10을 가리키게된다.

`var obj1={c:10,d:'ddd'};`

객체 obj1은 별도의 data를 가리키고 그 data는 객체의 property인 c, d의 주소를 가리키고 있다.

객체 a, d는 각각 10, ddd를 가리킨다. 

이때 10은 이미 메모리에 있으므로 새로 만들지 않고 기존에 있던 10을 가리킨다.

`var obj2=obj1;`

ob1이 가리키고 있는 주소를 obj2에게 복사했으므로 obj2도 객체의 property를 가리키고 있는 data를 가리킨다. 

즉 obj1과 obj2는 같은것을 가리킨다.



## 1-8

기본형 데이터와 참조형 데이터가 복사 이후 가리키는 값이 어떻게 되는지 알아보는 예제이다.

이전 예제와 같은 코드
```
var a=10;
var b=a;
var obj1={c:10,d:'ddd'};
var obj2=obj1;
```

```
b=15;
obj2.c=20;
```

기본형 data인 b는 가리키는 대상이 15로 바뀐다.

참조형 data인 obj2는 여전히 property의 주소를 가지고 있는 data를 가리키고 있고 property c가 가리키는 값만 20의 주소로 바뀌었다.



## 1-9

새로운 객체를 할당하여 값을 바꾸는 경우는 어떻게 바뀌는 가에 대한 예제이다.

```
var a=10;
var b=a;
var obj1={c:10,d:'ddd'};
var obj2=obj1;

b=15;
obj2={c:20,d:'ddd'};
```

이제는 obj2에 새로운 객체가 할당되었으므로 property c, d의 주소를 가지는 별도의 data를 가리킨다. 

이 data는 obj1이 가리키는 것과는 다른 값이다.

property c는 20을 가리키고 d는 ddd를 가리키는데 기존에 있었으므로 같은 ddd를 가리킨다.



## 1-10
불변성이 확보되지 않았을때 문제점을 보여주는 예제이다. 

원본 객체가 바뀌는 문제가 발생한다.

```
var user={
    name:'Jaenam',
    gender:'male'
};
```

user 객체 선언

```
var changeName=function(user,newName){
    var newUser=user;
    newUser.name=newName;
    return newUser;
};
```
user객체를 받아=user가 가리키는 주소를 받아 newUser가 같은 주소를 가리키게 한다.

그리고 name property가 가리키는 이름을 바꾸고 객체의 주소를 반환한다.


`var user2=changeName(user, 'Jung');`

user 객체를 받아서 name property 를 Jung으로 바꾼후 user2에 반환하였다. 

즉 user2와 user는 같은 곳을 바라보고 있고 원본 user 내부의 값은 바뀌어 버린 상태이다.

```
if (user!==user2){
    console.log('유저 정보가 변경되었습니다.');
}
console.log(user.name,user2.name);
console.log(user===user2);
```

출력으로 같은 이름이 나오고 true가 출력된다.


## 1-11 

객체의 불변성을 확보하기 위해서 어떻게 해야하는지에 대한 예제이다.

함수에서 새로운 객체를 return함으로서 해결하였다.


```
var user={
    name:'Jaenam',
    gender:'male'
};
```

```
var changeName=function(user,newName){
    return {
        name : newName,
        gender : user.gender
    };
};
```

user 객체를 받은후 새로운 객체를 반들어 반환하는 함수이다. 

이전 예제와는 달리 별도의 data를 가리키는 별도의 객체이므로 원본이 유지될수있다.

새로운 user 객체와 형태가 같은 객체를 생성한뒤 이름을 할당하고 gender는 받은 객체의 gender와 동일한 값을 가리키게 설정한다.


```
var user2=changeName(user, 'Jung');

if (user!==user2){
    console.log('유저 정보가 변경되었습니다.');
}
console.log(user.name,user2.name);
console.log(user===user2);
```

출력으로 유저 정보가 변경되었습니다., Jaenam Jung, false 가 출력된다.


## 1-12

shallow copy함수이다. 

바로 아래 단게의 값만 복사가 가능하다.

```
var copyObject=function(target){
    var result={};
    for (var prop in target){
        result[prop]=target[prop];
    }
    return result;
};
```

target 객체를 받은뒤

result라는 빈객체를 만든다.

이후 target객체의 모든 property를 찾아서 result에 같은 이름의 property를 만들고 같은 값을 가리키게 한다.

결과로 result 객체를 반환한다.

별도의 객체이므로 원본은 손상되지 않는다. 


## 1-13

1-12 shallow copy함수의 사용 예제이다.

```
var copyObject=function(target){
    var result={};
    for (var prop in target){
        result[prop]=target[prop];
    }
    return result;
};

var user ={
    name: 'Jaenam',gender: 'male'
};

var user2=copyObject(user);
user2.name='Jung';
```

이름이 Jaenam, 성별이 남자인 user 객체를 선언한다.

user 객체를 복사하여 새로운 객체를 user2로 넘긴다.

```
if(user!==user2){
    console.log('유저 정보가 변경되었습니다.');
}
console.log(user.name, user2.name);
console.log(user==user2);
```

새로운 객체이므로 유저 정보가 변경되었습니다. 가 출력되고 

Jaenam Jung, false가 출력된다.


## 1-14

shallow copy가 바로 아래 단계의 값만 복사함에 따라 생기는 문제를 보여주는 예제이다.

```
var copyObject=function(target){
    var result={};
    for (var prop in target){
        result[prop]=target[prop];
    }
    return result;
};

var user={
    name : 'Jaenam',
    urls:{
        portfolio: 'https://github.com/abc',
        blog : 'http://blog.com',
        facebook: 'http://facebook.com/abc'
    }
};
```

user 객체 선언

user 객체안에 참조형 data인 urls가 있다.

urls는 별도의 data를 가리키고있고 그 data는 urls의 property들을 가리키고 있다.

```
var user2=copyObject(user);

user2.name='Jung';
console.log(user.name===user.name);
```

user2를 선언하고 shallow copy로 user를 복사한다.

user2dml 이름을 바꾼다.

별도의 객체이고 property name은 서로 다른 변수 영역에 저장되어 있으므로 원본 user의 이름은 바뀌지 않는다.

따라서 false를 출력한다.

```
user.urls.portfolio='http://portfolio.com';
console.log(user.urls.portfolio===user2.urls.portfolio);
```

하지만 shallow copy를 할때 단순히 property가 기리키는 주소를 복사한 것이기 때문에 참조형 data인 urls가 복사될때 urls 의 property를 가리키는 

data가 복사된다. 즉 복사된 user2는 같은 urls 객체를 가리킨다.

따라서 user2의 urls.portfolio를 바꾸면 user의 urls.portfolio도 같이 바뀌어서 true를 출력한다.


```
user2.urls.bolg='';
console.log(user.urls.blog===user2.urls.blog);
```

이것도 위와 동일하게 true가 출력된다.



## 1-15

중첩된 객체에 대해서는 어떻게 복사를 해야하는가에 대한 예제이다.

참조형 안에 참조형이 있다면 그 안쪽의 참조형에 대해서 shallow copy를 수행하면 된다. 

```
var copyObject=function(target){
    var result={};
    for (var prop in target){
        result[prop]=target[prop];
    }
    return result;
};

var user={
    name : 'Jaenam',
    urls:{
        portfolio: 'https://github.com/abc',
        blog : 'http://blog.com',
        facebook: 'http://facebook.com/abc'
    }
};
```

```
var user2=copyObject(user);
user2.urls=copyObject(user.urls);
```

user2에 shallow copy를 수행한다. 이때 user2의 urls과 user의 urls은 같은 곳을 가리킨다.

user 객체 내부의 참조형인 urls에 대해서 shallow copy를 수행하여 user2.urls에 넘겨준다.

이제 user2.urls는 새로운 객체를 가리키므로 user.urls와는 다르다.

```
user.urls.portfolio='http://portfolio.com';
console.log(user.urls.portfolio===user2.urls.portfolio);

user2.urls.blog='';
console.log(user.urls.blog===user2.urls.blog);
```

urls의 property를 바꾸어도 별도의 객체이므로 다른 값을 가진다.

false 출력



## 1-16

Deepcopy 함수

```
var copyObjectDeep=function(target){
    var result={};
    if (typeof target=='object' && target!==null){
        for (var prop in target){
            result[prop]=copyObjectDeep(target[prop]);
        }
    }
    else {
        result=target;
    }
    return result;
}
```

앞에서 보았던 shallow copy를 재귀적으로 수행하여 가장 깊은 곳에서 위까지 객체로서 반환하여 모든 참조형 객체들을 별도의 객체를 만들어 할당한다.


## 1-17

앞에서의 Deep copy함수를 사용한 예제이다. 

```
var copyObjectDeep=function(target){
    var result={};
    if (typeof target=='object' && target!==null){
        for (var prop in target){
            result[prop]=copyObjectDeep(target[prop]);
        }
    }
    else {
        result=target;
    }
    return result;
}
```

```
var obj={
    a:1,
    b:{
        c:null,
        d:[1,2]
    }
};
var obj2=copyObjectDeep(obj);

obj2.a=3;
obj2.b.c=4;
obj.b.d[1]=3;
```

객체 obj선언후 Deep copy수행

재귀적으로 모든 참조형 객체들을 별도의 객체를 만들어 반환햐였으므로 원본이 바뀌지 않는다.


```
console.log(obj);
console.log(obj2);
```

따라서 출력은 
{a: 1. b: { C: null, d: [1 ,3] } }

{a: 3. b: { C: 4, d: {0:1, 1:2} } }



## 1-18

JSON을 이용한 Deep copy 방법이다.

```
var copyObjectViaJSON=function(target){
    return JSON.parse(JSON.stringify(target));
};
```

객체를 JSON 문자열로 바꾸었다가 다시 JSON 객체로 바꾸면 Deep copy가 가능하다.

하지만 순수 정보가 아닌 함수 같은 경우 JSON으로 바꾸지 못하여 무시하고 복사하지 않는다.


```
var obj={
    a:1,
    b:{
        c:null,
        d:[1,2],
        func1:function(){console.log(3);},
        func2:function(){console.log(4);}
    }
};
var obj2=copyObjectViaJSON(obj);

obj2.a=3;
obj2.b.c=4;
obj.b.d[1]=3;
```

obj를 선언하고 JSON Deep copy를 이용하여 obj2로 복사하였다.

obj2 의 property a는 3을 가리키고 property b.c 는 4를 가리킨다.

원본인 obj의 property b.[1]은 3을 가리킨다.

이때 함수 같은 경우 무시하고 복사하지 않았으므로 obj.b.func1과 obj.func2는 복사되지 않았다.

```
console.log(obj);
console.log(obj2);
```

따라서 결과는 

{a: 1. b: { c: null, d: [1, 3], func1: f() }, func2: f() }
{a: 3. b: { c: 4, d: [1, 2] } }



## 1-19

자바 스크립트에서 자동으로 undefined를 부여하는 경우에 대한 예제이다.

자바 스크립트에서 부여하는 undefined와 혼동하지 않기위해 사용자가 undefined를 사용하지 않아야 한다.

```
var a;
console.log(a);
```

data를 할당하지 않은 identifier에 접근시 undefined 출력

```
var obj={a:1};
console.log(obj.a);
```

정상적인 접근, 1출력

```
console.log(obj.b);
console.log(b);
```

존재하지 않는 property에 접근시 undefined 출력

존재하지 않는 변수 접근 error 문구 출력

Uncaught ReferenceError ReferenceError: b is not defined 

```
var func=function(){};
var c=func();
console.log(c);
```

return이 없는 함수를 실행하면 undefined를 반환한다. undefined 출력


## 1-20

빈 배열과 undefined가 있는 배열의 차이에 대한 예제이다.

```
var arr1=[];
arr1.length=3;
console.log(arr1);
```

빈 array선언후 길이를 3으로 설정한다. 이때 undefined가 아니라 빈 배열이 출력된다. [emptyX3]

실제로는 [...]으로만 출력되었다.

```
var arr2=new Array(3);
console.log(arr2);
```

Array 생성자로 길이가 3인 array을 만들어 arr2에 달당하였다.

마찬가지로 array가 비어있어 빈 배열이 출력된다. [emptyX3]

실제로는 [...]으로만 출력되었다.

```
var arr3=[undefined,undefined,undefined];
console.log(arr3);
```

앞에서의 경우와 달리 사용자가 직접 undefined로 할당하였다.

이 경우 빈것이 아닌 undefined가 있는것이다. 

출력으로 undefined, undefined, undefined가 나온다.


## 1-21

실제 비어있는 값과 undefined가 배열 관련 매서드들에서 어떻게 다른가를 확인하는 예제이다.

```
var arr1=[undefined, 1];
var arr2=[];
arr2[1]=1;

arr1.forEach(function (v,i){console.log(v,i);});
arr2.forEach(function (v,i){console.log(v,i);});
```

순회하면서 index와 value를 출력하는 동작이다.

arr1은 undefined가 자리를 차지하고 있으므로 무시되지않고 undefined 0 / 1 1 이출력된다.

arrr2는 비어있는 index 0가 무시되기 때문에 1 1만 출력된다.

```
arr1.map(function(v,i){return v+i;});
arr2.map(function(v,i){return v+i;});
```

value와 index를 더해서 새로운 배열을 반드는 동작이다.

arr1은 undefined와 더할수 없으므로 NaN, index 1 value 1을 더해서 2가된다. [NaN, 2]

arr2은 index 0는 무시되고 index 1은 1+1=2가 된다. [비어있음, 2]

```
arr1.filter(function(v){return !v;});
arr2.filter(function(v){return !v;});
```

순회하면서 value가 없는것을 남기는 동작이다.

arr1에는 value가 없는것이 undifined만 있으므로 undefined만 남는다.

arr2에는 index 0은 건너뛰고 1은 filter되어 아무것도 남지 않는다.


```
arr1.reduce(function(p,c,i){return p+c+i;}, '');
arr2.reduce(function(p,c,i){return p+c+i;}, '');
```

순회하면서 p+arry[i]+i를 string concate하는 동작이다.

arr1은 undefined가 무시되지않고 string concate된다. index 0에서 ''+undefined+0, index 1에서 undefined0+1+1

결과적으로 undefined011이된다.

arr2는 비어있는 index 0을 무시하여 index 1에서 ''+1+1수행, 결과적으로

11이된다.


## 1-22

null의 type이 object라는 사실과 변수의 값이 비어있는 것을 확인하려면 어떻게 해야하는지 보여주는 예제이다.

```
var n = null;
console.log(typeof n);

console.log(n==undefined);
console.log(n==null);
```

null의 type은 object이기 때문에 비어있더라도 typeof를 사용하면 object를 반환해 실제 object가 있는지

null이 있는지 구분할수 없다.

또한 ==로는 undefined와 null을 구분할수 없다.

n==undefined, n==null모두 true로 나온다.

```
console.log(n===undefined);
console.log(n===null);
```

정확히 비교하려면 ===를 써야한다.

n===undefined 는 false, n===null 는 true라고 출력된다.



## 2-1

call stack의 개념을 설명하는 예제이다.

```
var a=1;
function outer() {
  function inner() {
    console.log(a);
    var a=3;
  }
  inner(); 
  console.log(a); 
}
outer(); 
console.log(a); 
```

먼저 global 환경정보가 수집되어 golbal E.C가 call stack에 담긴다. 

이후 outer() 수행시 outer의 환경정보 수집후 outer E.C가 call stack에 담긴다. 

outer함수에서 inner()를 만나 inner의 환경정보를 수집해 inner E.C가 call stack에 담긴다. 

이후 역순으로 inner가 끝나면 inner E.C가 pop되고 다음은 outer, 마지막으로 global이 pop된다.(stack동작)

inner 실행시 undefined가 나오는데 hoisting이후 실행 단계시 a가 가리키는 값이 없기 때문이다.

outer안의 a출력시 1이 나오는 이유는 outer안에 a변수가 스코프 체인을 통해 전역에 있는 a를 찾아 출력했기 때문이다. 


## 2-2

호이스팅과 코드 수행시 어떻게 되는가 보여주는 예제이다.

자바 스크립트는 먼저 컨택스트 내부를 hoisting한 이후 코드가 수행된다.

```
function a(x) {
    console.log(x);
    var x; 
    console.log(x); 
    var x = 2; 
    console.log(x); 
  }
  a(1);
```

a의 E.C에서 hoisting시 x를 수집한다. x가 3번 나오지만 1번만 수집된다. 

수행 단계에서 x=1이므로 처음 console.log(x)에서 1출력, 두번째도 동일하게 아직 x=1이므로 1출력

x=2 수행으로 x는 2를 가리키고 있다. 마지막 console.log(x)에서 2를 출력한다.

위와 같은 단계로 hoisting과 실행이 별도로 나누어져 있기 때문에

 var x를 한다고 해서 x가 가리키는게 없어지는게 아니다. -> undefined를 출력하지 않는다.



 ## 2-3

2-2에서 함수에 argument로 1준것과 이것처럼 함수 내부에서 제일 먼저 할당하는 것과 다른점이 없다

라는 것을 보여주는 에제이다.

 ```
 function a() {
    var x = 1;
    console.log(x);
    var x;
    console.log(x);
    var x = 2;
    console.log(x);
  }
  a();
  ```

  내부환경 입장에서 완전히 같은 동작이다. hoisting시 x를 한번만 수집하고 실행단계시 가장먼저 x=1를 할당하여 진행한다.

  출력도 동일하게 1,1,2이다.



  ## 2-4

호이스팅에 대해 정확히 이해했다면 아래처럼 변수 선언을 위쪽으로 따로 모아주고 수행될 부분만 순서대로 써주면 

같은 동작을 할것이라고 예상할수 있다. hoisting이 먼저 선언된 변수들을 인식한것을 표현한것이다.

  ```
  function a() {
    var x;
    var x;
    var x;
  
    x = 1;
    console.log(x);
    console.log(x);
    x = 2;
    console.log(x);
  }
  a(1);
  ```

  hoisting시 x는 한번만 수집되고 수행시 x는 1을 가리킨후 console.log(x)를 2번 수행하여 1을 2번 출력한다.

  이후 x는 2를 가리킨후 console.log(x)를 수행하여 2를 출력한다.


## 2-5

아래의 예제를 기반으로 hoisting을 수행시 어떻게 자바 스크립트가 구동되는지 2-2,3,4처럼 코드를 변환해 볼것이다.

```
function a() {
    console.log(b);
    var b = 'bbb';
    console.log(b);
    function b() {}
    console.log(b);
  }
  a();
  ```

  hoisting시 b를 수집하는데 function b()는 hoisting단계에서 이미 함수를 가리키고 있다.

  따라서 수행시 첫번째console.log(b)에서 함수를 출력하고 var b = 'bbb' 이후부터 bbb를 출력한다.



## 2-6

2-5의 연속인 예제

  ```
  function a() {
    var b;
    function b() {} 
  
    console.log(b);
    b = 'bbb';
    console.log(b);
    console.log(b);
  }
  a();
  ```

  hoisting이 identifier를 먼저 수집하므로 선언 관련 line들을 위로 올리고 아래쪽에는 수행관련 line들을 둠으로써 

  실제 2-4의 수행과정을 사람이 이해하기 좋게 순서를 바꾸었다.

  hoisting시 b는 function을 가리키고 있으므로 첫번째는 함수출력 bbb가 할당된후 bbb출력


## 2-7

2-6에 연속인 예제

  ```
  function a() {
    var b;
    var b = function b() {};
  
    console.log(b);
    b = 'bbb';
    console.log(b);
    console.log(b);
  }
  a();
  ```

  마지막으로 function b() {}를 hoisting이 끝난이후 변수 b에 함수를 할당한 것처럼 보이기 위해 var b = function b() {}로 수정하였다.

  이렇게 2-5의 코드를 사람이 이해하기 좋게 실제 자바 스크립트의 동작과정을 모사해보았다. 

  변수 b hoisting으로 수집후 hoisting이 끝난 다음 수행과정에서 b에 함수를 할당,

  출력으로 함수를 내보낸후 b에 bbb를 할당 출력으로 bbb를 2번 내보낸다.


## 2-8.js

함수를 선언하는 방식에 따라 hoising 과정에서 어떤차이가 있는지 설명하는 예제이다.

```
function a() {/* ... */}
a();
```

변수 a가 함수 a를 가리키고 있는것과 같은 표현이다. 

hoisting시 a를 수집함과 동시에 변수 a에 함수 a를 할당한다.

```
var b = function() {/* ... */};
b();
```

변수 b에 함수를 할당한다는 뜻이다.

즉 hoising시 b를 수집하고 실행당계에서 함수가 할당된다.

```
var c = function d() {/* ... */};
c();
d();
```

변수 c에 함수 d가 할당된다는 뜻이다. 

c에 함수가 할당되었으므로 c()로 실행이 가능하지만 함수명인 d()로는 불가능하다. error 출력

하지만 함수 내부에서 함수명으로 실행은 가능하다.


## 2-9

아래의 예제를 기반으로 hoisting을 수행시 어떻게 자바 스크립트가 구동되는지 코드를 바꾸어 가면서 볼것이다.

```
console.log(sum(1, 2));
console.log(multiply(3, 4));

function sum(a, b) {
  return a + b;
}

var multiply = function(a, b) {
  return a * b;
};
```

결과부터 말하자면 hoisting시 sum, multiply가 수집되고 sum은 동시에 함수가 할당된다.

이후 수행과정시 console.log(sum(1, 2))에서 3이 출력되지만 

console.log(multiply(3, 4))에서 multiply에 함수가 아직 할당되지 않았으므로 error가 출력된다.



## 2-10

2-9의 예제에서 hoisting 이후를 코드의 순서를 바꾸어서 표현해 본것이다.

```
var sum = function sum(a, b){
    return a + b;
};
var multiply;
console.log(sum(1, 2));
console.log(multiply(3, 4));
  
multiply = function(a, b){
    return a * b;
};
```

hoisting 과정을 코드 위로 올리고 수행과정을 아래로 옮겼다. 

hoisting시 sum은 수집과 동시에 함수 할당, multiply 수집

수행과정에서 console.log(sum(1, 2))은 3출력 console.log(multiply(3, 4))은 함수가 할당되지 않아서 error출력

이후에야 multiply에 함수가 할당된다.


## 2-11

함수 선언문을 사용할시 발생하는 문제에 대한 예제이다. 

선언문은 hoisting시 수집과 동시에 할당하기 때문에 발생하는 문제이다.

함수 선언문이 아니라 함수 표현식으로 코딩해야한다.

```
console.log(sum(3, 4));

function sum(x, y) {
  return x + y;
}

var a = sum(1, 2);

function sum(x, y) {
  return x + ' + ' + y + ' = ' + (x + y);
}

var c = sum(1, 2);
console.log(c);
```

위 코드에서 hoisting을할때 sum이 2번있다. sum의 수집 자체는 중복이므로 1번이지만 함수을 할당할때는 첫번째 함수를 할당한 이후 두번째 함수가 

다시 할당 되어서 첫번째 함수가 덮어씌어진다. 때문에 모든 sum 함수는 마지막 sum 함수로 실행되게 되고 출력은 3+4=7, 1+2=3이 나오게 된다.

var sum=function() 처럼 hoisting시 할당되지않는 표현식으로 사용해야한다.


# 2-12

앞의 예제와 달리 함수 표현식으로 사용하면 오류를 줄일수 있다. 

앞 예제의 경우 첫 줄의 console.log(sum(3, 4))가 의도치 않은 출력을 하는 반면

표현식은 hoisting시 할당을 하지 않으므로 함수 표현식 이전에 함수를 불러오면 error를 출력하여 사용자가 오류가 발생한 것을 인식하도록 한다.

```
console.log(sum(3, 4));

var sum=function(x, y){
  return x + y;
};

var a=sum(1, 2);

var sum=function(x, y){
  return x + ' + ' + y + ' = ' + (x + y);
};

var c=sum(1, 2);
console.log(c);
```

hoisting 단계에서 sum, a, c가 수집되는데 sum은 중복이므로 한번만 수집되고 아무것도 할당되지 않는다.

이후 실행단계에서 console.log(sum(3, 4))수행시 sum에 할당된것이 없으므로 오류가 발생한다.

맨 위의 console.log가 없었다면 sum에 함수가 할당되고 변수 a에 3이 저장될것이다.

그다음 sum에 새로운 함수 가 할당되고 변수 c에 1+2=3이 할당되고 이것을 출력할것이다.

결과적으로 각 변수에 다른 함수가 사용되었다.