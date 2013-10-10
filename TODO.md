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

I don't like having to add that flag. I'm going to restart my computer and see if anything changes. She's been through a lot today.