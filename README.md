

!   !   !

Please note that all commit messages, the amount of commits, branches names must be the same as in tasks to successfully pass tests.

!   !   !


Create an empty git repository with git init command. Also read up about --bare option and bare repositories themselves. 

Create a new file with touch README.md command. 
    git init && touch README.md


To modify the existing file, we will use VIM text editor. 
Type vim README.md command to open vim text editor. 
Press letter i to enter the insert mode. 
Type in “Hello World” or something you like. 
Press escape on the keyboard to exit from insert mode and go to the command mode. 
In the command mode press shift + ZZ to save current file and exit.  
In the bottom left corner you can see that currently the editor is in insert mode.

    vim README.md
    i
    Type in “Hello World” or something you like.
    Press escape on the keyboard to exit
    shift + ZZ to save current file and exit


To check the progress type git status command. 
You should see that readme file is untracked now. 
You should check for a status as often as it is possible. 
If you always read status carefully enough, you will never end up in strange unpredictable situations.

    git status


To track readme you can use git add . command. 
This will track and stage all the files in the current directory. 
Now you should see that your readme file is green which means it is also staged. 
Take a moment to read about tracking and staging and how they are different with each other.

It is time to commit changes. 
To create commit use git commit -m “created readme” command which will create commit with corresponding message. 
Your working tree should be clean now. 

    git add . && git commit -m "created readme"


We are going to create new branch called develop, which will contain all the functionality you are currently working on. 
To create a new branch, execute git checkout -b develop command. 
This will create new branch from the current (master). 
Create git_task branch from develop and git_0 branch from git_task. 
You can use git show-branch command to view all branches at once. 
The branch you are currently working with is marked with * symbol.

    git checkout -b develop && \
    git checkout -b git_task && \
    git checkout -b git_0 && \
    git show-branch


Now we will 
    with vim, add some changes to README.md, 
    check status, 
    stage changes with git add README.md command, 
    commit changes, 
    check the result (status) then 
    checkout to git_task branch (with git checkout git_task command) and 
    merge changes from git_0 branch with git merge git_0 --no-ff command. 
Take some time to read about merging and no-ff option. 
This is usually the default pull request merging behavior so you will work with it on you daily basis. 
Also note that you can view staged changes with git diff --cached command. 
For example tere we can see that new line “changes from git_0” was added to the file.

        with vim, add some changes to README.md
    vim README.md
    i
    add an update or something you like.
    shift + ZZ to save current file and exit
    git add . && git commit -m "changed readme"

        checkout to git_task branch (with git checkout git_task command) and         merge changes from git_0 branch with git merge git_0 --no-ff command.
    git checkout git_task && git merge git_0 --no-ff


 
    optional
Also note that you can view your latest changes with gitk command (which should invoke gitk tool). 
If this command does nothing or returns error, this usually means that you do not have gitk installed by default (e.g. working from mac). 
This tool is not necessary and is the matter of choice.

    gitk


Now repeat merging process to get your commit to master (through develop of course) branch. 
When you finish, you can use something this git log --all --graph --decorate --oneline --simplify-by-decoration or this git log --graph --oneline –all command. 

These commands were found on the stackoverflow as an answer to a question of viewing git history as a tree. 
This is not the best solution but it is more than enough for our needs. 
You output should look similar to this: 
From this picture you can see that the HEAD is currently looking at the master’s latest commit. 
We have created 5 commits: 2 with actual edits and 3 merge commits.


    git checkout develop && git merge git_task --no-ff
    git checkout master && git merge develop --no-ff


    repeat merging process to get your commit to master (through develop of course) branch. 
    git log --all --graph --decorate --oneline --simplify-by-decoration
        or
    git log --graph --oneline



Synchronize all created branches with a remote repository.

    git push (fo each of)


The idea here is simple. You should always develop you features in custom branches made from develop branch. 
When you feature is ready it goes to the develop branch (usually with pull request instead of merge). 
When the release time has come, all the merging to the develop branch should stop (or you may create custom *** pre_release*** branches with locked functionality). 
develop branch (or pre_release) should be tested and stabilized. 
As soon as the branch is stable, it goes to the master branch (or you may have different release branches and even don’t have a master, or don’t use master branch at all). 
This procedure might differ from project to project and always should be designed with the respect to the concrete project and goals. 
All this helps to keep the repository clean and always have some stable versions for the production.



Task 2


Part 1

We are going to practice some skills obtained in the previous task. If you come across something you still don’t know, please use links provided in the descriptions, internet search, other students as sources of knowledge and help. For this task you will create two separate branches git_1 and git_2 in your remote repository and local tracked branches with same names. Both these branches should be made of the git_task branch.

in your remote repository, create two separate branches git_1 and git_2 and local tracked branches with same names. Both these branches should be made of the git_task branch.
    
    git checkout -b git_2 && git checkout -b git_1



git_1: Add and commit firstFile.txt file with 10 lines with message 'Added firstFile.txt to git_1'.
    git checkout git_1
    touch firstFile.txt && vim firstFile.txt
    i
    Added firstFile.txt to git_1 x 10
    esc+sh+zz
    git add . && git commit -m "Added firstFile.txt to git_1"
    


git_1: Add and commit secondFile.txt file with 10 lines with message 'Added secondFile.txt to git_1'.
    git checkout git_1
    touch secondFile.txt && vim secondFile.txt
    i
    Added secondFile.txt to git_1 x 10
    sh+zz
    git add . && git commit -m "Added secondFile.txt to git_1"


Merge branch git_1 to git_2 with default message 'Merge branch 'git_1' into git_2'
    git checkout git_2 && git merge git_1 -m "Merge branch 'git_1' into git_2"


git_2: Update and commit any two lines in secondFile.txt with message 'Changed 2 lines in secondFile.txt in git_2'
    git checkout git_2
    vim secondFile.txt
    i
    Update any two lines
    sh+zz
    git add . && git commit -m "Changed 2 lines in secondFile.txt in git_2"


git_1: Update and commit the same 2 lines with the different info in secondFile.txt with message 'Changed 2 lines in secondFile.txt in git_1'.
    git checkout git_1 && vim secondFile.txt
    i
    Update the same 2 lines with the different info
    sh+zz
    git add . && git commit -m "Changed 2 lines in secondFile.txt in git_1"
    

Merge branch git_2 to git_1, resolve conflict. Left all (4) modified lines. Commit with message 'Fixed merge conflict'
    git merge git_2 -m "Merge branch 'git_2 into git_1"
    git add . && git commit -m "Fixed merge conflict"


git_1: Update and commit 1.txt file, modify two lines. Message - 'Changed 2 lines in firstFile.txt in git_1'
    vim firstFile.txt
    i
    modify two lines
    git add . && git commit -m "Changed 2 lines in firstFile.txt in git_1"
    wsc+sh+zz


git_1: Update and commit 1.txt file, modify another two lines: 'Changed another 2 lines in firstFile.txt in git_1'
    vim firstFile.txt
    i
    modify another two lines
    git add . && git commit -m "Changed another 2 lines in firstFile.txt in git_1"
    wsc+sh+zz


Transfer changes of commit from Step 7 only to git_2, using format patch. Commit: 'Apply patch'
    
    df3b616

    git format-patch -1 df3b616 && \
    git checkout git_2 && git am < 0001-Changed-2-lines-in-firstFile.txt-in-git_1.patch && \
    git add . && git commit -m "Apply patch"



Transfer changes of commit from Step 8 only to git_2, using cherrypick command.

    1dcd01f

    git checkout git_1 && git cherry-pick 1dcd01f
    git checkout git_2 && git cherry-pick 1dcd01f


git_2: Concatenate the last two commits ('Apply patch' and 'Changed another 2 lines in firstFile.txt in git_1') using reset + commit commands.
    git reset --soft HEAD~2 && git commit


git_2: Change author and message of the last commit and add non-empty thirdFile.txt file to it. Message - 'Concatenated two commits', author - Ivan Ivanovich <Ivan_Ivanovich>
    git commit --amend + message edit and save
    'Concatenated two commits', author - Ivan Ivanovich <Ivan_Ivanovich>


git_2: Create a new commit that reverts changes of the last one. Leave the default message - 'Revert "Concatenated two commits"'
    git revert HEAD
    git commit -m "Revert 'Concatenated two commits'


git_2: Create and commit thirdFile.txt file. Message - 'Added thirdFile.txt to git_2'
    touch thirdFile.txt && git add . && git commit -m "Added thirdFile.txt to git_2"


git_2: Run command that removes all changes of the last two commits. You will end up with commit - 'Concatenated two commits'
    git reset --hard HEAD~2


Synchronize git_1 and git_2 with a remote repository.


        -   -   -   -
-   -   -    DONE   -   -   -
        -   -   -   -





Part 2

For this task you should learn how to use interactive rebase, thus other ways of achieving the same are prohibited.

Create git_3 branch from git_task. Checkout to git_3.
    git checkout git_task && git checkout -b git_3


Add new empty file doubtingFile.txt and commit it with message - 'Added doubtingFile.txt to git_3'.
    touch doubtingFile.txt && git add . && git commit -m "Added doubtingFile.txt to git_3"
    

Add a line to a file and commit changes. Do it 5 times. You should end up with 5 lines in a file and 6 commits: 1 for creating an empty file and 5 for adding a line. Messages are the following: 'Added line 1', 'Added line 2' ...
    vim doubtingFile.txt
    Add a line to a file
    sh+zz
    git add . && git commit -m "Added line 1"

new line

    touch doubtingFile.txt
    vim doubtingFile.txt
    Add a line to a file
    sh+zz
    git add . && git commit -m "Added line 2"

    touch doubtingFile.txt
    vim doubtingFile.txt
    Add a line to a file
    sh+zz
    git add . && git commit -m "Added line 3"

    touch doubtingFile.txt
    vim doubtingFile.txt
    Add a line to a file
    sh+zz
    git add . && git commit -m "Added line 4"

    touch doubtingFile.txt
    vim doubtingFile.txt
    Add a line to a file
    sh+zz
    git add . && git commit -m "Added line 5"


Check your log and copy it somewhere.
    git log --oneline
    copy the output


Launch interactive rebase for 5 last commits, squash all the latest commits into the first one. 
Reword first commit. 
You should end up with 2 commits: 
    1 for creating an empty file (Added doubtingFile.txt to git_3) and 
    second for adding 5 lines. 
        Second commit should have a new commit message - 'Rebased commits'

        git rebase -i 546c6e8


Check your log and compare it with the previous one. Look at the hash, date, commit message. Explain what changed and why.
Check your reflog. Explain what you can see and why.

Synchronize git_3 with a remote repository.
    git push git_3

-   -   -


