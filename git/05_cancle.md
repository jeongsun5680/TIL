# 05. 취소하기

1. git add 취소하기

   - git add가 된 상황

     ```bash
     $ git status
     On branch master
     Changes to be committed:
       (use "git restore --staged <file>..." to unstage)
             new file:   e.txt
     ```

     ```
     $ git restore --staged e.txt
     ```

     - 구버전

       ```
       $ git reset HEAD e.txt
       ```

     ```bash
     $ git status
     On branch master
     Untracked files:
       (use "git add <file>..." to include in what will be committed)
             e.txt
     
     nothing added to commit but untracked files present (use "git add" to track)
     ```



1. git add 취소 (위의 내용)

2. git commit 취소 (되돌아가기)

   - 옵션

     ``` $ git reset --mixed [hash]
     $ git reset --mixed [hash]
     ```

     - staging 없앰 + **작업한 것은 남아있음.**
     - 옵션이 없다면, mixed가 기본

     ```
     $ git reset --soft [hash]
     ```

     - staging 그대로 유지 + **작업한 것은 남아있음.** : ex) 커밋 메세지만 실수한 경우

     ```
     $ git reset --hard [hash]
     ```

     - **[주의]** 완전히 취소하는 것 (작업한 것도 삭제!)

   - hash

     - ```
       $ git reset 해쉬숫자
       ```

   - HEAD의 상대적 위치

     - HEAD~{숫자}

       - HEAD~1 = `HEAD~`
       - HEAD~2

       ```bash
       $ git reset HEAD~
       ```

       - commit 되돌리기
         - HEAD~1 (1단계 전으로 되돌리고)
         - `--mixed` : staging은 취소, 작업 내용은 유지 
         - `staging은 취소` : add부터 다시 해야한다는 것

   - git log시 내용이 너무 많이 잘리는 경우

     - q로 종료
     - 방향키로 위아래 왔다갔다 할 수 있음

3. WD(Working Directory) 변경 내용 취소(삭제)하기

   - WD
     - 지금 우리가 작업 중인 공간
     - == Git이 관리하고 있는 공간
     - == 기록이 한번이라도 기록된 파일들이 있는 공간
     - ex) a.txt ~ e.txt까지 폴더에 있더라도, g.txt와 e.txt는 git으로 한 번도 관리되지 않았다면 a.txt~f.txt만 WD에 있는 것이다.

   ```bash
   $ git restore [파일명]
   $ git restore a.txt
   ```

   - 구버전

     ```bash
     $ git checkout -- [파일명]
     ```

     

