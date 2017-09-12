
## I. Environment Variable

#### Vào This PC --> properties --> Advanced system setting --> Advanced --> Environment Variables --> Path --> Edit --> this Pass in path : 


```
C:\Ruby23-x64\bin;

C:\Program Files\nodejs;

C:\Users\Dao.DC\AppData\Roaming\npm;

C:\Users\Dao.DC\AppData\Roaming\npm\node_modules\grunt-cli\bin;

C:\Users\Dao.DC\AppData\Roaming\npm\node_modules\grunt\bin;
```



## II. Git Guide

 **1. Create SSH KEY:**

       - ssh-keygen -t rsa -C "daodcfrontend@gmail.com"
       - Enter --> Enter
       - cat ~/.ssh/id_rsa.pub --> See SSH KEY --> Copy SSH KEY
       - http://192.168.1.241/profile/ pass SSH KEY on Input Content.

 **2. Git config:**

       - $ git config --global user.name "daodc"
       - $ git config --global user.email daodcfrontend@gmail.com

  **3. Create new branch `feature/20161107_daodc_createpage_top`:**

       1. Switch `develop` branch 
           [git checkout develop]
       2. Get code lasted
           [git pull origin develop]
       3. Create branch
         - [git checkout -b feature/20161107_daodc_createpage_top]
         - [git add -A] or [git add *]
         - [git commit -m "Create top page."]
         - [git push origin feature/20161107_daodc_createpage_top]

  **4. Merge `develop` to `feature/20161107_daodc_createpage_top`:**

       1. Switch `develop` branch 
           [git checkout develop]
       2. Get code lasted
           [git pull origin develop]
       3. Switch branch will merge `feature/20161107_daodc_createpage_top`
          [git checkout feature/20161107_daodc_createpage_top]
       4. Merge `develop` to `feature/20161107_daodc_createpage_top`
          [git merge develop]
       5. Conflicts
          5.1. if has `Conflicts` will fix it.
              5.1.1. Show file `Conflicts`
                `CONFLICT (content): Merge conflict in lib/hello.html`
              5.1.2. Open the file will fix `lib/hello.html`
                - fix Conflicts -> finished -> go to step `6`
       6. Add new code to server GIT
          - git status
          - git add --all
          - git commit -m 'fix Conflicts'
          - git push origin `feature/20161107_daodc_createpage_top`
       7. Link reference
          - https://githowto.com/resolving_conflicts
       
  **5. Backup the code to temporary `git stash`:**

       1. Show the code change
          [git status]
       2. You don't want to commit, so you use backup the code to temporary
          [git stash]
       3. Show all list `stash`
          [git stash list]
            - stash@{0}: WIP on master: 049d078 added the index file
            - stash@{1}: WIP on master: c264051 Revert "added file_size"
            - stash@{2}: WIP on master: 21d80a5 added number to log
      4. Get stash index {2}
          [git stash apply stash@{2}]
      5. Link reference: 
          - https://git-scm.com/book/en/v1/Git-Tools-Stashing

  **6. Revert code older via `commit`:**

      1. Show the log of commit
          [git log]
            - commit ca82a6dff817ec66f44342007202690a93763949
              Author: Scott Chacon <schacon@gee-mail.com>
              Date:   Mon Mar 17 21:52:11 2008 -0700

                 changed the version number
     2. Revert code on commit `ca82a6dff817ec66f44342007202690a93763949`
         [git check out `ca82a6dff817ec66f44342007202690a93763949` (id)]

  **7. Get all branch form `GIT Server` to `Your Local`:**

         [git fetch --all]
     
  **8. Create SSH KEY:**

       - ssh-keygen -t rsa -C "dao.dc@globaldesignit.vn"
       - Enter --> Enter
       - cat ~/.ssh/id_rsa.pub --> See SSH KEY --> Copy SSH KEY
       - http://192.168.1.241/profile/ pass SSH KEY vào Input Content.

  **9. Add file:**

       - git add <ten_file>
       - git add <ten_file1 ten_file2 ten_file3>

  **10. Reset/Revert branch:**

       - git log(Xem id commit)
       - git reset --hard <commit_before_merge>(git reset --hard bbf30a33ae9fc8046a407ab7731509bae93a6de9)

  **11. Deleting local branches in Git:**

         [$ git branch -d feature/login]

   **12. Deleting remote branches in Git:**

         [$ git push origin --delete <branch_name>]
         [$ git branch -d <branch_name>]

   **13. Khi Git xuất hiện lỗi này khi push len:**
        
         ```
         \nThis repository is configured for Git LFS but 'git-lfs' was not found on your path. If you no longer wish to use Git LFS, remove this hook by deleting .git/hooks/pre-push.\n
error: failed to push some refs to 'https://github.com/dmorris99/MAOMAO.git'
         ```

       ==> Thì vào folder delete .git/hooks/pre-push : xóa file pre-push là được.

   **14. Đưa folder tên có dấu cách lên Git thì phải thêm dấu \ chỗ space:**

   - ```git add styles/fonts/Courier\ New/```

   **15. Remove commit:**

   - ```git reset --soft HEAD~1```
   - ```git status```
   - ```rm -rf cms8341/shared/js.zip```
   - ```git add -A```
   - ```git commit and push```
