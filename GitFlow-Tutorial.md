* Branch off develop
```
	git checkout -b feature/foo
	git push -u origin feature/foo
```
* Work
```
	git commit
	git push
```
* Rebase
```
	git rebase -i develop
	git push -f
```
* PR
```	
	git pull-request -b develop
```

* Feedback

* Fix
```
	git commit
	git push
```

* Rebase
```
	git rebase -i develop
	git push -f
```

* Merge

```
	Merge Pull Request
	Delete branch
```
Never force push
never force push shared history
never force push shared history without talking about it

* Get you  team's changes in, then:

```
git reset --hard origin/branch
```
* Why Pull Request?

1. Good mechanizm for code reviews 
2. Learning, Teaching, Sharing 
	a. more consisten code
	b. more maintainable code
	c. more discussion to change your mind
3. Bug finding

* What makes Better PUll Requests

1. Implement one feature or fix one bug
2. Include < 200 LoC
3. Do not (directly) include dependencies
4. Merge in cleanly
5. Have high signal to noise


* rebase from feature
```
git rebase -i feature/foo
git push -f
```
*PR in to feature
```
git pull-request -b feature/foo
```
*eventually
```
git checkout feature/foo
git rebase oi develop
git push -f
```

*How to fix when accidentally merged develop to master
what we can do is reset master back to 94523a1, which is when the 404 fix got merged in

[2:21]  
then make a new PR for the header change

Bin Liu [2:21 PM] 
ok

[2:21]  
How do I reset master?

[2:21]  
...

Matt Tingen [2:21 PM] 
1 sec

Bin Liu [2:22 PM] 
ok

Matt Tingen [2:23 PM] 
first, `git checkout master`

[2:24]  
and `git pull` to make sure you're matching what's on github

Bin Liu [2:24 PM] 
yep

Matt Tingen [2:24 PM] 
then `git reset --hard 94523a1` to point the head at the correct commit

[2:25]  
now, if you do `git status` it will say you're behind origin, which is what we want

Bin Liu [2:25 PM] 
yes

[2:25]  
your branch is behind ‘origin/master’ by 24 commits

Matt Tingen [2:27 PM] 
the you can `git push -f` to push with a force. the force is required since it will rewrite history

Bin Liu [2:27 PM] 
yep

[2:28]  
now we are back to before I create the PR, right?

Matt Tingen [2:29 PM] 
Yep, and the header change is a new change, not a hotfix so we don't need to merge it in yet

Bin Liu [2:29 PM] 
but the header change is merged before i merged 404 change

[2:30]  
does it mean i should cherry pick?

Matt Tingen [2:30 PM] 
ah, i see. yeah the header change is still in master

Bin Liu [2:30 PM] 
yes...

Matt Tingen [2:31 PM] 
sorry, i didn't realize that

Bin Liu [2:31 PM] 
no problem, I saw James merged this morning, and told him to hold off any further merge,

[2:31]  
so what you suggest we do?

Matt Tingen [2:33 PM] 
Normally, I would say we should remove the change from develop, but that change is very small and has already passed QA

[2:33]  
so I think it would be okay in this case to include it in the release

Bin Liu [2:33 PM] 
OK.

[2:33]  
so I will create a PR from develop to master now

Matt Tingen [2:34 PM] 
I'm not sure it's necessary

[2:34]  
at this point, they match, so there's nothing to merge

Bin Liu [2:34 PM] 
yeah.. i was creating PR and saw nothing to pull...

[2:35]  
OK.

Matt Tingen [2:35 PM] 
so you'll need to verify that stage has the correct version

Bin Liu [2:35 PM] 
yep i m doing it now

[2:38]  
heroku is a6b1647, but github master latest commit is 94523a1

[2:39]  
heroku pick up the version of my revert of revert PR..

Matt Tingen [2:39 PM] 
I think since we modified history, heroku didn't pick up the change.

[2:40]  
So we need to tell heroku to make a build. If you click on the title "wta-stage" and then go to the deploy tab, there's a button at the bottom "Deploy Branch". That will manually run a new build. Do that for wta-stage-dev, as well.

Bin Liu [2:40 PM] 
Ok , just click that deploy branch button, right?

Matt Tingen [2:41 PM] 
yeah

Bin Liu [2:41 PM] 
yep did both

[2:42]  
heroku is biulding now

[2:42]  
i will verify the version match github once it is done

Matt Tingen [2:42 PM] 
Cool, we need to make sure TeamCity is correct, too

[2:42]  
for the automation tests

Bin Liu [2:42 PM] 
is TeamCity auto kicked off? if we kick off heroku build?

Matt Tingen [2:42 PM] 
nope, they're independent

[2:43]  
they both watch for changes on the `master` branch

Bin Liu [2:43 PM] 
I see

Matt Tingen [2:43 PM] 
but I suspect rewriting history confuses them

Bin Liu [2:43 PM] 
i am openning teamcity

[2:43]  
i guess there is a button i should push to start the test

Matt Tingen [2:44 PM] 
I'm trying to figure out if it says anywhere which version it ran the tests against

[2:46]  
Hmm, I'm not too sure. TeamCity is still a bit of a mystery to me. We can go ahead and run it either way

[2:47]  
Just click the "Run" button on "Automation Test - Release Builds"

Bin Liu [2:48 PM] 
seems i cannot open team city

[2:48]  
do I need a VPN for that?

Matt Tingen [2:48 PM] 
yeah

[2:48]  
I'll kick off the run

Bin Liu [2:48 PM] 
Thank you so much!

Matt Tingen [2:53 PM] 
no problem

Bin Liu [2:54 PM] 
One basic question, how do I see in github, the long list of commits with all the versions?

Matt Tingen [2:54 PM] 
i want to make sure you understand that doing force pushes, especially on master, is a special case; not something we'd normally do

Bin Liu [2:54 PM] 
Yes. i assume anything force /reset is not a normal operation...

Matt Tingen [2:54 PM] 
awesome

[2:54]  
near the top left it says "1,127 commits"

[2:55]  
click on that and it will list the commits for that branch

Bin Liu [2:55 PM] 
Awesome! See them! Thanks! :slightly_smiling_face:

Matt Tingen [2:55 PM] 
you can also `git log` or `git log --oneline`, but i usually find github easier to use

Bin Liu [2:56 PM] 
I will wait until TeamCity test passed and tell Amanda it is ready to test , i saw you kicked off the test

[2:56]  
Thanks! I will need to write them down so that i will remember next time!

Matt Tingen [2:57 PM] 
it's going to be quite a while before teamcity runs the tests. we're short on testing agents


