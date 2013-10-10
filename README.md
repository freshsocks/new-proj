Git Commands
============

## Cloning to a new project

Suppose you always start from the same base app. This base app is maintained in a repo called "freshstart". Every project you start, you want it to start with the "freshstart" base app.

You also want you project to be linked to "freshstart", so that every time it is updated, your new project gets the updates to it's base app as well.

### Remotely create 

```
curl -u 'stevefloat:PASS' https://api.github.com/user/repos -d '{"name":"new-proj"}'
```

### Start a new repo

```
curl -u 'stevefloat:PASS' https://api.github.com/user/repos -d '{"name":"new-proj"}'
cd ~/git
git init new-proj
cd new-proj
git remote add origin https://github.com/stevefloat/new-proj
git remote add base https://github.com/stevefloat/freshstart
git add .
git commit -a -m "setup"
git pull --rebase base master
git push origin master

```

```
git config --global core.mergeoptions --no-edit
```

### Set 

```
git remote set-url origin --push --add user1@repo1
git remote set-url origin --push --add user2@repo2
git remote -v show
```
```
git remote update
```


### Clone into specific folder

```
git clone https://github.com/stevefloat/freshstart new-proj
```
-or-
```
git clone git://github.com/stevefloat/freshstart.git new-proj
```


git remote add upstream https://github.com/stevefloat/freshstart


## References

* [git pull --rebase](http://viget.com/extend/only-you-can-prevent-git-merge-commits) Used to prevent the prompt for a commit message when merging using git pull, and also apparently makes a more readable commit history.

* [curl command for creating new repo](http://stackoverflow.com/questions/2423777/is-it-possible-to-create-a-remote-repo-on-github-from-the-cli-without-ssh) so that you can init a new repo from CLI

* [commands for setting a remote repo](http://stackoverflow.com/questions/849308/pull-push-from-multiple-remote-locations)

* [solution to suppressing git-merge commit message prompt](http://stackoverflow.com/questions/12752288/git-merge-doesnt-use-default-merge-message-opens-editor-with-default-message/12752379#12752379) that I wasn't able to get working. I ended up using the ```git pull --rebase <repo> <branch>``` command to suppress the prompt, although there might be other implications that are messing with my commits & pushes that I haven't figured out yet.

* [more info on --rebase](http://gitready.com/intermediate/2009/01/31/intro-to-rebase.html) that could be helpful.


TODO
====

* Still trying to get the synchronizing commits from the base app working properly...

```
git pull --rebase base master
git remote update
# I have no idea what this does >_<
git commit -a -m "updated README.md"
git push origin master
```

Still getting the same error.

>
```
To https://github.com/stevefloat/new-proj
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/stevefloat/new-proj'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

Errrg.... I think it might be the --rebase command.

**deleting repo & local copy. Lets try again....**


```
curl -u 'stevefloat:PASS' https://api.github.com/user/repos -d '{"name":"new-proj"}'
cd ~/git
git init new-proj
cd new-proj
git remote add origin https://github.com/stevefloat/new-proj
git remote add base https://github.com/stevefloat/freshstart
git config --global core.mergeoptions --no-edit
git add .
git commit -a -m "setup"
git pull base master
git push origin master

```

> No ```--rebase``` this time.

This time, it did work. No prompt, set up everything correctly.

I was able to make a commit to the base app _freshstart_, pull it into the _new-proj_ app, and then push the changes to the new-proj master branch. **SUCCESS**!

The only problem is that I wasn't able to pull the changes from _freshstart_ without getting the damn prompt again.

I edited the ```.git/config``` file directly to reflect the --no-edit config option.
```
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
	ignorecase = true
	precomposeunicode = false
	mergeoptions = --no-edit
```
For some reason, ```git config --global core.mergeoptions --no-edit``` isn't actually modifying the config file like its supposed to.

After trying another push/pull, I **STILL** got prompted for a commit message when I ```git pull base master```

Finally, I could only get it working using the ```--no-edit``` flag on the git pull. So, like this:
```
git pull --no-edit base master
```

I don't like having to add that flag. 