---
title: "터미널에서 경로이동 쉽게 하기"
image: 
  path: /images/termanal-app-00.jpg
  thumbnail: /images/termanal-app-011.jpg
  caption: "Photo from [COSMO'S](https://www.instagram.com/deftone2000)"
last_modified_at: 
---

맥 서비스와 쉘 스크립트 함수를 이용하면 터미널을 효과적으로 사용할 수 있습니다. 

### 맥 서비스로 열기

시스템 환경설정 > 키보드 > 단축키 탭 > 서비스를 선택하고 “폴더에서 새로운 터미널 열기”를 활성화합니다. 이곳에서 단축키 지정했지만 참조한 글처럼 작동하지 않았습니다. 앱 단축키를 선택하고 <kbd>+</kbd>를 누른다. 응용 프로그램에 Finder.app을 선택하고, 메뉴 제목에 다음 항목을 넣습니다. 보는 바와 같이 서브로 열리는 메뉴는 ->로 표시합니다.

`Finder->서비스->폴더에서 새로운 터미널 열기` 

![terapp]({{ '/images/termanal-app-01.jpg' | absolute_url }}){: .align-center} 

자신이 원하는 <kbd>키보드 단축키</kbd>를 지정합니다. 앱 단축키 설정은 잘 작동했습니다.

### 쉘 스크립트 함수 추가

쉘 스크립트
: 셸이나 명령 줄 인터프리터에서 돌아가도록 작성되었거나 한 운영 체제를 위해 쓰인 스크립트이다. 

.bash_profile[^1] 존재의 확인을 위해 터미널을 열고 홈경로에서 `ls -a`  입력하고 파일들을 확인합니다. 만약 없다면, `touch .bash_profile` 명령어를 입력하여 파일을 생성합니다. 다음으로 `open -e .bash_profile` 명령어를 입력하여 생성한 .bash_profile 파일을 텍스트 편집기로 엽니다. 이제 최종 목적인 자신의 .bash_profile에 다음 함수를 추가합니다. 

```shell
# cd into whatever is the forefront Finder window.
cdf() {  # short for cdfinder
  cd "`osascript -e 'tell app "Finder" to POSIX path of (insertion location as alias)'`"
}
```
위 내용을 추가하고 저장한 후 쉘을 다시 실행하면 cdf 명령을 사용할 수 있게 됩니다. 사용법은 터미널에서 `cdf` 을 입력하면 파인더에서 현재 선택된 폴러의 경로로 즉시 이동합니다. 함수명은 취향에따라 변경이 가능합니다. <strike>이걸 한다고?</strike>

Source  
[맥 파인더에서 터미널 여는 방법들](https://nolboo.kim/blog/2016/10/25/finder-terminal/)  
[bash_profile](http://ohgyun.com/378)  
[Mac OS에서 안드로이드 개발환경 설정하기](http://androidhuman.com/409)


[^1]: 환경 설정 파일, 시스템에 로그인할 때마다 실행된다.(login shell 에서 실행) .bash_profile 을 찾지 못하면, .bash_login 을 찾고, 없다면 .profile 을 찾는다.



