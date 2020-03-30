---
title: "LCP 미리알림 등록"
image: 
  path: /images/lcp-alarm-regist-00.jpg
  thumbnail: /images/lcp-alarm-regist-01.jpg
  caption: "Photo from [COSMO'S](https://www.instagram.com/deftone2000)"
last_modified_at: 
---

Launch Center Pro, TextExpander 의 콜라보(?)를 이용해서 Fantastical2 에 빠르게 미리알림을 등록하는 액션입니다.

### TE Snippet 추가 (Date / Time Math)

TE를 이용하면 타임로그처럼 오늘날짜를 자동으로 입력 할 수 있는데요. 일종의 매크로라고 이해하면 됩니다.  

예를들어 Today를 **%m.%d**  

라고 콘텐츠에 등록해 놓으면 **04.01** 처럼 일자정보가 자동으로 입력됩니다. :) 이뿐 아니라 여기다가 한시간 뒤, 하루 뒤, 한달 뒤, …..등도 자동으로 계산해서 입력되게 할 수 있는데요.  

간단 합니다. **%@+1D%m.%d**  

앞에 **%@+D**를 추가하면 자동으로 하루 추가된 일자가 입력 됩니다. 맞죠? 초단위에서 연도까지 방법은 모두 비슷하며, 반대로 지나간 일자는 **+**를  **-** 로 바꿔주면 됩니다. 매크로 위치에 따라 변하는 사항등 보다 자세한 사항을 알고 싶으시다면 아래 같이보기를 참조해 주세요. 추가할 Snippet 은 Today, Tomorrow, 3 Days Later, Next Week, Next Month 이며, 사용할 액션은 [여기](http://dl.dropbox.com/s/td8m4x4k40uztx6/DT.textexpander)링크를 복사해서 추가하시면 됩니다. 정말 간단한 것이라 익숙해질겸 한번 만들어 보실 것을 권장합니다.  

### LCP 액션 등록  
등록시 주의사항은 두가지 입니다. 우선 TextExpander의 단축키를 LCP에서 사용하기 위해서는 **< >**로 감싸줘야 합니다. 그리고 설정에서 Update TextExpander Snippets 를 해주는 것도 잊으면 않되겠죠? 나머지는 **Encoding** 과 관련된 내용입니다.   

**[[ list:일정...**  

부분인데요, 일반적으로 list를 쓰기 위해서  

**[ list:**  

이렇게 사용하면 됩니다만, LCP에서 Fantastical2로 일자정보를 보낼때 TextExpander의 단축키가 아닌 일자정보로 변경한 다음 입력되어야 하기 때문입니다. 이해를 위해서 앞뒤에 **[ ]** 를 하나씩 제거하고 실행해 보시면 금방 이해되실 꺼에요. 

{% raw %}
```  
fantastical2://x-callback-url/parse?sentence=[prompt:어떤 미리알림을 등록 할까요?]%20[[list:일정을 선택하세요.|Today=<ddat>|Tomorrow=<ttom>|3 Days Later=<ttdl>|NextWeek=<nnwk>|NextMonth=<nnmo>]]&x-success={{launchpro://}}
```
{% endraw %}

LCP 액션은 [여기](http://launchcenterpro.com/62rpwh)에서 다운받을 수 있습니다. 
