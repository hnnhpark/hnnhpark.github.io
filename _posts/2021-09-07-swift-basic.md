---
title:  "[Swift] Swift 기본문법 정리"
excerpt: "Swift의 기본 문법a-z를 정리해보자."

categories:
  - Swift
tags:
  - [swift]

toc: true
toc_sticky: true
comments: true
 
date: 2021-09-07
last_modified_at: 2021-09-07
---
안녕하세요, iOS에 갓입문한 hnnh라고 합니다:) 저는 프로그래밍 경험은 있지만 swift는 처음 배우게 되어 각 문법의 기초 개념보다는 swift만이 가지고 있는 특징이나 문법을 빠르게 정리해보고 오래 기억하려는 목적으로 글을 작성하게 되었습니다. 

이글은 아래 두 훌륭한 문서들을 참고하여 작성했습니다. 

[Swift 공식 문서](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html#)

[야곰님의 Swift 블로그](https://yagom.github.io/swift_basic/)

둘다 너무 좋은 자료이니 저같은 입문자분들 잘 활용하시길 바랄게요 ㅎㅎ!! 

<br />
<br />


## 변수와 상수 
변수는 var, 상수는 let을 사용한다. 
``` swift는 
var sumCount = 0
let PI = 3.14
```
---

타입 추론이 어려운 경우 `var inputA: String = "abc"` 형태로 타입을 명시해 주어야 한다.  
``` swift 
var input: String = "hello world"
```
---
변수나 상수를 선언한 이후 초기화를 하려고 할때, 반드시 타입을 명시해 주어야 한다. swift에서는 상수의 선언과 초기화가 꼭 동시에 이루어지지 않아도 된다. 
``` swift
let myName: String
myName = "hnnh" 

// let myName
// myName = "hnnh" // 에러
```
<br />

## 기본 데이터 타입
* swift의 기본 데이터 타입으로는 Bool, Int, UInt, Float, Double, Character, String이 있다.  
* Swift는 type에 대한 부분이 엄격한 type-safe language이다. Bool 타입의 변수에 0이나 1을 저장하면 swift에서는 에러가 발생한다. 또한, 같은 타입의 변수끼리만 사칙연산이 가능하다. 
``` swift
var isEmpty: Bool = true
// isEmpty = 0  // 에러

var a = 1
var b: Float = 2
// var c = a + b // 에러
var c = a + Int(b) // 타입캐스팅을 해주어야 가능하다.
```
---

### String
string의 각 character 접근하기 
``` swift
let word = "apple"
for ch in word {
  print(ch)
}
```
다른 타입 -> string으로 변환하기  
``` swift
let isEmpty = false
String(isEmpty) // "false"
isEmpty.description // "false"

print("isEmpty: \(isEmpty)")  "isEmpty: false"
```
string의 다양한 함수 (추가 보충 포스팅 예정)
``` swift
let phoneNum = "010-3030-1010"
phoneNum.split(seperator: "-") // ["010", "3030", "1010"]


```

<br />

## Any, AnyObject
Any는 swift의 모~든 타입을 저장할 수 있다. 
``` swift
var someAny: Any
someAny = "hello world"
someAny = 10
```
---
AnyObject는 어떤 클래스의 인스턴스든 저장할 수 있다.
```
class truck {}
var myCar: AnyObject = truck()
```
<br />

## Optional
Swift에서 null은 `nil`이다. 기본 타입들은 nil을 할당할 수 없다. 
``` swift
var myAge: Int = 0
// myAge = nil // 에러 
```
Optional은 타입뒤에 `?`를 붙여 나타내는데, 이는 "값이 있을 수도 있고 없을 수도(nil) 있음을 나타낸다"
``` swift
var myAge: Int?
myAge = nil 
```
---
Optional은 원래 타입의 값을 opional로 포장wrap한 상태이다.
``` swift
var optionalNum: Int? = 10
print(optionalNum)
// 출력: Optional(10)
```
Optional은 nil이 들어있을 수 있다는 가정하에 있어서인지, optional을 그대로 이용하기에 여러 제약이 있다. 
``` swift
var a: Int? = 10
var b: Int? = 20
// var c = a + b 에러: optional 타입에 대해서는 사칙연산이 불가하다 
```
따라서 optional타입에서 본래 값을 꺼내서 이것이 nil여부를 확인하여 적절한 연산을 수행해주어야 한다. 이를 위해서 다음의 방식들을 이용한다.
* Nil coalescing operator ?? 
* Forced unwrapping 
* Optional binding(if문을 이용 / guard문을 이용)

---
### nil Coalescing operator : ??
`a ?? b` : a에는 optional이 들어간다. optional에서 값을 추출하여, 값이 있다면 a의 값을 반환하고, 값이 없다면 즉, nil이라면 b를 반환하는 연산자이다.
``` swift
var a: Int? = 10
var b: Int? = 20
var c = (a ?? 0) + (b ?? 0)
// a가 nil이라면 0을 더하고, 마찬가지로 b도 nil이라면 0을 더한다.  
```
<br />

### Forced unwrapping
nil이 아니라는 상황을 가정하고 optional에서 값을 추출한다. nil이라면 critical한 상황이 발생할 수 있으므로, 정말 확신이 있을때만 써야 한다. 
``` swift
var a: Int? = 10
var b: Int? = nil
print(a!) // 10
// print(b!) 에러 
```
<br />

### if를 이용한 Optional binding
Optional의 nil여부에 따라서 적절한 처리를 수핼할 수 있다. 다음과 같은 형태를 가진다. 
``` swift
if let 임시변수명 = 옵셔널변수 {
    // nil이 아니라면 임시변수에 옵셔널 변수가 할당된다. 
} else {
    // nil일 경우. else 문은 생략 가능하다. 
}
```

``` swift
var a: Int? = 10
var b: Int? = nil

if let actualNum = a {
  print(actualNum)
} else {
  print("값이 없습니다.")
}
```
``` swift
if let numA = a, let numB = b {
  print(numA + numB)
} else {
  print("더하기를 수행할 수 없습니다")
}
```
### guard를 이용한 Optional binding
if문을 사용했을때와 유사하지만, 몇가지 차이점이 존재한다. 기본형태는 다음과 같다. if문이 '값이 있다면 ~한다'의 의미라면 guard let else문은 '값이 없다면 ~한다'의 의미를 가진다.
``` swift 
guard let 임시변수 = 옵셔널값 else {
  // nil이라면 
}
```
 
if문과 달리, guard문에서 할당된 임시변수는 {}밖에서도 유효한 변수이다. 
``` swift
var a: Int? = 30
if let numFromIf = a {
  print(numFromIf)
}
// print(numFromIf) // if문 밖이므로 numA는 유효하지 않음 

func printNum(){
  guard let numFromGuard = a else {
    print("값이 없습니다")
    return
  }
  print(numFromGuard) 
}
printNum() // 출력: 30 
```
주의할점은, guard let else 문에서는 return, break, continue, throw등의
scope를 벗어날 명령어가 필요하다. 따라서 함수나, 메서드, 반복문 등 __특정 블록 내부__ 에 위치할때에만 사용이 가능하다. 
``` swift
var a: Int? = 30

func printNum(){
  guard let numFromGuard = a else {
    print("값이 없습니다")
  }
  print(numFromGuard) 
}
printNum() // 에러: "'guard' body must not fall through." return같은 흐름을 전환하는 명령어가 없다면 이후 nil이 아닌 경우의 코드가 그대로 수행되는것을 경계하기 위해 이런 규칙을 갖는 것 같다. 
```
<br />

## Array
### 배열 선언 
``` swift
var integers = Array<Int>()
var integers = [Int]()
var integers = [1,2,3] // 타입 추론 가능

// []를 이용하여 배열을 선언할때에는 변수명 뒤에 타입 명시를 해주어야 한다. 
var integers: [Int] = []
var integers: Array<Int> = []
```

### 배열 다루기 
``` swift 
var integers = [1, 2, 3, 4, 5, 6]

// index로 접근
print(integers[2]) // 출력: 3

// 전체 요소 갯수
print(integers.count) // 출력: 6

// 추가
integers.append(7) // 7 추가
integers = integers + [10,11,12]
integers.insert(100, at: 3) // 4번째에 100 추가

// 삭제 
integers.remove(at: 0) // 첫번째 요소 삭제 
integers.removeLast()

// 포함여부 확인 
print(integers.contains(1)) // true

// enumerate
for (index, num) in integers.enumerated() {
  print(index, name)
}
```

<br />

## Set
중복없는 요소들의 집합
### 선언
``` swift
var ids = Set<String>()

// Array를 set으로 변환
var sameIds = ["aaa", "bbb", "ccc", "ccc"]
var ids = Set(sameIds)

// [요소1,..]을 이용한 초기화시, Set을 명시해주어야 Array와 구분가능하다.
var ids: Set = ["aaa", "bbb", "ccc"]
```

### set 다루기 
``` swift
// 추가 
ids.insert("ddd")

// 삭제 
ids.remove("ddd")
ids.removeFirst()

// 요소 갯수
ids.count 

```
### Set의 집합 연산
``` swift
var numbers1: Set = [1, 2, 3, 4, 5]
var numbers2: Set = [4, 5, 6, 7, 8]
// intersect
numbers1.intersection(numbers2)

// union
numbers1.union(numbers2)

// union - intersect
numbers1.symmetricDifference(numbers2)

// remain
numbers1.subtracting(numbers2) // [1, 2, 3]
```

<br />

## Dictionary
### 선언
``` swift
var nicknames = Dictionary<String, String>()
var nicknames = [String: String]()

var nicknames = ["sarah" : "princess", "jason" : "coolguy"]
var nicknames: [String: String] = [:]
```

### dictionary 다루기 
``` swift
// 추가 
nicknames["jack"] = "frog"

// 존재하지 않는키 접근시 에러 발생하지 않고 nil 출력한다
nicknames["sally"] // nil 

// 삭제
nicknames["jack"] = nil
nicknames.removeValue(forKey: "jack")

// 키들 출력
nicknames.keys

// for문을 이용한 전체 출력
for (name, nickName) in nicknames {
  print("\(name)'s nickName: \(nickName)")
}
```

## if 
특별한 사항 없이 if, else if, else를 조합하여 사용하면 된다. 
``` swift 
let age = 15
if age < 19 {
  print("청소년입니다")
} else {
  print("성인입니다")
}
```

## switch 
swift에서는 switch문에 break를 명시하지 않아도 기본적으로 각 case에 해당하는 코드를 실행 후 switch 문을 빠져나간다. 
``` swift 
var age = 5
switch age {
case 0..<8: // 0이상 8미만.
    print("미취학아동")
case 8..<14:
    print("초등학생")
case 15..<17:
    print("중학생")
case 17..<20:
    print("고등학생")
default:
    print("성인")
} // 출력: 미취학아동 
```
break를 무시하고 다른 case문도 실행하려면 fallthrough 키워드를 사용하면 된다.   
``` swift 
var age = 5
switch age {
case 0..<8:
    print("미취학아동")
    fallthrough
case 8..<14:
    print("초등학생")
case 15..<17:
    print("중학생")
case 17..<20:
    print("고등학생")
default:
    print("성인")
} // 출력: 미취학아동 \n 초등학생 
```
case문에 `,`를 이용하는 것도 가능하다. 
``` swift 
var aage = 16
switch aage {
case 0..<8:
    print("미취학아동")
case 8..<14, 15..<17, 17..<20:
    print("학생")
default:
    print("성인")
}
```

## for 
`for 요소 in 순회하고자 하는 대상` 의 간단한 문법이다. 
``` swift 
let nums = [1, 2, 3, 4, 5]
for num in nums {
  print(num)
}
```


## while
``` swift 
var i = 0
while i < 10 {
  print(i)
  i += 1
} 
// 0부터 9까지 출력 
```


## Function

## Closure
:> 작성중입니다