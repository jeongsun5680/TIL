# 08. Merge Branch

1. Fast-Forward

   ```
   (main) $ git switch -c login
   (login) $ touch login.txt
   (login) $ git add login.txt -> $ git commit -m 'login 추가'
   (login) $ git switch master
   (main) $ git merge login
   ```

   - merge 이전

     ```
     $ git log --oneline --graph --all
     * 0fa3953 (login) login 추가
     * 84a25b3 (HEAD -> master) b 추가
     * 54ca575 a 추가
     ```

   - merge 이후

     ```
     $ git log --oneline --graph --all
     * 0fa3953 (HEAD -> master, login) login 추가
     * 84a25b3 b 추가
     * 54ca575 a 추가
     ```

   - `git branch -d [브랜치이름]` : 브랜치 삭제

2. 3-Way Merge

3. Merge Conflict

