#Git For Newbies ( Skip if you are not!)
##What the Hell is Pull Request?
A Pull Request is eligible to born when you have more than two branches. 
And Most common practise is you always create a branch to work on your stuff, when you think it is good enough, issue a PULL REQUEST from your branch , saying "Hey! Master, I have something that I want to merge into the tunck(for SVN usersm, master is the trunk)"
##How to Create a Pull Request?
I went through a lot of 'WTH is that? ' and 'Ah, here it is' phase before I got this happend. Now I am going to write it down so that I will save myself some time next time I need to do this. 

1, Clone an existing repo

`
using SSH : git clone git@github.com:<GIT_NAME>.git
using HTTPS : git clone https://github.com/<GITNAME>.git
`

The Git Name part you can find it from clone or download part on the git repo website


2, Generate ssh-key for a private repo ( You have to have it to push to remote) 
if it is a pulic repo, you don't need it.


`ssh-keygen -t rsa -C "YOUREMAIL@EMAILHODLER.com"
 $eval "$(ssh-agent -s)"
 ssh-add ~/.ssh/id-rsa
 pbcopy <~/.ssh/id-rsa.pub
 ssh -T git@
 `
 Then go to your github web, Add SSH key


 3,Remote origin
 
 `
 git remote
 git remote -v
 git remote add origin <remote link-- same as git clone .git link>
 git remote remove origin
 git remote add another_remote_any_name <...>
 ` 

 You can have mulitpl remote for one repo

 4, branch & commit


 `
 git branch
 git branch -v
 git checkout -b <branch-name>  // create a branch <branch_name> locally
 git push --set-upstream origin <branch-name> //push local branch to remote
 `

 //AFTER YOU DID WHAT YOU DID CODING

 `
 git commit -m "my commit message" // commit to local 
 git push // push to remote
 `

 5, create pull request

 
 
 Go to github website, select your new branch, follow the step, it is pretty intuitive! :)




 6, FLOWs of branching and issuing pull request
 git clone ...
 git checkout <branch> ( develop <--)
 git pull
 git checkout -b <my_local_branch_name>
 git push  -u origin <my_local_branch_name>

 Then go to github repo website, issue pull request. 
 make sure the number of commits matches your local commits number. 

 7, after code review, we should rebase multiple commits into one before merge to the trunk

 git log ---> check log
 git rebase -i HEAD~2    -----> clappse the first /latest two comments
 keep the first one pick , squash all others below it  -- although they are newest/newer comment
 
8, How to abandon unwanted changes
git clean -df
git checkout -- .

9, What happen when you checkout a branch but have some unchecked in changes, but you are not ready to abandon them?

git stash -u

then git checkout <newbranch>

when done, switch to your current branch and do 

git stash pop

10, About "rebase"

git rebase develop  --- rebase current branch to develop branch
git rebase master   --- rebase develop branch to master        

NOTE:: your master or develop are your local develop and master. to really make you remote branch base to the updated develop and master, 
you need to git checkout develop or git checkout master first, and do git pull, and then do the rebase. 

then after rebase, did a git push -f , 

then go to github, change your PR from compare to develop to compare to master, verify the PR change is consistant with it when you are vs develop( since you already rebased, there shouldn't
be any older changes...)

otherwise, STOP here and understand what is going wrong. 

11, sourceTree is a good GUI interface for git control
12 git --help is very helpful
13 git log --graph --oneline  will print out similar tree /picture sourcetree will give you
 

