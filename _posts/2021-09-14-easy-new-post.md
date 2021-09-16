---
title: "[Shell Script] 스크립트로 GitHub 포스팅 마크다운 파일 간단하게 생성하기!"
excerpt: "은근 귀찮은 파일 날짜 적기, 파일 형식... 귀차니즘 타파하는 간단 스크립트 파일을 만들어요!"

categories:
  - Shell Script
tags:
  - [Shell Script, GitHub blog]

toc: true
toc_sticky: true
 
date: 2021-09-14
last_modified_at: 2021-09-14
---
정말 별거 아니지만, 저는 깃허브 블로그 글 쓸때, 마크다운 파일 만들고 날짜 적고 양식 복붙하고 내용에 또 날짜적고 이 과정이 좀..ㄱ.. 귀찮더라구요 ㅠㅠ ...ㅋㅋㅋ 그래서 간단한 스크립트 파일 만들어봤는데 편하더라구요..!! 너무 간단해서 포스팅도 민망하지만 그래도 도움이 되실분이 있을까~해서 공유해봅니다..! :smile: 

<br />
<br />

## Usage

생성될 마크다운 파일 이름을 인자로 주어 스크립트를 실행시키면, 


<img src="https://user-images.githubusercontent.com/90241991/133559693-62c7483d-67fb-4831-b1c4-be7131135756.png" width="100%" height="100%">

파일 제목이나 기본 내용 양식과 현재날짜에 맞게 알아서 생성된답니다ㅎ

<img src="https://user-images.githubusercontent.com/90241991/133559818-5edd5045-975f-4e87-b4dd-71b650d31484.png" width="60%" height="60%">

## Get Started

우선 아래 내용을 복붙해서 스크립트 파일을 만들어주세요. 저는 new_post.sh 라고 저장했네요 ㅎ
<br />

``` script
#!/bin/bash

# today's date
TODAY=$(date +"%Y-%m-%d")

# directory to save new markdown file
DIR="/Users/hnnhp/Desktop/github/hnnhpark.github.io/_posts"
FILE="$TODAY-$1.md"

cat > $DIR/$FILE <<- EOF
---
title: "[Category] Title"
excerpt: "let's learn swift!"

categories:
  - Swift
tags:
  - [swift]

toc: true
toc_sticky: true

date: $TODAY
last_modified_at: $TODAY
---
EOF

echo "DONE! New markdown file was created in $DIR/$FILE"
```                                                               
<br />

여기서 수정해야 할 부분들이 있는데요!
우선 포스팅 글을 저장할 폴더에 맞게 `DIR`를 수정해주세요.

`FILE`은 저같은 경우는 2021-01-01-제목.md 를 파일 형식으로 지정해주었는데 사용하시는 방식으로 수정해주시면 됩니다! 

``` script 
# directory to save new markdown file
DIR="/Users/hnnhp/Desktop/github/hnnhpark.github.io/_posts/"
FILE="$TODAY-$1.md"
```

<br />

다음은 생성될 파일에 들어갈 내용을 적으면 됩니다. 이부분도 각자 블로그 포스팅 테마에 맞게 지정하시면 될것 같아요! (참고로 저는 minimal mistakes 테마를 쓰는데 처음 써보는 깃허브 블로그여서 비교 대상은 없지만 맘에 들어서 잘 정착할것 같아요 ㅎㅎ)
``` script
cat > $DIR/$FILE <<- EOF
---
title: "[Category] Title"
excerpt: "let's learn swift!"

categories:
  - Swift
tags:
  - [swift]

toc: true
toc_sticky: true

date: $TODAY
last_modified_at: $TODAY
---
EOF
```

이렇게 하면 끝입니다! 간단하죠 ? ㅎ 모두들 즐거운 포스팅 되세요 :blush: 

<br /> 

*혹시 다른 편한 방법이나 깃허브 블로그 포스팅 꿀팁있다면 언제든 환영입니다 ㅎㅎ*

