# 06. gitignore

* 우리가 git으로 관리하고 싶지 않은 파일들을 제외 시키는 방법

  * 우리가 원하지 않는 파일을 제외
  * 외부에 공개되면 안되는 것들 (key, secret)

* `.gitignore`

  * `.gitignore`에 작성도니 파일들은 git으로 관리하지 않겠다! 무시해라!

  ```
  .DS_Store # Mac OS에서만 사용하는 파일
  ```

* 작성법

  ```
  f.txt # 특정 파일
  secret/ # 특정 폴더
  *.png # 특정 확장자 : .png로 끝나는 모든 확장자를 제외한다
  !profile.png # 모든 .png는 제외, profile.png는 넣고!
  ```

* b.txt를 gitignore에 넣었더니 무시가 되지 않는다, 왜인가?

  * 처음부터, git으로 관리한 적이 없을 때부터 관리를 해줘야 한다

* 그렇다면 이미 commit을 한 파일들은 어떻게 제외할 수 있을까?

  1. `.gitignore`에다가 파일을 명시
  2. `git rm --cached [파일명]` : git bash에서 명령어를 입력
     - git에서 더 이상 관리하지 않겠다!
     - `git status`에는 `deleted : b.txt`라고 뜬다 = WD에서 삭제해서 더 이상 관리하지 않겠다!

* `.DS_Store` : Mac OS

* `Thumbs.db` : Windows

