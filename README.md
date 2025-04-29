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