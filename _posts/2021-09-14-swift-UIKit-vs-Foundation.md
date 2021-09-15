---
title:  "[Swift] UIKit과 Foundation"
excerpt: "import UIKit과 import Foundation에는 어떤차이가 있을까?!"

categories:
  - Swift
tags:
  - [swift]

toc: true
toc_sticky: true
 
date: 2021-09-14
last_modified_at: 2021-09-14
---

안녕하세요, 제가 xcode에서 swift로 알고리즘 문제풀이를 하려고 하는데, 
입력을 받는 readline() 함수는 프로젝트 생성시 macOS - command line tool로 선택해야 가능하더군요! 

그런데 comman line tool로 프로젝트를 생성했을때는 파일의 가장 상단에 import UIKit가 아닌 import Foundation을 볼 수 있었습니다.

그래서 간단하게 UIKit와 Foundation의 차이가 무엇인지 살펴보려고 합니다!

<br />

## Foundation
공식 문서를 살펴보면 Foundation은 정말 이름처럼 프로그램의 기반이 되는 데이터 타입, 콜렉션, 클래스를 포함하고 있고, 네트워크와 관련된 모듈까지 포함되어 있다고 하네요!  

<img src="../assets/images/foundation.png" width="60%" height="60%">

<br />
<br />


Foundation 선언파일의 상단부분을 캡처해서 가져왔는데요, 보시면 설명대로 Array, Data, Date, Error, HTTPCookie 이런 키워드들이 보이네요! 

<img src="../assets/images/foundation_import.png" width="50%" height="50%">


<br />
<br />

## UIKit 
공식 문서를 살펴보면 UIKit도 이름대로 유저 인터페이스와 관련된 사항들을 포함하고 있었습니다. 인터페이스를 위한 윈도우나 뷰, 또는 사용자의 터치나 클릭같은 이벤트 처리와 관련된 모듈이 여기에 포함되어 있는 거군요!  

<img src="../assets/images/uikit.png" width="60%" height="60%">

<br />
<br />

UIKit는 Foundation에 대한 reference를 가지고 있다고 하길래 열어봤더니 정말 가장 상단에 `import Foundation`을 볼 수 있었습니다! UIKit를 import하고 있다면 Foundation은 import할 필요가 없고 말고요 ~
<img src="../assets/images/uikit_import.png" width="60%" height="60%">


<br />

이제는 왜 Command Line Tool을 통해 생성된 파일에서는 import UIKit가 아닌 import Foundation을 하는지를 알것 같아요! 오늘 포스팅은 여기서 마치겠습니다. :smile:

<br />
<br />


*아직 배우는 단계라 모르는 부분이 많습니다 ㅎㅎ 잘못된 정보가 있거나 같이 토의하고 싶은 부분이 있다면 댓글이나 이메일 편하게 주세요* :blush:



