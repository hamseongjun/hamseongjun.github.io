---
layout: single
title: "참고용 : 깃허브 사용법"
categories: "ASC-Programing_study"
tags: [ASC, 참고용]
author_profile: false
header:
    teaser: /assets/images/GitHub.jpeg
sidebar:
    nav: "counts"
---

<br>


- 깃허브 왜 사용하냐?
    - 버전 관리
    - 코드 협업
    - 공유
    - 등등..

![](https://velog.velcdn.com/images/hamseongjun/post/f8ed43ae-e289-4c66-aa26-7fd35344a2a2/image.png)


기본 설정

- `git config --global [user.name](http://user.name/) “자신의 닉네임”`
- `git config --global user.email “자신의 이메일”`

기본 명령어

- `git init` : git 저장소(Repository) 생성
    - .git(숨김파일) 생성
- `git add` : 버전 관리할 파일을 등록, 새로운 버전에 선택적으로 파일(변경내용)을 포함시킴
- `git status` : 파일의 상태를 알 수 있음
- `git commit` : 버전 생성
    - -m “메시지” : 커밋 메시지 설정
- `git push` : 원격 저장소로 업로드
- `git log` : commit log 봄
- `git reset “file명”` : add취소
- `git clone “주소”` : 레파지토리 복사해옴
- `git checkout “버전id”` : 해당 버전으로 이동