---
title: "[Swift] 프로그래머스 신규아이디 추천"
excerpt: "Swift 문자열 다루기 관련 문제"

categories:
  - Algorithm
tags:
  - [Swift, Algorithm]

toc: true
toc_sticky: true
 
date: 2021-09-16
last_modified_at: 2021-09-16
---

프로그래머스 [신규아이디 추천 문제](https://programmers.co.kr/learn/courses/30/lessons/72410?language=swift)는 문제에 명시된대로 따라하면 된다. 이때 여러 함수를 잘 숙지하고 있다면 보다 빠르고 쉽게 문제를 풀 수 있다. 

<br />
<br />

## Code

``` swift
import Foundation

func solution(_ new_id:String) -> String {
    var newID: String = new_id

    // 1단계
    newID = newID.lowercased()

    // 2단계
    newID = newID.filter{ $0.isLetter || $0.isNumber || $0 == "-" || $0 == "_" || $0 == "." }

    // 3단계
    while newID.contains("..") {
        newID = newID.replacingOccurrences(of: "..", with: ".")
    }

    // 4단계
    while newID.hasPrefix(".") {
        newID.removeFirst()
    }

    while newID.hasSuffix(".") {
        newID.removeLast()
    }

    // 5단계
    if newID == "" {
        newID = "a"
    }

    // 6단계
    if newID.count > 15 {
        newID = String(newID.prefix(15))
        while newID.last == "." {
            newID.removeLast()
        }
    }

    // 7단계
    if newID.count <= 2 {
        while newID.count != 3 {
            newID = newID + String(newID.last!)
        }
    }

    return newID
}
```
<br />
<br />

## Note
- 함수의 파라미터는 기본적으로 상수(`let`)이기 때문에, 값을 수정하고 싶다면 아래와 같이 `var` 변수를 만들어 값을 할당해준다.
```swift 
func solution(_ new_id:String) -> String {
    var newID: String = new_id
    ...
}
```
- `str.lowercased()` 함수는 `str`에서 모든 대문자를 소문자로 바꾼 문자열을 반환한다. `isLetter`을 이용하여 숫자인지, 기호인지 문자인지 뭔지를 확인하지 않아도 된다. 알아서 대문자만 쏙쏙 골라서 소문자로 바꿔준다. 

- `str.replacingOccurrences(of: "..", with: ".")`는 `str`에서 모든 `".."`을 `"."`으로 바꿔주는 함수이다. 이 문제에서 `while`문을 써야 하는 이유는 `str`이 가령 `"a....b"`라고 한다면 `str.replacingOccurrences(of: "..", with: ".")`의 결과값은 `ab`가 아니라 `a..b`이다. 따라서 모든 `..`가 대체되도록 하기 위해선`while`문을 이용해야 한다. 
``` swift 
while newID.contains("..") {
        newID = newID.replacingOccurrences(of: "..", with: ".")
    }
```

- `suffix`, `prefix` 접두사 접미사 관련 함수
```swift  
var word = "green apple"
word.prefix(1) // "g"
word.suffix(1) // "e"
word.prefix(3) // "gre"
word.suffix(5) // "apple"

word.hasPrefix("Grr") // false
word.hasSuffix("le") // true

word.removeFirst(2)
word // "een apple"
```