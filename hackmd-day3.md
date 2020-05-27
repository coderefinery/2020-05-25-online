---
permalink: /hackmd-day3/
---

# day 3


## git-collaborative

https://coderefinery.github.io/git-collaborative/

* Will we discuss how to work collaboratively using git? Just practical stuff and best practices.
    * Yes, basically that.  Key points are two ways to use github, and hints related to that.

* In the email sent on 26.05.2020, it was said that _deleting a branch does not delete the commits_. Can you show how we can reach those commits in a deleted branch?
    * I guess this applies only to a _merged_ branch? A deleted unmerged branch is lost.
        * see below for ways to recover these lost commits
        * eventually, these lost commits get deleted as part of a garbage collection
    * Note that when you delete a branch, it prints "was: [hash]".  This can be used to recreate it, if you happened to delete the wrong thing.
    * `git reflog` can show these "orphaned commits", but is rather advanced.  General summary: find the hash, then create a new branch from that with `git branch old_hash`

* What is the difference between a `tag` and a `ref`?
    * A tag is a type of ref.  ref is anything that points to a commit (branches/tags/remote branches)

* Does `git graph` as defined by us show orphaned commits?
    * No, `--all` means "everything reachable from all current branches/tags/etc.  Orphaned excluded

* With some frequency it appears a terminal in front of the screen of Radovan
    * I see it too I think it's a zoom artifact.  I've seen the same in other meetings, and we couldn't find a good solution

* Please try to put all the websites, that are used at the moment also to the chat, not only here, thank you!
    * OK, I'll try to.  Often times I miss the websites, so any help is appreciated!

* How do you submit a pull request?
    * We'll get to this soon.


### Remotes

https://coderefinery.github.io/git-collaborative/01-remotes/

- what does origin/HEAD mean? wasn't HEAD the current branch
    - This is a really good question!  So, it tells you what the current remote's HEAD (or perhaps more precisely, current branch) is.  I don't think it's used for much.
    - `origin/HEAD` will point to the default branch on the remote. Typically `master` but you can change the default branch and then you will see `origin/HEAD` adjust. The default branch determines 1) which branch tracks issues and 2) which local branch we get when we clone.

- Can you recommend a website to generate the templates (i.e. the cookiecutter idea)?
    - do you mean, for example, "generate a template Python project?"
        - Yes
        - I don't know of any myself, maybe someone else can comment
    - You can make your own template repos (that's how I've seen it so far)
    - I have seen few templates but for some reason the authors chose not to make them "templates" in the GitHub sense (e.g. https://github.com/MolSSI/cookiecutter-cms)

- How can multiple branches be reduced to only one commit (generate from template)? What happens if you have parallel branches, what does this commit contain?
    - It does the equivalent of "create one new commit, with the current state of all files"
    - For the *multiple* part, I'm not sure just what it does
    - If you generate including all branches, it will flatten all of them into separate commits, each on one branch, and these branches are then unrelated/unconnected, as if they all started separately.

- difference between fetching, cloning and pulling, forking
    - clone: make a full copy of a repository (on your local computer)
    - fork: make a full copy of the repository on github or other site (yes, very similar to above - you could consider a clone a fork, too, but it's just a terminology thing)
    - fetch: check the remote, bring commits from it to current view.  Don't adjust our own branches
    - pull: fetch + merge(using some default strategies)

- Is there a command to generate from a template on github?
    - Besides clicking the button?  I'm not sure.
    - Either the button or follow a link (e g. https://github.com/coderefinery/template-centralized-workflow-exercise/generate)

- How does git resolve merge conflicts in pulling? Does the remote have priority?
    - If merge can't be done fully automatically, it will create a conflict and leave it for you to solve.  Unless you give it a strategy that says otherwise.  They are treated basically equivalent.
    - `git pull` is a `fetch` followed by a `merge`. If the merge fails, the conflict will behave as with the branches we have seen yesterday and resolution is the same (edit, resolve conflict, git add, git commit)

- I cloned the rvest repository, do git graph , but then I do not see a local master, just the origin/master as branch . Why?
    - I'm not sure, I see it... I have to scroll down a bit to see the local master (it should set up the same as the remote master)
    - If you did the exercise yesterday, your local branches may be different.

- Suggestion for when you need to explain something in addition to web content, maybe to use the 'screen stream' app for bluetooth mirroring of phone/tablet with drawing app.  :o)
  - Thanks for the good suggestion. We should make more use of drawing boards to build it up progressively instead of throwing learners into a possibly confusing drawing.

- Does using Github's desktop app automatically sync repositories?
    - I'm not sure, does anyone know?  It would make sense if it semi-automatically fetched, but not merge
    - I don't think it does, you still have to fetch/pull and publish/push changes to update the fork last time I tried.


### Centralized workflow

https://coderefinery.github.io/git-collaborative/02-centralized/

- In creating the branch, why is it a good idea to use `/` (eg. yourname/feature1) instead of eg. `-` (yourname-feature1) or `_`?
    - I actually think `-` might be less confusing... it's just convention (a confusing convention)...
      - I was always wondering whether '/' was confusing and from now on I will recommend to use '-' although personally I got used to '/'. I feared that it could be mixed up with 'origin/somebranch'.


### Centralized workflow exercise

https://coderefinery.github.io/git-collaborative/02-centralized/#centralized-workflow-exercise

* You go through most of this lesson, see if you can get to some discussion
* Each person should be able to make a pull request and have it merged.
* 20 minutes, ending around xx:15.  Break afterwards.


### git-collaborative continued

* A quick question, is the pull request on github similar to a git pull? because the name is confusing for a merge of branches vs a pull from a remote
    * The name comes from "I want the administrator to do a pull from me".  In reality, it's an internal merge within github.

* If you delete a local branch after merging, the remote branch still exists. Does this mean that there is a another step to delete the remote branch, and does it matter?
    * Yes, another step.
    * You can delete remote branches from your terminal with `git push origin --delete branchname`. What I often do is to go to GitHub and delete them there by clicking on a trashcan in the branches overview.

* I deleted the feature branch on GitHub but it shows up on my computer when I do a “git branch -a”
    * `git fetch --prune` should remove these.
    * Since git is decentralized, these views don't automatically update.

* How do synchronise the outputs of "git branch -a” across all collaborators?
    * Everyone should fetch.  also see above question

* What is the best way to make a new version of a repository if you don't want to merge the changes, but you want to make a new version of the code/experiment? Should you first copy it to a new repository or make a branch?
    * If you don't need both versions to be in the working directory at the same time, I would use different branches.  But of course, you can only have one thing checked out at once
    * If you need the files to be checked out at the same time, multiple clones.  Both to the same master repository, but different branches checked out.

- When should I use pull requests on Github, and when should I do a merge locally and push that to Github?
    - The major benefit of Github PRs is that other people can review.  Sometimes I do it on Github to give others a chance to comment (usually they don't, then I merge myself since this is a small project)
    - If it's not a repository you have write access to, you need to use PRs
    - if many people are working, PRs let you synchronize better

- After Radovan fixed the README.md on the template repository, how can I update the repository to include the template updates?
  - Assuming you have cloned your version of the repository, you can pull changes from the "central" repository with `git pull longcentralurl master` and then push them to your repository with `git push origin master`
      - But, since it's a template, aren't the histories disconnected, hash different, and there's no real good way to do this?
        - Ah yes, very good point! Forgot about that. Right.
        - I would probably solve it like this:
          - I would add the "central" repo as an additional remote (I would call it "central")
          - I would then `git fetch central` changes from that remote
          - With `git log central/master` I would find the hash of the change
          - I would try to cherry-pick that change to my local master: `git cherry-pick somehash`
          - Then push to my remote
          - I think this would work

- when I am using a remote repo and switch between a local and a remote version, am I editing files locally or on the remote? E.g., in the exercise, my last command was `git push origin -u username/feature`. Now if I do `vim filename.txt`, an I editing locally or on the remote?
    - You are editing locally (you only can).  Committing and pushing/pulling is how remote things get changed
    - All commands are local, except git push, pull, or fetch. Those are the only ones that travel over the network.

- how does github ensure that collaborators do not generate the same hashes?
    - The hash comes from the actual content (content+timestamp+authors+commit message), so that unless the content is the same, the hash will always be different
    - This is the way hashes are made, search "cryptographic hash" for info.


### Forking workflow

https://coderefinery.github.io/git-collaborative/03-distributed/

In this lesson, it is very similar to what we did before, but instead of "adding as a collaborator", we "fork" (make a personal copy), and see that we can send pull requests just like normal.  This means that you can easily contribute to any other repository, without asking for permission first.


### Forking exercise

https://coderefinery.github.io/git-collaborative/03-distributed/#exercise-practice-collaborative-forking-workflow

* This is quite similar to before, but instead of adding a collaborator, you *fork*, push to your fork, then make the PR.
* No need to add collaborators here, only thing they need is the URL where they will fork from.


### Forking workflow continued

We continue with an example of going through this repository

- in the last step of part F (long route), why do we use  `git push origin master`  if we created alias `upstream`? Shouldn't it be `git push upstream master`
    * You don't have permissions to push to the upstream.  In this case, teh point is to "transfer" commits from upstream (updated with everyone's stuff) to origin (your older copy)
        * So, origin is my forked copy and upstream is the central version?
        * yes - assuming you originally cloned from your own copy
        * `git remote -v` should clarify what is what
        * when I do `git remote -v`, it says (fetch) and (push) at the end. What does it mean? And it has it for both upstream and origin
        * There's a way to have separate paths for pushing and pulling.  I hardly ever use this, but could be useful in some cases.
        * The important part in the `git remote -v` is the web address, check whether origin refers to your repository where you can write to.
        * If you accidentally cloned the "wrong" one, there is no need to delete and re-clone, you can modify origin (`git remote set-url origin otheraddress`) or to add your fork as an additional remote (`git remote add myfork myforkaddress`) and refer to `myfork` instead of `origin`

* Is flow: central->fork->clone usually then updated central->clone->fork path (ie via local work directory to fork)
  - yes we will prefer to clone the fork, since this is the repo you can write to
  - and we update forks typically via the local repository (I wish there was a more automatic way and always wondered why GitHub does not have simply a button to update forks)

- 'git push origin "my-new-fork"' results in "remote: Invalid username or password"?
  - check what origin refers to with "git remote -v", maybe you are trying to push to a repository which is not yours? Also the syntax is `git push whereto whichbranch`
    - origin path is correct, I tried now login in to Github.com with another browser with my creds and I cannot login there either. Possibly some login bug?
      - if origin is correct, then either the password is wrong or maybe you have two-factor auth set up and then you may prefer using ssh keys to authenticate pushes.
        - ok, problem solved
          - thumbs up!

- Could you elaborate again the pull request? For me, I pull from a remote repository. Why do I have to accept a pull request when I push a branch to the remote?
  - the name is historical and better name would be "merge request" and this is the name on GitLab. Traditionally it meant "please review my changes and if you agree pull them from my fork".
  - even better name could be "change proposal"
  - ok, thanks. So it's not only me thinking that it's bad naming ^^
    - i also think it's confusing naming, confused me for a long time
    - Maybe it's worth to highlight the bad naming before introducing it..

- Git status does not show upstream differences?
    - This is based on "tracking branches", one gets set up when you use `-u` in the first git push.  It can be set other ways, too, like it may be automatically set when making a new branch.

- Can we update our forks from our GitHub fork page, or does it have to go through command line?
    - typically through command line (two commands; also discussed above)
    - I wish there was just a button
    - One way to do it through the web is to send a "reverse" (by reversing source and target repo) pull request towards your fork but I don't recommend it since it can create new merge requests and the master on your fork can at some point look different than the central one and that will bite you once you want to send the next pull request since it may then contain unrelated commits.
    - If you only work on feature branches, you perhaps don't even have to update the fork and `master` on fork can stay behind as long as you create new branches from an up-to-date master.

- is there a way to "protect" your master branch from accidental commits on the master branch when a new branch should have been used?
  - On settings -> branches you can add branch protection rules and I recommend this for `master` if you are several people. Then you can agree that all changes go through code review and nobody pushes changes to `master` directly.


### How to contribute changes to someone else's project

https://coderefinery.github.io/git-collaborative/04-contributing/

This quick lesson is about the social aspects of contributing to someone's project: technical tool is the distributed workflow we just did

- When I push some changes to a fork and am waiting for the "acceptance" and then continue working on that branch: should I wait before pushing again or should I chain several pushes?
    - If you get to this point, we recommend one branch per feature
    - Otherwise if you continue on the same branch, these commits get added to the open pull request which can surprise you and confuse the reviewer
    - If your continued work depends on something that you have submitted and that is waiting, branch off from that branch and continue work. Once your first change was merged, you can rebase that new branch onto `master`.
    - Sounds good except I don't understand the rebase part yet.
      - Rebase can be used to "move" the starting points of a branch
      - https://coderefinery.github.io/git-branch-design/01-rebase/
      - It's like cutting off a branch on a tree and transplanting it to another place
      - In this case above I would start branch2 based on branch1. Branch1 waits for code review and eventually gets merged to master. Later I can "move" (rebase) branch2 on top of master and it will look like branch2 started from master and at some point I can send a pull request from branch2.
      - Rebasing is advanced and it modifies history and it is OK to not use it.
      - It can help creating more linear histories.
      - Ok, got it. Thanks!

- how to add a colaborator in a project on github? Is it under setting/action permission/add runner?
  - settings -> "manage access"


### Day 3 feedback

* Pro: The breakoutroom worked much better today. Examples are very clear and gave us good experience of working collaboratively.
* Cons: The only thing is to keep the  text in one place to not confuse people with what the text is. Try to be consistent in time structure for class (when breaks are).

* For the breakout rooms we managed to do very little, and that little was not even always correct. Next time that will have to be better prepared and at least tested, to make sure the instructions are up to date.

* The examples with central->distributed were very clear, to improve: some were missunderstanding "examples" as lines that should have been executed. The remote upstream namely would benefit from different backround for "do this", and "read this". But I liked a lot.

* The first part of the main session was good, although really fast and I am not sure those not familiadayr were all able understand.
* The second part was really confusing and difficult to follow (Richard even intervened to ask what that was about) especially when the trainer went back & forth in the teaching material or did not share his terminal while typing.

* A thorough recap next Tuesday at the start of the session about what we did today will be highly appreciated.

- The main reason I registered for this workshop was to know more about "Collaborative distributed version control" and learn the best practices through simple exercises. I get out of here really frustrated.
  - [name=Radovan] sorry to read this. I would love to hear what I/we can do to avoid this in future. Was it the presentation? The material? The exercises/examples? The timing? Speed?

- Feedback:
    - Pros:
        - Very well designed exercises
        - Clear and easy to follow explanations
    - Cons:
        - Time allocated to exercises a bit short
    - Overall: a big big up for the effort, the material and the energy put in this. Thank you!

* Maybe next time we could show how to do it firstly, then we redo it in our group. I think it is easy for following. This morning, I did not get most of lessons.

- In our breakout rooms one person litterally monopolized all attention of the helper, systematically. That slowed down everything and significantly affected our sessions. It may be better, perhaps, to put absolute beginners together into a separate group and adapt the the training for them.

- Great and important exercises (\*\*\*\*\*)! Unfortunately not enough time to finish them during the time in the breakout rooms, we always ended with 70% or so. In addition, I managed to mess up the setup a bit as a helper. Clearer helper instructions in advance (for dummies) would have helped, because even this trivial setups could be messed up when doing it under time pressure while listening to the instructions & following the lesson & editing the hackmd :-(
