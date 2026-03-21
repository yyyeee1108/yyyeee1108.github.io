<%*  
// 1. 팝업창으로 제목 입력 받기  
let title = await tp.system.prompt("포스팅 제목을 입력하세요");

// 제목을 입력하지 않고 취소했을 경우를 대비해 기본값 설정  
if (!title) title = "untitled";

// 2. 날짜 및 시간 설정  
let date = tp.date.now("YYYY-MM-DD");  
let time = tp.date.now("HH:mm:ss");

// 3. 파일명 변환 (소문자화, 공백을 하이픈으로 변경)  
// 예: "My New Post" -> "my-new-post"  
let slug = title.toLowerCase()  
                .replace(/\s+/g, '-')  
                .replace(/[^\w-]/g, ''); // 특수문자 제거 (선택사항)

let newFileName = `${date}-${slug}`;

// 4. 파일 이름 변경 실행
await tp.file.rename(newFileName);
%>---
title: <% title %>
date: <% date %> <% time %> +0900
categories:
tags:
---

# <% title %>