---
title: Obsidian iOS 모바일 앱 Google Drive 연동 셋팅
date: 2026-03-21 00:00:00 +0900
categories: Tools
tags:
  - obsidian
  - google-drive
---

## 개요

Obsidian에서 To-do를 이용하다 보니 핸드폰에서 To-do를 확인하고 싶을 때가 많았다. 이김에 미뤄뒀던 모바일 앱 연동 셋팅을 해보려 한다

> **나의 환경**
> - 노트북: Windows  
> - 핸드폰: iOS  
> - 아이패드: iOS  
> - Cloud: Google Drive

iOS는 파일 시스템 접근이 제한적이라 Android보다 연동 방법이 까다롭다. 이전에 `Remotely Save`라는 플러그인을 사용하여 Onedrive를 이용하여 연동했었는데, 현재는 각종 서비스가 유료화됐다.  
특히 내가 이용하려는 Google Drive를 이용한 연동 방식이 Pro 요금제에 속하여 다른 방법을 찾아야 했다

검색 결과 `Google Drive Sync`라는 플러그인이 가장 현실적인 대안인 듯 하여 이를 이용한 모바일 앱 연동 셋팅을 해보려 한다

## 셋팅

### 1. 설치

> **Google Drive Sync - Richard Xiong**  
> [GitHub - RichardX366/Obsidian-Google-Drive](https://github.com/RichardX366/Obsidian-Google-Drive)  
{: .prompt-info }

![](../assets/img/posts/2026-03-21/obsidian%20모바일%20앱%20연동%20셋팅-1774069050538.webp)  
Obsidian에서는 커뮤니티 플러그인 항목에서 `Google Drive Sync` 검색 시 쉽게 설치할 수 있다  
설치한 뒤에는 **활성화 버튼**을 잊지 말고 누르도록 하자

### 2. Google 로그인

> **OGD Sync 페이지**  
> 링크: [OGD Sync](https://ogd.richardxiong.com/)  
{: .prompt-info }

OGD Sync 페이지에 접속 후 우측 상단의 로그인 버튼을 통해 **사용하려는 Google Drive 계정**으로 로그인한다

### 3. Refresh Token 붙여넣기

![](../assets/img/posts/2026-03-21/obsidian%20모바일%20앱%20연동%20셋팅-1774073715063.webp)

로그인 하면 내가 사용할 Refresh Token이 뜬다. 복사 후 해당 플러그인의 설정 칸에 발급받은 Refresh Token을 붙여넣도록 한다.

Refresh Token을 붙여넣을 때 내가 연동하고자 하는 Vault가 어떠한 방식으로든 빈 상태가 아니면 아래와 같은 문구가 뜬다

> Your current vault is not empty! If you want our plugin to handle the initial sync, you have to clear out the current vault. Check the readme or website for more details

### 4. 충돌 방지한 연동 과정

연동 시 기존 파일들과의 충돌 방지를 위해 **vault를 백업해두고 vault가 빈 상태에서 연동**해야한다

1. `.obsidian`파일을 제외한 나머지 vault 파일들을 임시 폴더로 이동
2. Refresh Token 붙여넣기  
	![](../assets/img/posts/2026-03-21/obsidian%20모바일%20앱%20연동%20셋팅-1774075071242.webp)  
	붙여넣기에 성공할 시 위와 같이 뜬다
3. Obsidian 재시작
4. 임시 폴더에 있던 기존 파일 다시 vault에 이동
5. `Google Drive Sync: Push to Google Drive` 명령어 혹은 `옆 리본의 아이콘`을 클릭하여 Google Drive에 폴더 내용 올리기

Google Drive에 vault의 파일들이 잘 올라가 있으면 성공이다

### 5. push 테스트

![](../assets/img/posts/2026-03-21/obsidian%20모바일%20앱%20연동%20셋팅-1774080171321.webp)  
![](../assets/img/posts/2026-03-21/obsidian%20모바일%20앱%20연동%20셋팅-1774080312040.webp)  
**push 테스트**
- 새 post를 작성하고 push 명령어 수행 시 위와 같이 뜬다면 설정 끝
- 삭제 시에도 push 반영 목록으로 뜬다

### 6. 모바일 기기 연동

1. Obsidian 모바일 앱 설치
2. 새 vault 생성
	- `Create new vault` 클릭
	- vault 이름은 PC vault 이름과 동일하게 설정 (대소문자까지 동일하게!)
3. Google Drive Sync 플러그인 설치
	- PC 버전에서 설치-활성화한 과정과 동일
4. Refresh Token 붙여넣기
	- 이전에 얻어 PC 버전에 붙여넣기한 Refresh Token을 모바일 플러그인 설정에도 똑같이 추가한다
	- 붙여넣기 후 Obsidian 앱 재시작
5. pull 실행
	- 재시작하면 알아서 pull 작업이 이루어져 pc로 올려둔 파일들이 연동될 것이다
	- 만약 연동이 이루어지지 않았다면, 명령어 팔레트를 열어 `Google Drive Sync: Pull from Google Drive` 명령을 수행한다

## 주의사항

> **이용 주의사항**
> - **충돌 방지:** `한 기기에서 편집 → Push → 다른 기기에서 Pull` 순서로 사용
> 	- 동시사용 X
> - **인터넷 연결 유지:** 동기화 중 앱을 닫거나 인터넷 연결이 끊기면 데이터 손상이 발생할 수 있다
> - **Obsidian 앱 외부에서 파일 직접 수정 금지:** 플러그인이 변경사항을 추적하지 못한다  
{: .prompt-warning }
