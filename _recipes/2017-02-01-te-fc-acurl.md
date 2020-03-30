---
title: "나만의 단어장 만들기"
excerpt_separator: "<!--more-->"
image: 
  path: /images/flash-card-00.jpg
  thumbnail: /images/flash-card-011.jpg
  caption: "Photo from [COSMO'S](https://www.instagram.com/deftone2000)"
last_modified_at: 
---

단어를 검색 할때, 중요하고 기억하고 싶은 단어는 단어학습 어플에  별도로 저장해서 나만의 단어장으로 활용한다. <!--more--> 또한 이러한 일련의 과정을 Terminology, FlahsCards Deluxe, URL action 을 이용해서 자동화 한다.

### Process  
- Terminology에서 단어검색
- Terminology action 다음, 네이버 단어검색
- 영한사전 단어 뜻 [[clipboard]] 에 저장
- Terminology Action Drafts 연동
- Drafts Word to Dropbox 실행
- FlashCards Dropbox에서 단어장 import
- FlashCards 동기화 설정

### Drafts action  
Tag Reference  

- %% %% : Markdown convert it to HTML.

Word to Dropbox action(2 action steps)
*remove blank lines from drafts* : script action, drafts의 필요없는 공백을 제거  
{% raw %}
```
draft.content = draft.content.replace(/$\s*\n+/gm, "\n");
commit(draft);
```
{% endraw %}
*word to dropbox* : 지정한 양식[^1]에 단어, 뜻을 저장합니다. 저장위치는 dropbox root 폴더 Flashcards Deluxe, Write type은 append  
{% raw %}
```
%%###[[title]]%%	%%###[[line|2]]%%|[[line|3]]	[[clipboard]]
```
{% endraw %}  

### Terminology action  
Tag Reference  

- definition마크다운 포맷으로 된 단어의 뜻.
- [[clipboard]] : Current contents of the iOS clipboard.  

*word to flashcard* : 검색한 단어를 drafts로 보내 word to dropbox action 발동  
{% raw %}
```
drafts4://x-callback-url/create?text=[[definitions]]&action={{Word to Dropbox}}&x-success={{terminology://}}
```
{% endraw %} 

![terapp]({{ '/images/flash-card-01.jpg' | absolute_url }}){: .align-center} 



### FlahsCards Deluxe

위 과정을 무사히 마치면 일단, dropbox에 txt 형식의 파일이 저장됩니다. 이제 이것을 가지고 단어장으로 활용하는 부분만 남았습니다.  

*import*  
앱을 실행한 후 상단의 `+ > 드롭박스 > terminology > 다운로드`  

*동기화*  
`설정 > 동기화 > 설정 > 개별 단어장 > terminology 활성화` 이렇게 하면 기존의 txt 파일이 "Flashcards Deluxe/_Sync/terminology.txt"로 복사된다.  

### Drafts action 변경  
동기화를 위해 txt파일의 업데이트 위치를 변경한다. `Flashcards Deluxe -> Flashcards Deluxe/_Sync`

### 최종 모습 

![terapp]({{ '/images/flash-card-02.jpg' | absolute_url }}){: .align-center} 

앞으로 단어를 추가하면 자동적으로 Flashcards와 동기화 된다. Terminology의 즐겨찾기 추가기능을 사용하는 것도 방법이지만, FlashCards 의 학습기능을 활용하기 위해 개인적으로 적용해본 것입니다. 

[^1]: Flashcards Deluxe에서 txt 파일을 이용할 경우 질문과 답을 탭(Tab)키로 구분. 엔터(Enter)키를 이용해서 각 카드를 구분합니다. "질문   {tab}   답변   {return} 질문   {tab}   답변   {return}"





