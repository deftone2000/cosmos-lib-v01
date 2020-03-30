---
title: "Autofs"
excerpt_separator: "<!--more-->"
image: 
  path: /images/auto-foce.png
  thumbnail: /images/auto-foce01.png
  caption: "Photo from [COSMO'S](https://www.instagram.com/deftone2000)"
last_modified_at: 
---

Autofs를 이용한 맥과 NAS 드라이브 연결과 관리 방법입니다. <!--more--> Synology NAS 를 도입한 후 다양한 활용 방법을 시도해 보면서 즐겁게 사용하고 있습니다. 플랫폼과 디바이스 종류에 상관없이 매우 넉넉한 저장공간을 장소의 제약 없이 사용하는 것은 큰 장점입니다. 특히 맥북과 연동할 때는 네트워크 드라이브를 연결하여 사용하는 경우가 많습니다. 다음은 Finder 메뉴를 이용한 NAS 드라이브와 맥을 연결 시키는 방법입니다.  

### 기본적인 NAS 드라이버와 맥북 연결  
Finder > 이동 > 서버에 연결(⌘+K)을 선택하고 URL, IP 주소 또는 DNS 이름을 입력합니다. 이 방법은 간단하지만 NAS나 맥을 재시작 할 경우 매번 다시 설정해야하는 불편함이 있습니다. 그래서 재시작시 NAS 드라이브가 마운트 되는 스크립트를 실행 시키는 방법이 있지만 이것도 문제가 있습니다. 제가 사용하는 Synology NAS의 경우 일정시간 동안 사용하지 않으면 잠자기모드를 자동으로 설정합니다. 이는 디스크의 수명을 보존하고 사용하지 않을 때는 소비 전력을 감소시켜서 유용합니다. 하지만 맥북을 재시작 할때만 NAS 드라이브에 접근하기 때문에 이러한 장점을 활용할 수 없게 됩니다.  

autofs[^1]를 사용하면 파일 접근이 필요한 경우에 OS X에서 네트워크 드라이브를 자동으로 마운트해줍니다. 이는 맥과 NAS 상태에 상관 없이 사용자의 필요에 따라 자동으로 연결이 유지된다는 의미입니다. 

### autofs를 활용하여 NAS 드라이버와 맥북 연결  
`Step 1` 다음을 터미널에서 실행하여 `auto_master`[^2]를 열어줍니다.  

```
$ sudo nano /etc/auto_master
```

`Step 2` 자신의 로그인 암호를 입력하면 편집모드로 진입하며, 다음과 같이 수정합니다.  

```shell
#
# Automounter master map
#
+auto_master		# Use directory service
/net			-hosts		-nobrowse,hidefromfinder,nosuid
/home			auto_home	-nobrowse,hidefromfinder
/Network/Servers	-fstab
/-			-static
/mypath		/etc/auto_nas
```
처음 autofs 사용하는 경우 마지막 줄을 추가하시면 됩니다. `/mypath`는 마운트되는 경로와 이름입니다. `/etc/auto_nas`는 마운트 세부설정 파일과 경로입니다.  

`Step 3` auto_nas 파일을 지정한 경로에 만들어 줍니다.  

```shell
$ sudo nano /etc/auto_nas
```

`Step 4` auto_nas 를 사용환경에 맞게 편집합니다.  

```shell
document -fstype=afp afp://username:password@192.168.0.100/document
```
저의 경우 afp를 사용하지만 smb, webdav도 사용할 수 있습니다. 당연히 공유폴더명, 아이디, 비밀번호, 연결주소는 각각 사용환경에 따라 변경합니다.  

`Step 5` 설정한 autofs 를 실행하고 확인합니다.  

```shell
$ sudo automount -vc
```

정상적으로 설정이 되었다면 다음과 같은 출력을 확인 할 수 있습니다.  

```shell
automount: /net updated
automount: /home updated
automount: /mnt/NAS mounted
automount: no unmounts
```

---

- [Keep Network Drives Mounted on Mac OS X using Autofs](http://blog.grapii.com/2015/06/keep-network-drives-mounted-on-mac-os-x-using-autofs/)
- [autofs를 이용한 nas 자동 접속](http://jmjeong.com/autofs/)

[^1]: utility that will mount network volumes on your OS X system
[^2]: autofs 환경설정 파일(auto_master : 주 설정, auto_mic : 추가설정)

