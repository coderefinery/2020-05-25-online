---
permalink: /hackmd-day1/
---


# CodeRefinery 25.may-4.jun


## Arrival

* Open this HackMD: (removed)
* Do you need software installation help?  Ask us.
* Rename yourself to include your breakout room number: e.g. (1) or (1,H).  Check email.
* Let us know how it's going.  Any initial thoughts?

## How to use this

* Always write new content/questions at the very bottom
* You can answer, comment, and revise other things, though.
* Be respectful and helpful. By participating in any CodeRefinery workshop series, participants accept to abide by [CodeRefinery's Code of Conduct](https://docs.carpentries.org/topic_folders/policies/code-of-conduct.html).

## Introduction session

Moved to (removed)

## git-intro

### What kind of problems do you anticipate when version control is making a zip file with a date?
* No comment about what, why, was changed and who made the change...
* Too confusing to manage. Also takes up lot of space.
* Dates (D/M) or (M/D) format confusion
* Ancestry is not visible
* Files get "lost"
* Conflict with other's work. Maybe do overlapping work at same time.
* Dots can create a problem being mistaken for file extensions
* Don't know what are the changes introduces in every version.
* My code has never been Final, even if I wanted it to be.
* Difficult to track edits.
* WWW
* What happens if something has to be changed after the "Final" version?
* Don't know what is where.
* no back-up
* Conflicting versions
* History is lost
* What was the reason for a snapshot?
* Difficult to merge parts from different versions
* dates are not sortable


### Motivation

- What about other version control systems?  Do you use them often?
  - I sometimes use [RCS](https://en.wikipedia.org/wiki/Revision_Control_System) as part of managing an HPC cluster, it's popular among system administrators because it's rather simple and convenient for managing e.g. single config files, but it's not very powerful
- Could you quickly explain branching?
  - branches are for managing parallel tracks of work. You create a new branch, switch to it, do some work. The branch can then be merged into the main branch, or discarded. We will cover branches in detail later
- How version control softwares manages a lot of changes? I've been thinking on version data that it is big but at the same time changes a lot. Do you think this could affect the performance of the version control software? What other alternatives do I have?
	- [Some experience from Microsoft about this ("The Probably Largest git Repo on the Planet")](https://devblogs.microsoft.com/bharry/the-largest-git-repo-on-the-planet/)
	- Git and others are used for large projects with many changes.  About version control for large data specifically, there are some add-ons strategies for data (git-lfs, git-annex).
	- There is also https://dvc.org/ but I haven't tried it yet.

- I tend to commit 2-10 times a day, is that too many commits. I do not konw "right" moment when to commit.
	- Not at all, in general the more the better as long as it helps you.
	- To add on this, we will see later (when using branches and pull requests) that it does not really matter how many commits you do. So as answered before: do as many as you need.
	- Too many is better than too few. You can always combine commits later but splitting commits is more work.
- I missed how to get to annotations...
	- Within Github, there is a "blame" button when viewing a specific file.  From command line, `git annotate`.  we'll go into details later.
- What's the difference between Github and Gitlab? Can we use Gitlab and Github simultaneously?
  - git is the command line program/repository format.  Github and Gitlab are hosting services with nice interfaces.  One repository (git) can be connected to either of them (or both at the same time, or neither, or other things).
  - yes you can use as many different online repository hosting platforms as you like! they're different companies offering more or less the same services
  - some projects keep public master branch on GitHub and unpublished private branches on GitLab or somewhere else
  - GitHub was recently bought by Microsoft, and afterwards GitLab got more traction. Microsoft has a traditionally bad relationship with the Open Source Community.
	- For what it's worth this has changed in last years where MS open sourced many of their projects and also recently admitted that being against open source in the 90ies was a mistake.
	- Since it has been bought, many new features have been offered and added for Open Source Community.
	- What we teach can be used with GitLab, bitbucket, etc. So if MS changes its strategy, Open Source projects can move their repositories.
  - While there is no lock-in in terms of Git itself (we will see that it is very little effort to move a repository between providers), moving issues and discussions (pull requests, merge requests) and testing pipelines is more work so there is some lock-in aspect to the latter.
- How to transfer repositories between Gitlab and GitHub?
  - Both are GIT repositories, therefore you can download from one and push it to the other.
  - We will also practice this on Wednesday.
  - I do this in my daily life. I have two remotes configured on my  repo, and can push and pull to/from either.  We will see later this week.

- Could you talk about using git with Mathematica?
	- well, i've read several discussion on stackexchange that git doesn't work well with mathematica notebooks because they contain code + meta+ lots of other things. And then there is a million of suggestions (remove history, etc) but then it sounds quite cumbersome. is there an easy streamlined process?
		- Ah, I read it as "math", not "mathematica".  Certain formats have auto-generated and changing data, so differences aren't so meaningful.  Still, sometimes I track data like that, it's not perfect but better than nothing.
- I didn'quite understand how git is distributed version control in contrast to centralized version control.
	- This will become more clear later in this lesson and this week!
	- It is distributed in the sense that each contributer has their own *complete* copy of the repository and can make their changes independently.
	- There is no main repository e.g. you can have as many as you want (distributed). It willl become clearer later.
- I created git account as Local, as I am not using GitHub othewise and my account in Aalto utilizes version.aalto.fi. Was creating name and email with switch -local the correct way?
- `git config --local user.name "Firstname Lastname"`
  `git config --local user.email "myemail@example.com"'`
  `git config --global core.editor emacs'`
	- What you did made the settings apply to the current repository. You did not create an account by changing these settings. This just means that whatever actions you do in this git repository, they will be performed under this name and this email. If you would have used `--global`, then all repositories on your local machine would use this name and email. Using `--local` just applies them to the repository you are currently in.
	- I'm not entirely sure what this means, but it will probably be OK.

- Are we supposed to type along now?
	- yes

- How sensitive is git usually between different versions? Should all team members have about the same git version?
	- The version itself is typically not very important.
	- Some commands like `git switch` (to switch between branches more intuitively) are available only in more recent versions, but actual repo is always compatible.

- How do you get your command prompt to display your branch?
	- https://github.com/jimeh/git-aware-prompt
	- Stefan uses the `zsh` shell with https://github.com/ohmyzsh/ohmyzsh and a modifier https://github.com/denysdovhan/spaceship-prompt

***Please focus on the type-along!***

- onion is missing in ingredients!
	- That's obviously a bug... So we will have to fix the bug later!

- Are there any guidelines on how to phrase and format a commit message?
  - You can check this out: https://chris.beams.io/posts/git-commit/
  - we will also discuss this later
  - convention is one line summarizing the commit, then one empty line, then more context in free form
  - it's good to write why was something done, not only what was done (the latter I can inspect with git diff/show)

- help not working: "(base) C:\Users\mle\coderefinery\recipe3>git help commit
  fatal: 'C:/Users/mle/Anaconda3/Library/mingw64/share/doc/git-doc': not a documentation directory.
	- I guess the help stuff isn't installed. I can test it on Windows10+GitBash, if you want to chat about this, find me in the contacts (CR, (name removed))

- I have deleted my file without using the `git rm` command and everytime I execute `git status` I can see it red. My question is how to compeletly remove it from git folder?
  - if you've already removed the file with `rm`, you can still do a `git rm <file>` to add that removal to the staging area.  The staged change will then be the removal of the file.
  - use `git rm <file>`
  - What's the difference between doing `git rm` ("or git mv") versus just doing `rm` or `mv` and then `git add`?
	- `git rm|mv|...` does the `mv|rm` and `git add` in one step.

- Also, what does oneline command does?
  - `git log --oneline` shows a simpler history with only one line per commit. Try it out and compare it to `git log`
- Link to the previous exercise description please?
	- https://coderefinery.github.io/git-intro/02-basics/#exercise-record-changes
-  omitting the `-m` command in `git commit`, git sent me into vim and I prefer Nano.
	- `git config --global core.editor nano`
	- https://coderefinery.github.io/installation/git/#configuring-git

- One in my team did not get anything on `git diff` after changes was made: does normally diff need to be configured?
	- It shouldn't need to.  Maybe files weren't added, maybe they were added and already committed. `git diff` by default only looks at already tracked files,  that are not committed yet.
	- I think it was already committed to, so we'll check it in next session. Thanks.

- Do sub directories inherit `.gitignore` from upper level?
	- yes

- In `.gitignore`, are directories denoted with double underscore?
	- no, this was a python specific folder which contained double underscores
	- you can denote directories by their name, without extra annotation

- Why to have a `.gitignore` and just not add it to your changes? `.gitignore` is for not considering files, but why not just ignore them on the way?
  - You really want `git status` to not have any extraneous output - a clean status output is the way to know that you've taken care of everything you need to.
  - everything you add to `.gitignore` becomes invisible to `git status`, i.e. it gives you more tidy output
  - you mean why was `.gitignore` staged and committed? because you don't want to see it when you do `git status`, and you also want all your collaborators to have the same git experience (or yourself on different computers)
  - generated/compiled files are typically not tracked as part of the repository
  - To make sure these files are never added even by mistakes

- Can commit hashes collide?
	- It is designed so they won't (sha1 hashes, if these could collide it would break a lot of stuff!).  Search "(sha1) hash collision" for details
	- It's good to know that two versions with the same hash not only correspond to the same code/project state, but also share the same history. If you change the history (in Git it is possible), all "future" hashes will also change.

- Can there be several `.gitignore` files in one repo?
	- Yes, you can have one per directory but often repositories have only one or very few such files.
	- They affect everything "below" that folder
	- To get a good understanding of what might change I'd suggest `tree .` (macOS, Linux) in the directory, which will show you the directories and files in a hierarchy

- What is the website that generates .gitignore for a particular programming language/editor?
	 - https://gitignore.io

### 04-staging area

- even the 1st example is better than Example 3 and 4;
  - 4 is often how I actually work/commit (too many commits better than too few) but I later combine/split/move commits and try to end up in 2 or 1.

- would you recommend adding permalinks to specific lines of code in commit messages?
	- Great point; normally this is not recommended; web interfaces like Github will show the changes in a way which will let you navigate to the changes; and ditto with the terminal interfaces. It is a good thing to keep in mind, but the solution tends to have many small commits instead of one commit for a major (large) change.
	- but if I understood the question correctly: if you want to refer to a code section which is not part of this commit and want to make sure that that code section does not "move", then I would do this.

- `-p` is short for `--patch`

- What is the difference between `git commit` and `git commit -p`?
  - With `git commit -p` or `git add -p` you can commit or stage partial changes. I use it when I modified different things in the same file but I want to stage/commit them separately.

- Can you fix commit message? As it happened with 1 vs 2 cloves of garlic example?
	- You can with `git commit --amend`.  I often do this to fix things, but you should do it only immediately after (before pushing).  Anything else `add`ed will get added to the commit, too.  This rewrites history, which we'll comment on later.

- Say you find a bug. Is it a good idea to record it separately in one commit and then record the fix in a different commit? Or do all at once(if possible)? In general, is it a good idea to keep history of bugs?
  - Normally there is not a separate commit to "record the bug" - there is no changed code to record.  You would normally make an issue in the issue tracker about it.
  - but the bug is then already probably committed
	  - Is it possible to make an "empty" commit? like add an empty line, just to record the bug
		  - It is technically possible, but not a common practice.  Normally a bug would be tracked in another issue.
	  - it is possible but a better solution might be: you open an issue on GitHub/GitLab when you discover the bug, you describe it there. Later you or somebody else can reference that issue in the commit that fixes the bug and both the issue and the commit end up cross-referenced (we will practice this next week).
  - very good idea to commit the bugfix as separate commit (not mixed in with other stuff) so that others (or you on a different branch) can take that one commit to a different branch (`git cherry-pick`)

- Does `git rm` remove file from all locations (computer, staging area, committed area and git-server)?
	- It only removes from the current branch on the current repository, but adds a commit "this file has been removed".
	- Actually, `git rm` stages the removal first. Then the file is removed as you do the commit. As you push and pull that commit around, it gets removed from the other copies.  We'll do this later this week. Note, that `git rm` do not remove the file(s) from history. It is only remove from "now on". If you check out a commit from before the the `git rm` you will find the file is still there.

Exercise: staging area

https://coderefinery.github.io/git-intro/04-staging-area/#exercise-using-the-staging-area

- so is the `git reset` for unstageing from uncommitted changes (edits / additions) and `git checkout` for already commited changes?
	- This always confuses me, too
	- Check the picture here: https://coderefinery.github.io/git-intro/04-staging-area/#staging-area-commands
	- `git reset` makes the staging area look like the last commit (so undoes a `git add`).  `git checkout` changes working directory files to the older (staged) version.  I used to always check before using either, sometimes I still do.
	- `git reset` can be used to unstage, it can also be used to remove commits and remove changes (`git reset --hard`) or remove commits while keeping changes (`git reset --soft`)
	- `git checkout` can be used to update the working tree and to undo unstaged/uncommitted changes by overwriting your working path with the staged/committed version. It can also be used to switch between branches (it then updates your working tree with the version from a branch). I "imagine" `git checkout` as (please go into `.git`, find a specific version and put this version into my working tree).

### 05-undoing

- Is (use `git restore --staged <file>...` to unstage) an alternative to git checkout?
  - It's a newer command (so we don't teach it by default).  It seems the exact command you put there is the same as `git reset`. `git restore <file>` seems the same as `git checkout <file>`.
  - Sorry I misunderstood the question - now I understand. In more recent Git I recommend indeed to use this instead of `git checkout` since `git restore` is more descriptive/intuitive.

- `git commit -v` is handy for seeing what is actually being committed
  - I use this a lot to see the variables which I changed etc. while editing the commit message.
  - I use an alias `ci` = `commit -v` to use this by default.

- If you change the commit message again to its original, will it recover the original hash?
	- No! since the date has changed. The hash is created from the author name, actual change, date, .... So even one bit change will change the hash.

- `git commit --amend` changes the HEAD, what if we want to change an older than HEAD commit?
	- Search "git interactive rebase"
	- This can be done with an interactive rebase: `git rebase -i [some hash before the one you want to change]`. In an interactive rebase you can modify commits, combine them, reorder them, remove them. You can also modify commit messages.
	- Interactive rebase changes hashes so I can do that on my local changes but I would be careful changing history for commits that others depend on because I have already shared them (we will discuss this tomorrow).

- Can we see what `git revert` will do before this is commited?
	- If you `git revert <hash>`, you can `git show <hash>` to see that change - what happens will be the opposite.
	- I don't know a way to see the final outcome in advance, but what I would do is make sure everything else is committed, do the revert, see, and then undo it with `git reset --hard` if I don't like it.  This is introduced later.

- I'm not getting what exactly what `git revert` do? what if you are reverting an insertion of something that was already deleted, for example: commit.1: add line 1, commit.2: delete line 1, revert commit.1?
  - `git revert` is to apply a new commit which applies the opposite of the commit I am reverting. In your example this will not be possible and Git will issue a conflict and stop and tell me that I am about to revert something which disappeared/changed later. We will discuss conflict resolution tomorrow when merging branches.

- What is the difference between `git checkout` and `git reset HEAD`?
	- `git checkout [filepath]` will undo unstaged modification of my file and basically bring my file to the state that I have staged or committed.
	- `git reset HEAD` does not modify my working tree but it unstages these changes.

- What does `HEAD` mean in git instructions?
	- "The most recent commit/version on the current branch", basically the "last commit you made" or "place where you'll add new commits".
	- so is it something I need to write in the terminal, or substitute it with some path?
		- It's a placeholder on command line when needed.
		- For now, I wouldn't worry and use it when it's listed as part of a command, in a day or two it will become clear.

- How to solve a conflict when attempting a revert?
	```
	-- On branch master
	You are currently reverting commit 6ae2117.
	  (fix conflicts and run "git revert --continue")
	  (use "git revert --abort" to cancel the revert operation)

	-- Unmerged paths:
	  (use "git restore --staged <file>..." to unstage)
	  (use "git add <file>..." to mark resolution)
		both modified:   file
	```
  - We will discuss conflict resolution next time.

- What if I want to use git but my collaborators prefer Dropbox, etc. Is there a good way to combine different methods of version control?
  - If your colleagues prefer Subversion (SVN), you can use `git svn` so that it looks like Git on your side but you talk to a SVN server.
  - If your colleague resists and prefers emails, create a branch for them on your side (we will talk about branches tomorrow) and every time you get a new version by email, commit it on your side and then you can compare and merge and rebase and do all the Git things.
	- I've done this many times...

- After staging the changes, what happens if you add one new change, not stage, and checkout?
	- The `git checkout <file>` will change you back to the staged version.

- I usually store my files on Dropbox instead of the hard drive. Could this cause any problems? Is it better to just use git in this case or git+github?
	- I think that in theory, it should work,  In practice, dropbox will also be synchronizing all the `.git/` files, and I would not be surprised if there's a problem someday.
	- I have tried this many years ago (sharing `.git` via Dropbox), it seemed to work first but it brought us strange effects since the synchronization is then different than how we would do it with Git.
	- GitHub and GitLab just add so many awesome features, that they're absolutely worth it!
	- It might **break** everything if you accidentially commit at the same time.
	- The thing is that I don't just have code. I usually have compiled, not compiled stuff. + data that I might not want to store on my harddrive for space reasons. So not sure if it is optimal to switch between Dropbox and hardrive.
		- I usually recommend to people to organize there files in to types: "source code and small data", "compiled and auto-generated outputs", "larger data", etc.  source code in git, compiled and auto-generated stuff is ignored, larger data moved as needed (or use git-annex/git-lfs if you want).

- Do commit messages pick up markdown formatting?
  - Thas is a feature of Github/Gitlab/etc, git itself just stores the text and it's up to the viewer to parse it as something.
  - It nevertheless makes sense to use markdown for formatting, as it is _very_ widely used.  And is basically the same as normal text.
  - GitHub and GitLab will also pick something like `#xxx` or `Fix #xxx` and redirect `xxx` to an issue or pull request. You can also refer to a repo/commit/GitHub user by using some specfic syntax. See [Github Help](https://help.github.com/en/github/writing-on-github/autolinked-references-and-urls) for more info. GitLab works the same way

- I dont find git graph ?
  - this was an alias (shortcut) and we will define it tomorrow for the branching episode
  - https://coderefinery.github.io/git-intro/06-branches/#a-useful-alias
  - I think it is also defined in the lesson quick reference
	- where is that quick reference?
	-  thanks found it ... https://coderefinery.github.io/git-intro/reference/ (link is on top of the lesson page)


## Feedback, day 1

what went well and what should we change/improve?

- Great on answering the questions in this document! +1! Supergreat!
- Good pace, very clear examples, break-out room time was relatively short, but size of members in break-out room is good.
- Organised and balanced between type-along and discussion, the only negative was that our heper was getting kicked out of the sessions. Otherwise superhappy.
- (from zoom chat) breakout room sessions could be longer
- Please consider having a more gender-balanced and otherwise more diverse faculty next time :) +1(if viable)
  - Very important suggestion. (Radovan) I would really like that. We try and we need to try better and I hope we can convince more persons to join as instructors to be better balanced and diverse. It is a problem.
- Do you think it would be possible to have the breaks with a few random breakout rooms, to have some informal chatting like in a physical workshop?
	- We thought about that, and having a randomly assigned "icebreaker time" at the start, but thought that for the first time, it might be a bit too much to manage.  (since our existing breakout rooms have to be manually managed, adding random rooms means we have to set them up again)
		- Would be super nice! But was ok the 1st day without ;-)
