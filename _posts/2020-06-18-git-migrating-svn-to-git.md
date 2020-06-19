---
layout: post
title: SVN에서 GIT으로 이전하기
featured-img: github
mathjax: true
categories: [Devlog]
tags: [Git, Github]
---

1. GIT 다운로드

    [Git - Git 설치](https://git-scm.com/book/ko/v2/%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-Git-%EC%84%A4%EC%B9%98)

2. SVN저장소를 GIT에 옮기기 위해 GIT 내 신규 저장소 생성
3. 로컬에 임시 폴더 생성합니다.
4. command 창을 열어 앞에서 만든 임시 폴더 경로로 이동합니다.

    ```r
    $ cd [로컬 폴더 경로]
    ```

5. git svn를 사용해 커밋했던 히스토리와 모든 파일을 로컬환경에 복사해줍니다. 

    ```r
    $ git svn clone [SVN 저장소 주소]
    ```

6. git으로 push 할 때 특정 파일을 무시하려면 .gitignore 파일을 만들고 그 안에 무시할 파일 패턴을 적어줍니다. 

    [참고] visual studio에서 작성된 프로젝트 및 솔루션을 위한 .gitignore

    [github/gitignore](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore)

    예시로 작성해놓은 .gitignore 😄

    ```r
    # Visual Studio 2015/2017 cache/options directory
    .vs/
    # Files built by Visual Studio
    *.obj
    *.pdb
    *.log
    *.rptproj.bak
    ```

7. 로컬 폴더에 새 리모트 저장소를 git url로 설정해줍니다.

    ```r
    $ git remote add origin [git repository url]
    ```

8. git으로 push합니다.

    ```r
    git push -u origin master
    ```
<br><br>