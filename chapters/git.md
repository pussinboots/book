#Github

##Git shortcuts

###for Play apps
Put the following line into your .profile file.
\begin{codelisting}
\codecaption{alias for git.}
\label{code:alias}
```bash
gitpushtesteddetail() { git pull && play test && git add -i && git commit && git push; }
gitpushcompletetesteddetail() { git pull && play test && npm test && git add -i && git commit && git push; }

alias gp=gitpushtesteddetail
alias gpt=gitpushcompletetesteddetail
```
\end{codelisting}

And then you can call
\begin{codelisting}
\codecaption{shortcut command for push}
\label{code:alias}
```bash
gp
```
\end{codelisting}
* git pull is performed to get all possible changes
* play test is performed and if it fails than nothing will be commit. If it succeed than step 2
* git add -i
* git commit
* git push

```bash
gpt
```
* git pull is performed to get all possible changes
* play test is performed and if it fails than nothing will be commit. If it succeed than step 2
* npm test is performed and if it fails than nothing will be commit. If it succeed than step 3
* git add -i
* git commit
* git push

Don't use git commit -am that commit in most case to much and the comments are also not detailed enough.

###javascript apps