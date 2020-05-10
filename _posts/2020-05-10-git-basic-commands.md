---
layout: post
title: Git 기본 명령어
featured-img: github
mathjax: true
categories: [Devlog]
tags: [Git, Github]
---

# git 저장소 만들기

주로 다음 주 가지 중 한 가지 방법으로 Git 저장소를 쓰기 시작한다.

1. 아직 버전관리를 하지 않는 로컬 디렉토리 하나를 선택해서 Git 저장소를 적용하는 방법
2. 다른 어딘가에서 Git 저장소를 **_Clone_** 하는 방법

## 기존 디렉토리를 Git 저장소로 만들기

먼저 Git으로 관리하고 싶은 경우 우선 프로젝트의 디렉토리로 이동한다.

```jsx
$ cd /c/user/my_project
```

그리고 아래와 같은 명령을 실행한다.

```jsx
$ git init
```

이 명령은 .git 이라는 하위 디렉토리를 만든다. .git 디렉토리에는 저장소에 필요한 뼈대 파일(Skeleton)이 들어 있다. 이 명령만으로는 아직 프로젝트의 어떤 파일도 관리하지 않는다.

Git이 파일을 관리하게 하려면 저장소에 파일을 추가하고 커밋해야 한다. `git add` 명령으로 파일을 추가하고 `git commit` 명령으로 커밋한다. `git push` 명령어를 실행하면 실제 저장소에 파일이 반영된다.

```jsx
$ git add *.c
$ git add LICENSE
$ git commit -m "initial project version"
$ git remote add origin https://github.com/im-hyunjin/im-hyunjin.github.io.git --처음에만 실행
$ git push -u origin master
```

## 기존 저장소를 Clone 하기

다른 프로젝트에 참여하려거나(Contribute) Git 저장소를 복사하고 싶을 때 git clone 명령을 사용한다.

Git이 Subversion(SVN)과 다른 가장 큰 차이점은 서버에 있는 거의 모든 데이터를 복사한다는 것이다. git clone 을 실행하면 프로젝트 히스토리를 전부 받아온다.

git clone <url> 명령으로 저장소를 Clone 한다.

```jsx
$ git clone https://github.com/libgit2/libgit2
```

이 명령은 “libgit2” 라는 디렉토리를 만들고 그 안에 .git 디렉토리를 만든다. 그리고 저장소의 데이터를 모두 가져와서 자동으로 가장 최신 버전을 Checkout 해 놓는다.

아래과 같은 명령을 사용하여 저장소를 Clone 하면 libgit2이 아니라 다른 디렉토리 이름 myLibgit으로 Clone 할 수 있다.

```jsx
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

## 수정하고 저장소에 저장하기

- Tracked

  - Unmodified = 처음 저장소를 Clone했을 때
  - Modified
  - Staged → Commit(스냅샷)

- Untracked

![](./../assets/img/posts/2020-05-10-23-26-11.png)

워킹 디렉토리의 모든 파일은 크게 Tracked(관리대상임)와 Untracked(관리대상이 아님)로 나눈다.

Tracked 파일은 또 Unmodified(수정하지 않음)와 Modified(수정함) 그리고 Staged(커밋으로 저장소에 기록할) 상태 중 하나이다.

그리고 나머지 파일은 모두 Untracked 파일이다. Untracked 파일은 워킹 디렉토리에 있는 파일 중 스냅샷에도 Staging Area에도 포함되지 않은 파일이다.

처음 저장소를 Clone 하면 모든 파일은 Tracked이면서 Unmodified 상태이다.

## 파일을 새로 추적하기

아래 명령을 실행하고나면 Git은 README 파일을 추적한다.

```jsx
$ git add README
```

하위 디렉토리 모든 파일을 추적하려면 아래와 같이 실행한다.

```jsx
$ git add .
```

## Modified 상태의 파일을 Stage 하기

git add 명령은 파일을 새로 추적할 때도 사용하고 수정한 파일을 Staged 상태로 만들 때도 사용한다. Merge 할 때 충돌난 상태의 파일을 Resolve 상태로 만들때도 사용한다.

```jsx
$ git add CONTRIBUTING.md
$ git status
```

```jsx
On branch master
Your branch is up-to-date with 'origin/master'.
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   README
    modified:   CONTRIBUTING.md
```

두 파일 모두 Staged 상태이므로 다음 커밋에 포함된다. 만약 git add 명령을 실행한 후에 또 파일을 수정한다면 git add 명령을 다시 실행해서 최신 버전을 Staged 상태로 만들어야 한다.

## 변경사항 커밋하기

Git은 생성하거나 수정하고 나서 git add 명령으로 추가하지 않은 파일은 커밋하지 않는다. 커밋하기 전에 git status 명령으로 모든 것이 Staged 상태인지 확인할 수 있다. 그 후에 git commit 을 실행하여 커밋한다.

```jsx
$ git commit
```

메시지를 인라인으로 첨부할 수도 있다. commit 명령을 실행할 때 아래와 같이 -m 옵션을 사용한다.

```jsx
$ git commit -m "Story 182: Fix benchmarks for speed"
```

## Staging Area 생략하기

Staging Area는 커밋할 파일을 정리한다는 점에서 매우 유용하지만 복잡하기만 하고 필요하지 않은 때도 있다. 아주 쉽게 Staging Area를 생략할 수 있다. -a 옵션을 추가하면 Git은 Tracked 상태의 파일을 자동으로 Staging Area에 넣는다.

```jsx
$ git commit -a -m "added new benchmarks"
```

## 파일 삭제하기

Git에서 파일을 제거하려면 `git rm` 명령으로 Tracked 상태의 파일을 삭제한 후에(정확하게는 Staging Area에서 삭제하는 것) 커밋해야 한다. 이 명령은 워킹 디렉토리에 있는 파일도 삭제하기 때문에 실제로 파일도 지워진다.

Git 명령을 사용하지 않고 단순히 ~~워킹 디렉터리에서 파일을 삭제~~하고 `git status` 명령으로 상태를 확인하면 Git은 현재 “Changes not staged for commit” (즉, **_Unstaged_** 상태)라고 표시해준다.

```jsx
$ rm PROJECTS.md
```

Staging Area에서만 제거하고 워킹 디렉토리에 있는 파일은 지우지 않고 남겨둘 수 있다. 다시 말해서 하드디스크에 있는 파일은 그대로 두고 Git만 추적하지 않게 한다.

```jsx
$ git rm --cached README
```

여러 개의 파일이나 디렉토리를 한꺼번에 삭제할 수도 있다. 아래와 같이 git rm 명령에 file-glob 패턴을 사용한다.

```jsx
$ git rm log/\*.log
```

이 명령은 log/ 디렉토리에 있는 .log 파일을 모두 삭제한다.

```jsx
$ git rm \*~
```

이 명령은 ~ 로 끝나는 파일을 모두 삭제한다.

## 파일 이름 변경하기

Git은 다른 VCS 시스템과는 달리 파일 이름의 변경이나 파일의 이동을 명시적으로 관리하지 않는다. 다시 말해서 파일 이름이 변경됐다는 별도의 정보를 저장하지 않는다.

```jsx
$ git mv file_from file_to
```

## 파일 무시하기

파일을 무시하려면 .gitignore 파일을 만들고 그 안에 무시할 파일 패턴을 적는다.

```jsx
$ cat .gitignore
*.[oa]
*~
```

첫번째 라인은 확장자가 “.o” 나 “.a” 인 파일을 Git이 무시하라는 것이고 둘째 라인은 ~ 로 끝나는 모든 파일을 무시하라는 것이다. “.o” 와 “.a” 는 각각 빌드 시스템이 만들어내는 오브젝트와 아카이브 파일이고 ~ 로 끝나는 파일은 Emacs나 VI 같은 텍스트 편집기가 임시로 만들어내는 파일이다.

아래는 .gitignore 파일의 예이다.

```R
# 확장자가 .a인 파일 무시 확장자가
*.a

# 윗 라인에서 확장자가 .a인 파일은 무시하게 했지만 lib.a는 무시하지 않음
!lib.a

# 현재 디렉토리에 있는 TODO파일은 무시하고 subdir/TODO처럼 하위디렉토리에 있는 파일은 무시하지 않음
/TODO

# build/ 디렉토리에 있는 모든 파일은 무시
build/

# doc/notes.txt 파일은 무시하고 doc/server/arch.txt 파일은 무시하지 않음
doc/*.txt

# doc 디렉토리 아래의 모든 .pdf 파일을 무시
doc/**/*.pdf
```

<br><br><br>
출처 : [https://git-scm.com/book/ko/v2](https://git-scm.com/book/ko/v2)
<br><br>
