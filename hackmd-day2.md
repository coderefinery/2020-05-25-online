

# Day 2

## git-intro

### Branches and merging

https://coderefinery.github.io/git-intro/06-branches/

- Is it better to use “git switch”?
    - `git switch` works with the newer version of Git.
    - We just don't teach it yet, because it's new enough it would cause confusion when it doesn't work for some people.
    - But if it is available on your version, I recommend to use it since there is less ambiguity than `git checkout` (which can do many different things).
- can you show more than just the last command
    - C-b ESC `<down>` should increase the top one by five lines
- can you again explain quickly what git graph does
    - It shows the full "commit graph", how each commit relates to each other.  Also the branches.  It is very useful as a "overall summary" of your latest commits
- When I have unstaged changes at master and switching to master branch via `git checkout master`, will the unstaged changes be lost?-
    - It never loses changes (as far as I see).  It will first try to move the changes to the new branch.  If that doesn't work, it shows a message saying "can't change branches with uncommited changes" or similar.
        - When this happens, I ues `git stash` before to save changes, , do the switch, and then `git stash pop` to get it back.  Don't worry about this yet, though

- The output of my git command show in refreshed clean window , instead of show right after the command line. Is there a way to change this?
  - This can be changed by changing the "pager" (see below)
  - Which operating system are you using?
      * I use macOS with iterm2
  - A quick workaround is to pipe it to `cat`, e.g. `git show hash1 | cat`
  - `git --no-pager log` stops the pager, too.
    * this works for me, thanks!

- What does the git do with the different versions of files in different branches? Are they stored separately or only their differences?
    - Git does not store differences but actual snapshot. But it does it very efficiently by chopping up files into portions, storing them in a tree structure and reusing common parts. When you run a `git diff`, the differences are actually computed on the fly, they are not stored. This storage format works less well for large binary files.
    - This goes into a bit more detail: https://coderefinery.github.io/git-intro/13-under-the-hood/

- What is the difference between git graph and git log --oneline? Does it matter which one to use?
    - graph has `--decorate` (show branches and tags) and `--all` (show other branches) and `--graph` (show how the commits connect), too.  `graph` is just an alias we define, so you can use what you'd like.
    - you will see the difference once we have more branches and tags

- If I committed to the wrong branch, can I easily move the commit to the correct branch?
    - Yes, it's "easy" but requires some care.  See below.  I recommend using `git graph` between every stage, to ensure you understand all the steps.  Then, it becomes natural.
    - I would do this (let's imagine I wanted to create `somebranch` but forgot and accidentally committed to master):
      - Create a branch referencing this new commit: `git branch somebranch` (now `somebranch` points to this commit)
      - Run `git graph` to verify that the new branch really points to that new commit.
      - Do a `git log` or `git graph` to find out to which hash you want to move `master` back, say the hash is `abc1234`
      - Make sure you are on `master`
      - Move `master` back to `abc1234`: `git reset --hard abc1234` (be careful, `git reset --hard` "throws away" commits but if you do this by mistake, you can recover from it with the help of `git reflog`)

- Why do we always need to "add" before "commit"? Is it ok to just "commit"?
    - It lets you check that you've added all the right things first.  You can use `git diff` and `git diff --staged` to make sure all the right things are about to be committed.
    - But you don't have to, there are several options that directly commit without adding (as long as it's added at least once)
    - You can also do directly `git commit filename(s)` but we recommend to do this in two steps since you can review your commit with `git status`

- If I clone a repo, why do I have to use git checkout branch_name to make the branch visible in git branch output?
  - We will clarify this later but after `git clone` you get all the remote branches, but `git branch` only shows you local branches (clone will create a local branch for you, typically `master`)
  - To see all branches, included remote branches, use `git branch --all`
  - `git checkout somebranch` will create a local branch referencing a remote branch `somebranch`, if the latter exists as a remote branch `origin/somebranch`

- When I change on some branch, eg less-salt, the changes are also visible in master. Does that make sense? Doesn't seem like clean separate branches for me...
    - It shouldn't, we should investigate in the breakout room.  What does `git graph` show?
    - It doesn't show my branch even though it's there. I can checkout to it.
    - We should look at this in a breakout room in a bit.  There are plenty of ways for stuff to get mixed up.
    - What is your breakout room number?
    - 14. So it seems before staging and commiting any changes on branches are "global". Only after staging there solely on the branch.

- "git branch" after the mergers still shows the other branches. So it is still possible to get back to those and rebranch?
  - you can jump back to a branch that has already been merged and keep working on it if you want. But normally you organize your work in feature branches which get deleted after merging. Sometimes though you want to merge the other way, e.g. from `master` to your feature branch (to keep up to date with the master branch). Then obviously you don't want to delete master

- I got merge conflict, are we going to discuss this? x2
  ```
  -Error/conflict: git merge less-salt
   Auto-merging ingredients.txt
   CONFLICT (content): Merge conflict in ingredients.txt
   Automatic merge failed; fix conflicts and then commit the result.    --- what to do?
   ```
    - Yes, soon.  If you get a merge conflict, you probably adjusted the same lines.  It's OK, there is a way to recover from this in the lesson.
    - Try to follow along as best as you can, and we'll

- please before merging a lot, could we discuss, what exactly happened with the files?
  - Git is able to automatically combine modifications done on two branches done in the same file, unless both branches modified the same code portion.
  - Then it creates a new commit, a merge commit.
  - If the same code portion has been modified differently on two branches, and we try to merge these, Git issues a "conflict" and we need to resolve it, we will see later how.
  - - THANK YOU!

- Merge operations can only happen between the master and a child branch?
  - Merge always modifies the current branch you are on but you can merge any other branch into the current branch.
  - We typically merge feature branches into `master` once the feature is done.
  - You sometimes want to merge `master` to the feature branch to update it with features/bugfixes done on other branches.

- Why are merged branches still visible when using "git branch"? (continued)
- The `git merge` does not delete the branch after merging. How can we delete it. Should we delete the branches?
  - they are not deleted automatically.
  - If you want to delete a branch after merging you have to do `git branch -d branch-name`

- Is `Gitk` any good for visualization? Do you use it?
  - Personally I use `git graph` and also I look at the "network" (via insights) on GitHub to browse branches.
  - Yes, it's good but for day to day work I find `git graph` more convenient.  Other things are nice for really complicated stuff.

- How does git select between the changed lines when merging? Child branch overrides the parent (experiment -> master)?
  - By default Git is very conservative and will not automatically select. If both modified the same code portion, Git stops and asks you to resolve the conflict.
  - If you are sure that you want to keep the one or the other without reviewing, you can instruct `git merge` to automatically follow the one or the other if it hits a conflict (example later in the session).

- What happens if I make add-pepper and add-chili branches, commit a change into the ingredients.txt so that '1 chil1' and '1 pepper' are on 'line 2' on both files since the files are different in different branches.  If I now merge them BOTH with the master, what happens?
  - The first merge will work (does not matter which branch)
  - But merging the second branch will issue a "conflict" where you need to decide whether to keep the chili or the pepper (we will later see how to resolve conflicts).

- So when I have git graph as following:
```
| * 2ae77cc (less-salt) reduce amount of salt
* |   e77e41a Merge branch 'experiment'
|\ \
| * | 86772b6 (experiment) reduced amount of cilantro to 1 tbsp
| * | 1686bed add cilantro to recipe
```
  And I say 'git show e77e41a', I do not see the changes caused by merge.
    - The merge commit doesn't introduce any actual changes itself, so that is probably why it shows nothing.

- What do the colours in git graph mean?
  - vertical lines: the colors are a visual aid to help you distinguish the different branches. Note that the asterisks symbolize commits

- What happens if I delete the last branch, or a branch that uniquely refers some commits? Are these commits then lost?
  - git will raise a warning if you try to delete an unmerged branch with `git branch -d`. If you're really really sure that you still want to delete it you can override the warning with `git branch -D`
```
git branch -d experiment less-salt
error: The branch 'less-salt' is not fully merged.
If you are sure you want to delete it, run 'git branch -D less-salt'.
Deleted branch experiment (was d78c499).
```
   - The merge probably has not worked somehow.  We should examine in breakout rooms.

- Can one undelete a deleted branch?
    - Yes, will tell more in a bit
    - If you remember the hash, you can recreate it with `git branch somename somehash`
    - If you forgot the hash, you can for some time find it using `git reflog`

- We had a conflict in our rebasing. I wanted to know how to open the conflict in the diff tool etc., like I usually do in VSCode. It would be nicer than deleting.
    - I think `git difftool` would do it.  But, I haven't done this too many times, so maybe someone else can comment

- If your breakout room had technical problems (no helper, not enough time, something else), please comment here so we can know the extent of the problems (and breakout room number):
    - I again kept getting kicked out. Although happened less serverely than yesterday, breakout room 10.
        - Can you try Zoom in Chrome?
            - I'll try from Chrome in the next break then.

### Branching and conflicts

https://coderefinery.github.io/git-intro/08-conflicts/

- How `git branch -d` works? should my HEAD be in the source branch? can I delete from a different branch a branch that it is merged in another? Clarification: You have `master` create from there branch `A`, add 1 commit, create from there branch `B`, add 1 commit, merge`B` into `A`, move the `HEAD` to `master`. From there can you `git branch -d B`? or you have to be in `A`?
    - Can you clarify some?
    - You shouldn't delete the currently checked out branch (I think it won't let you)
    - It removes the "pointer" to commits, so if those commits are merged somewhere else, all commits still exist.  If those commits aren't merged somewhere, they are "orphaned" and don't appear anywhere (but not deleted right away)
    - To clarification: yes, you could delete `B` if I understand correctly.  It seems like a reasonable thing to do in that case (of course depending on your goals).

- Is it possible to create a new branch with just few files. Let's say if the master had thousands of files and I want to create a new branch but making a copy of the entire master will take up lot of space. In such a situation, could we copy just the files that will be worked on rather than the entire master?
  - Note that creating new branches does not mean using up more space. So create many branches. Git will not duplicate files between branches, in Git branches are not implemented as copies. A branch in Git is a file containing 40 characters and all it contains is the hash that it points to. Branches in Git are like sticky notes.
  - You can create unrelated, so called "orphan" branches which have no connection to the branch where you issue this command but I think what you wanted is still to have some connection but only with a subset of the files? Because with the orphaned branch you are completely disconnected.
  - It is also very fast at switching branches: only modified files have to be adjusted.

- **Can you comment on why the git graph looks that way after merging the branch from the exercise?**
    - why is there no 'lines' going to the right like with earlier branches?
        - do you mean at the commits on top?
    - yes, earlier branches got those lines going out to the right when something was changed, while the branch from the exercise did not have any in git graph.


- I made dislike branch from like branch. How can I move it to master?
    - See two points below for the same question

- Answer to a question regarding update file with a following `checkout <branch>`
This is explained in `git help checkout` (here is a text cut):
`git checkout <branch>``
           To prepare for working on ``<branch>``, switch to it by updating the index and the files in the working tree, and by pointing HEAD at the branch. Local modifications to the files in the working tree are kept, so that they can be committed to the ``<branch>``.


- What if you mistakenly branch from like-cilantro? Can you just delete it or can you rewind it back to the correct commit?
  - if you haven't committed to it yet, you can delete the branch with `git branch --delete somebranch`, go to the right hash, and create it there
  - alternative is to move it to the right place (`somehash`) with `git checkout somebranch` followed by `git reset --hard somehash`
  - before moving branches I would always first create a "backup" branch pointing to the same commit as the branch I am about to correct, before I move it. If I mess up, I can then always go back and still have it.

- Has anyone ever merged not with master?
  - Git merge always changes current branch which I am on (check with `git graph`) and I can merge any other branch into the current branch. My current branch does not have to be `master`.
  - `master` is not different/special, only difference is the name. One can even delete the `master` branch.
  - Does this answer?

Breakout room task:
- https://coderefinery.github.io/git-intro/08-conflicts/#exercise-create-another-conflict-and-resolve  ???
- You can also discuss the optional exercises too.
- And make sure you take a break!

- Can you explain to me what 'rebase' means in this optional exercise on conflict resolution? (ie definition, not written anywhere in that course page) Thanks
    - "Rebase" in git means "move a branch from one place to another" - rewriting history.  We don't got into detail about it now (by design), but you can check more about rebasing later.
    - It is a way to keep a more linear history, without forks.

- Github supports three types of "merging" operations (let's say merge branch `A` into `master` without conflicts):
    - Create a merge commit: you will see all commits of the branch `A` plus an additional "merge branch A" commit in the history of `master`.
    - Squash and merge: in this case, all commits of branch `A` are "compressed" into a single commit and being added to the history of `master`.
    - Rebase and merge: all commits of branch `A` are added to the history of `master` without an "merge branch A" commit.
    - The second and third types are useful for keeping you history clean :)

- What is the purpose of `-s recursive` in `git merge`?
    - It's a "merge strategy", some way it determines how to resolve conflicts.  I have personally never paid attention to this much, except sometimes this `theirs` and `ours` thing.

- If you had technical problems in the breakout room, please comment here:
    - I got kicked out a few times again, breakout room 10. But it went fine the last 7-8 minutes.
        - Did Chrome improve anything?

- Going over how to prevent merge conflicts in detail would be nice. But maybe just following all the software development guidlines in this workshop will achieve the same goal?
  - merge conflicts are bound to happen from time to time, but here's some advice from the lesson to minimize the risk: https://coderefinery.github.io/git-intro/08-conflicts/#avoiding-conflicts

- When cloning the repository for the last exercise some of us were getting the message "You are in 'detached HEAD' state. You can look around, make experimental changes and commit them, and you can discard any commits you make in this state without impacting any branches by switching back to a branch." What does that mean? Can you explain a little bit?
    - "Detached head" is a funny name, that occurs when you `get checkout` a certain hash or tag, instead of a branch.  It means "you aren't on a branch, if you make new commits they become unreachable"
    - In this workshop, we shouldn't get there, so I'd recommend making and checking out the branch.


### Sharing repositories online

https://coderefinery.github.io/git-intro/09-remotes/

This is just a preview of tomorrow, don't worry too much about full details here!

- Can I create a private repository instead?
    - You always can. in this case, you can if you want.  It won't affect much for this particular exercise.


Exercise: this type-along as an exercise:
https://coderefinery.github.io/git-intro/09-remotes/#type-along-create-a-new-repository-on-github


- How do we delete a remote repository name when it was mistyped in the terminal (after creating the repo in github)? Thanks.
    - `git remote remove <name>`
    - `git remote` lists the current remote names.


### History inspection

https://coderefinery.github.io/git-intro/10-archaeology/

- Is there a way to completely delete a file from history? Say, I push a very large file accidentally, and I don't want it in my repository.
    - `git filter-branch` can do this.  Search the web for descriptions of this.

- How does `git grep` differ from `grep -R`?
    - Quite similar, `git grep` has more options for searching history, only added files, etc.

- Any particular reason why the rvest repository is in a detached HEAD state when you clone it?
    - I'm not sure why it would be - can you show us?
        - I think I understood why, it's because it's cloning from a branch "git clone --branch v0.3.5 https://github.com/tidyverse/rvest.git". In "git clone help" says that "--branch" "can also take tags and detaches the HEAD at that commit in the resulting repository."
    - Please leave angle brackets in backquotes, otherwise coloring for the whole document gets off


Exercise:
  Main goal: https://coderefinery.github.io/git-intro/10-archaeology/#archaeology-exercise
  Optional: https://coderefinery.github.io/git-intro/10-archaeology/#git-bisect-exercise
  15 minutes, ending at xx:55


- `git checkout <hash> <branch-name>` creates a new branch, would a soft reset also be technically correct?
    - No, this is not correct. HEAD will move to the `<hash>.` All commits following the `<hash>` will be lost, or almost lost. There is ways to get it back, but a `git graph` will not show the commmits.

- Is it a very bad habit to use `git commit -a` in personal work (automatic staging of modified files)? Or should this be avoided for some reason?
    - If you are OK with having everything in giant commits, it's OK
    - In the future, when you come back, you wont't b able to tell things apart much.  If you only care about the big picture, it's OK
    - Another way to look at it, it's better than nothing!  (I have an alias that does this, but don't use it very often)

* I have problems with the command 'git commit -p'. This is the output in Win 10/anaconda prompt: git: 'add--interactive' is not a git command. See 'git --help'. fatal: interactive add failed
    * Interesting.  Does it say `add--interactive` without a space after `add`?
    * It says "git: 'add--interactive' is not a git command. See 'git --help'." So it seems that there is no space after add
    * It looks like `git commit -p` is trying to internally call `git add-interactive` instead of `git add --interactive` (the right command, with a space).  So... I'm not sure how to debug this.
    * As a workaround, I would use `git add -p` to add parts interactively (you can select which chunks to add), and then `git commit` which will commit those added changes.  I often do this anyway, when I want to make sure I got everything.


## Feedback, day 2

One thing that is good, one thing that should be improved:

* If you kind of lost it today could you give a takehome message about the main points I should learn so that I can follow the training tomorrow.
    * We showed a lot but will try to summarize the take home messages last 5 minutes and also be around for questions later

- There wasn't just enough time for the last exercise, mostly because the first one took 80 minutes instead of 35.  That being said, if/when this is the first time you are doing this online it wasn't too bad.  I am sure you guys have a better idea about the pacing next time.  I have never worked with git and I had no hard time following it - however your exercises could show the desired output so we could figure out if our input was correct. The message for grepping the text ended in vague 'FAIL' message so few of us thought that it didn't work...
  - It was indeed rushed and I apologize for that.
  - We will add solutions: https://github.com/coderefinery/git-intro/issues/250
  - And I need to find a better example so that it does not look wrong when it is actually working.

- In one breakout room, two people said it was good, one said it might have been too fast for new people

- `git commit -p`: unclarity in the manuals, doesn't mention what happens when changes are split between a few lines.
  - thanks for pointing it out, created an issue: https://github.com/coderefinery/git-intro/issues/249

* In the beginning of today's session we had to do some initialisation (add/commit/etc.). That kind of took some time for me and then I lost part of the intro and after that I was not able to follow at all. Could you next time have some instructions on what to do before the session so that no need to worry about that in the beginning.
    * Add/commit was covered yesterday.  We have tried to have more effort on makin sure software is prepared and configured in advance.  We will keep trying to make it better, but this will be difficult.

* Would it be possible to send link to the theory/introduction material before the session? It would be nice to familiarise oneself with it beforehand. Today, I was not able to follow the introduction and after that I just tried to "type-along" without actually understanding anything I was doing.
  - All the schedule is online, by clicking through lessons you can see some introductory explanation at the top of each episode.
      - But yes, the schedule didn't say what episode we would start on until very late last night.
  - Good suggestion. Tomorrow we will traverse this lesson: https://coderefinery.github.io/git-collaborative/
  - It will be important that you are able to push to GitHub and you can test it by making sure this works: https://coderefinery.github.io/git-intro/09-remotes/
  - TODO: make sure that the first episode of every lesson stands on its own as introduction to read.  Plus the first few paragraphs of every other episode.

* More metatalk would be nice. I understand it may give more stiff feeling but it helps to follow. Just explain what we will do in the next breakout room, point exactly to the web page where the exercise is and which exercises we will do. And the helper could perhaps repeat this in the breakout room. Radovan's last session was good in this sense.
    * This is a good idea, we will try to do this.
    * TODO: add to instructor guides
    * TODO: ensure that breakout room instructions are always clearly written in hackmd (and people know to look there).

* Could you repeat how to ask help during the sessions (push button x, say aloud, etc.). We are here for the first time so repetition is ok.
  - Indeed we need to make this clearer to everybody. Also to us. We are still experimenting with optimizing the setup.

- Will there be any more on rebase and squashing commits policy before pull requests? The two optional exercises on that was premature for most I think.
  - We will talk about this tomorrow (Wednesday) when we discuss code review in more detail.
  - Yes, they were too advanced for most people, but we try to have a variety of material to keep different people satisfied.

- Make the streaming link more clear on the website, confusion in left/right columns.
  - Thanks. We are working on making this clearer.

- When breakout rooms don't work for someone, we can leave it in the main room.
  - We are considering to try for the instructor to go through the exercise in the main room so that those who cannot join a breakout room or those following via stream can also follow.

- I was very happy today with the way the session went, and I believe that having exercises in the main room together worked better than in individual breakout rooms. Today I was in a breakout room where the helper did not share screen, therefore one of us share it and everything went very slowly so that we ended up working on our own to do the exercises. So to summarize: keep us as much as possible together in the main room (so that we all can follow what is going on, all at the same pace) and keep the breakout rooms for those who are in need of help.
    - Sorry, I removed some of your comments as they break our code of conduct. We would like to remind everyone that all our helpers are volunteers.
    - It is also a good approach to ask another person (not the helper) to share their screen, especially recommended when the helper sees that some attendees have lots of problems. We of course understand that it can be frustrating for you as there is no time to discuss more general questions in the break out room.

- It would be nice if the answers/solutions of the various exercises (with detailed explanations, tips and so on) were made available online.
  - Good suggestion. We need to add solutions, tracking it here: https://github.com/coderefinery/git-intro/issues/250

* The people in my break-out room have very different levels. A few have clearly already developed code but most are real beginners (they barely know how to use their computer). As a result the helper spends all the time available sorting out their basic problems and we do not discuss anything. That is a shame since these separate rooms were meant to be a place to exchange, ask questions, do more examples...
    * Yes, there are very many different levels of people.  It's a delicate balance to help most people and teach everyone.  In the end, the large workshops probably help the majority, and we have other events for others.
    * In this case, a helper should adjust and try to transition them to following along.  But it's hard to do this well.

- Given the extremely different level of the partecipants, I think showing all those (very nice) tools is a bit of an overkill. Instead of twenty minutes on how to explore git history I would have preferred a twenty minutes examples on how to write a proper commit message or a detailed discussion on good practices. The reason for this is that many users will not start from huge GitHub repos but will use git for their personal projects and building a solid history is the prerequisite for searching it. Also, I think that the concept of HEAD and the detached HEAD state should be a little bit clarified. How to recover from detached HEAD state? Why when we cloned the R repository for the last exercise we ended up in the detached HEAD state? I know all the answers are in man pages but I think that many people with less experience got a bit lost in the huge amount of information shared. Neverteless, personally, I enjoyed the session and learned a lot :smiley:
    - Yes, this is hard.  In this case, we try to have a final lesson which medium-level users can look forward to in the long term: to really show the long-term power of git.  and everyone can see some nice examples.
    - Thanks for the feedback. It's a difficult balance. But I agree we need a bit more on recovery from typical issues for beginners: https://github.com/coderefinery/git-intro/issues/217

- Yesterday we used terms Work tree and branch, are those about same concept of branching?
  - Working tree is the tree of files that we are currently modifying, in other words everything "outside" of `.git`.

- For us less experienced people the term staging was explained only after we had used 'ADD' leading to situation where instructions told you to stage things without us having never heard about staging. :P
    - Good point, the term isn't used before.  I'll make an issue about this.
    - Maybe one should also make an issue at git to rename `add` and `reset` to `stage` and `unstage` :)

- Yesterday, one of the instructor's voice was a bit noisy as if a paper was being crumbled.
    - Maybe visual instructions how to set microphone level to auto in Zoom would help (in many cases it does solve it)

- Better to split exercise and break , we were also not sure when the exercise
  session/break is over, maybe good to write it to hackmd when break/exercise
  session ends
