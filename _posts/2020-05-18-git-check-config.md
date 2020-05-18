---
layout: post
title: Git config 설정 확인 및 수정하기
featured-img: github
mathjax: true
categories: [Devlog]
tags: [Git, Github]
---

git config 안에 다른 사용자 정보가 저장되있는 경우 config에 설정된 사용자 정보를 삭제하고 내 계정을 새롭게 연동해봅시다. 

# config 확인

config에 설정되있는 전체 내용을 봅니다.

config에 user.name과 user.email이 설정되있는 걸 확인할 수 있습니다.

```jsx
git config --list
```

```jsx
core.symlinks=false
core.autocrlf=true
core.fscache=true
color.diff=auto
color.branch=auto
color.status=auto
...
user.name="User1"
user.email="user1@test.com"
```

# 사용자 계정 삭제

config에 저장되있는 계정 정보를 삭제해줍니다.

```jsx
$ git config --unset user.name
$ git config --unset user.email
```

전역으로 설정되었을 경우 `--global`을 붙혀 작성해줍니다.

```jsx
$ git config --unset global user.name
$ git config --unset global user.email
```

다시 한번 `git config --list`를 입력해  정상적으로삭제되었는지 확인합니다.

# 사용자 계정 추가

마찬가지로 전역으로 설정하고 싶을 경우 `--global`을 추가해주면 됩니다.

```jsx
$ git config user.name "User2"
$ git config user.email "user2@test.com"
```

```jsx
$ git config --global user.name "User2"
$ git config --global user.email "user2@test.com"
```

<b><br><b><br><b><br>