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



