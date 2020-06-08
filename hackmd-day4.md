---
permalink: /hackmd-day4/
---

# Day 4 questions and feedback


## Questions about previous days

* This is related to a question about interactive committing (hackmd-day2). First, `git commit -p` did not work. I tried `git add -p` but it gave this error message: git: 'add--interactive' is not a git command. See 'git --help'. So similar problems seem to exist with `git add -p` as with git `commit -p`. I am using Win 10 and Anaconda prompt.
    * I tested this with Win 10 anaconda prompt and it works. I am using git version 2.25.0.windows.1. What is your version? Personally on win 10 I prefer git-bash as a shell/prompt (ask [name=Enrico] in private if you want to debug this)

- how to get a `.gitignore` file? I mean you guys have shown a weblink from where one can create one gitignore file so I am interested in that.
    - [gitignore.io](https://www.gitignore.io/)
    - I always hand-curate it, to make it as compact and meaningful as possible - but that's just personal preference
    - Alternative is that when you create a new project on GitHub/GitLab, you can create it with a gitignore file suitable for your choice of language and it can form a good start.
- after using the git revert, how can I access the files/open the files from the previous hash/commit? I mean can I open those files since I would not have them in my computer.
    - `git show $hash:$filename` will show any old version of the file
    - `git checkout $hash` will check out all files at that point.  Remember to checkout master again, or your next commit will be in some random place and become detached (happens to me too often)!

- I did not find the pre workshop instructions anymore, it was difficult to prepare for today.
    - There weren't any special instructions for today, besides the same software installation as before.  There were some things to think about it in the past  https://coderefinery.github.io/2020-05-25-online/

- Advanced optional topic: Does anybody here have experience with git hooks in GitHub Desktop? We tried to set up a pre-commit hook, and it works in bash, but our contributor using GitHub Desktop can't get it working (hook script runs, but paths to files in the pre-commit script do not work there :'(). 1000000 thanks if anyone can help! (stackexchange didn't:()
    - can you see any error output from the script?  In cases like this, I might put in an `echo $PWD` in order to figure out what directory it's running in
        - Excellent idea, thanks, will do as the 1st thing!
    - can you share a simplified/anonymized version of the script? or the link to the stackexchange question?

- Will the workshop website instructions and related videos be available on the CR website long-term? I would like to get my students to view these and follow the slides in the future...
    - Yes, the plan is that these remain available long term.


## Reproducible research

- Question: How about large data? if the raw data is TBs or GBs large it is not feasible to have it in the same repo.
  - there are several options to track metadata in a Git repo while keeping the big data itself on some storage in a versioned fashion:
    - https://git-annex.branchable.com/
    - https://git-lfs.github.com/
    - https://docs.gitlab.com/ee/topics/git/lfs/
    - https://dvc.org/
    - https://www.datalad.org/
  - Communities handling large amount of data usually have their own "repositories" and associated tools to access/version data. However, having metadata information in your github repository is good practice (with links/examples on how to access data).
    :+1:

- Will we get an overview of all questions to discuss in the first breakout session, or do we need to remember all the questions ourselves?
  - we will summarize these below

- Do you suggest using `Markdown` instead of `LaTeX` for writing thesis? If yes, which flavour do you recommend?
  - [name=Radovan] Hmm... I was thinking about this question myself how I would do it if I started with this today. I think I would still go for LaTeX. Markdown could be nice for more collaborative projects like book writing or open manuscript or open proposal writing. A thesis is more one person writing but then the question is, how do you want to collect and process feedback/corrections? Is the supervisor familiar with LaTeX?
  - It depends on your topics. LaTeX is not used by all communities (mostly depends whether you have equations or not in your thesis). There are other alternatives using markdown, jupyter notebooks, etc. (such as jupyter book, git book, etc.). The main issue is that most Universities still require to have a pdf final version (not an online version).
    - Good point. Whatever tool, what I find important is that images and tables can be cross-referenced, and that I can add references late and also reorder chapters late and move subchapters up and down one week before submitting and the numbering should automatically adapt.
  - I'd want to use restructured text, but probably still use LaTeX because people are so particular about formatting.
  - Note that if you start in Markdown or LaTeX or RST and you realize later that you prefer another format, you can convert using https://pandoc.org/.
  - Good to use a format which can be tracked in Git and which can be branched and merged (branching and merging can be useful when interacting with colleagues/supervisors who prefer to communicate changes/suggestions only via email or on paper).
  - [name=Rohit] Another alternative is writing in any kind of structured text (markdown, orgmode, restructured text) and taking some time to work out a `pandoc` template to convert to LaTeX


### Managing dependencies

- What is the difference between `conda` and `Anaconda`?
    - conda is the package manager, Anaconda is a "distribution" that comes with a lot of stuff by default, and does releases with certain versions.  Normally, one installs Anaconda to get a lot of good default stuff (or miniconda, to have a minimal setup), then upgrades/installs more as needed with conda
    - [name=Rohit] Specifically, `conda` is the 'super pip' tool which is shared by `miniconda` and `Anaconda`, but the difference is in the packages which are downloaded by default (think of Anaconda as a 'batteries included' version). I personally prefer `miniconda` simply because I like to keep track of what I use explicitly


### Exercise session: creating and exporting conda environments

Discussion for breakout rooms:

- computer programs should produce the same output for the same input.  Is that true for research software? https://coderefinery.github.io/reproducible-research/01-motivation/#discuss-with-your-neighbors-or-among-all-participants
    - [name=Room 16] Yes! Should we err towards keeping fixed random seeds (like in tests) or towards having more "example" workflows (like R vignettes)?
    - Room 3:
      - it became easier now to move between architectures and instruction sets
      - we live on 5-6 decimal points of reproducibility
      - is it a problem of software design if the code is not robust enough to not reproduce more than 5-6 decimals?
      - small incremental changes vs. cost of rewrite

    - Room 22:
        - Some of us have experience with complex softwareprocessing large data sets. In this case, runs typically do not generate the same results.
          - [name=Radovan] how do you track/version these large data sets? (for my own interest/education)
              - [name=Rohit] I've used Figshare for large (>1GB) trajectory files (but it isn't really version control in the command line sense)
          - [name=Rohit] What kind of analysis does not generate the same results? Even statistical measures like sampling should produce the same results with specified seeds....
        - One reason for getting different results when running parallelized programs is the random number generation. Since the ordering of events in the program in one rank in the cluster is dependent upon how communication patterns fall out (something which can vary from run to run), the random numbers drawn from the PRNG can be used for different purposes from run to runt. It is possible to make parallel programs deterministic, but it can require substantial effort.
        - Reproducibility can be re-gained by not looking at data from individual runs but by running multiple runs and look at the statistics.
- Collaboration on writing papers https://coderefinery.github.io/reproducible-research/02-organizing-projects/#discussion-how-do-you-collaborate-on-writing-academic-papers  - How do you collaborate on writing papers?
      - [name=Room 16] Google docs, but many people are working towards a git workflow
    - Room 3:
      - Overleaf
      - Anybody integrating Overleaf with GitHub/GitLab/Dropbox?
      - You can also git clone the manuscript to your computer and work locally. Can be nice when working on a manuscript on a plane/ without network. Later you can git push the changes.
      - Can one change the markup in Overleaf from TeX to something else? To use the collaborative features of Overleaf with colleagues who are not familiar with LaTeX.
    - Room 22:
        - We had different experiences, some of us using LaTeX, Overleaf and sending Word files around.
    - Overleaf!
  - Do you use version control?
      - yes within overleaf, history and 'resolved comments'
    - Room 22:
        - Yes. One of us had the problem  that he wanted to use git but the colleagues wanted to use svn.
  - How do you handle collaborative issues?
      - sometimes some people do not want to use overleaf and send comments on pdf version, usually we summarize them and also add them as overleaf comments, so that we can follow 'resolved' comments
  - How would you like to work if you could decide?
      - preferably everyone would use same system for collaboration, eg everyone would use overleaf/gdocs, unfortunately often everyone has different preference which, with many collaborators can end up in huge mess or a lot of work for the main author

- Creating conda environments
    - https://coderefinery.github.io/reproducible-research/03-dependencies/#exercise-creating-and-exporting-conda-environments

At the end of this session, you should have spent a few minutes discussing the first two questions (write down some ideas above), and then done most of the conda environment exercise.  **Session ends at xx:05 (update: 5 more min)** (both discussion and exercise).

Other questions/comments during exercise session:
- I cannot find the git repository to clone, link please!
    - https://github.com/coderefinery/word-count - but note, don't clone, "use it is a template" (see instructions) and then clone from your own imported repo
- CR staff, please write your visits above.
    - [name=Richard] some groups are just starting the word-count exercise now, some almost done.
    - [name=Enrico] some more time for discussion/exercise in the 3 rooms I visited

- Why generating from a template and not simply forking?
  - Forks can be preferred if there is an intent to later maybe contribute changes back. Templates are more useful if the goal is not to collaborate on the original repository but rather to create pristine repositories with a certain structure.

- Cannot remove env by "conda env remove wordcount":->
    '''
    usage: conda-env [-h] {create,export,list,remove,update,config} ...
    conda-env: error: unrecognized arguments: wordcount'''
    - what about `-n wordcount` ? >> Nope, I just removed the folder


### Recording environments

https://coderefinery.github.io/reproducible-research/04-environments/

- Any suggestion how to manage single computer environment vs cluster environment? Namely testing before launching to cluster...continuing... I am not sure what I am actually asking. It is both how to manage code such that I can run it in single computer and cluster, as well as how to define environments if needed for cluster. I'll clarify this when I know what I need to know.
  - Both would use the same requirements or environment file, right? Or is that
    perhaps problematic? Or is the problem perhaps that on the cluster you use
    parts of the environment which is not or cannot be encoded within a
    requirements/environment file?
  - Answering follow-up of the question: If all the dependencies fit into a requirements/environment file, then it should work on both computers (local and cluster). Sometimes you depend on libraries which are not available on Conda/PyPI/... and then there are dependency managers like Spack or EasyBuild which are popular on clusters but they can also be used locally on your computer to isolate environments and then you could use that to have a testing system on your laptop so that you don't have to queue on the cluster for every small debug/test case.
  - Another option is to use a Singularity container if the cluster supports this, then you could run the same "operating system" on both machines. One can convert Docker to Singularity.
- Is there a reason to use conda, when you can use docker? I feel like docker supersedes conda, am I right about that? Is there something conda is better at?
    - Docker itself has security issues that mean it can't be run on clusters (but that's what Singularity is for, so basically same thing)
    - containers are quite heavy and require more setup.  In my opinion, something simple should depend on the minimum amount  If something is distributed only as a container and has no way to install otherwise, I don't consider it reproducible.  So, you have environment.yml/requirements.txt for tracking dependencies, container for distributing.
    - Conda and Docker/Singularity have slightly different use cases. The former can record and manage library dependencies whereas the latter can record the entire operating system. If you have very few dependencies and the dependencies are persistent and well versioned, then Conda can perhaps be a more lightweight solution.


### Workflow management.

https://coderefinery.github.io/reproducible-research/05-workflow-management/

- Can Snakemake only be used with Python or with other languages as well?
    - It can also run shell commands (maybe that's the main way?), so nothing really special about Python
    - It is only written in Python and understands Python syntax but the rules can use any language/tool.

- How is snakemake better than shell scripting?
    - [name=Rohit] It does handle more edge cases out of the box, for example working with clusters or in docker environments. There is probably little to be gained if you have a good robust set of bash scripts tailored for your use-cases. The idea is that it is a gentler introductory workflow which is just as scalable. Additionally, using FOSS documented tools is also easier to share with collaborators, since you may not have documented your srcipts to the same extent as the snakemake documentation.
  - It's a question about how long the steps take and how many of these you have. If they are super short, a shell script is probably simpler and preferrable. But if the steps take a long time and you want to rerun only some of these, with a script you have to go in and comment out completed steps and a workflow tool can figure it out and also run steps in parallel.
  - Mainly, it manages dependencies and what has already been run to avoid re-running.  If you always only run the whole thing, then there's not much benefit.  Once you rigorously define things in a snakemake format, you get lots more, too: automatically submitting tasks to clusters, etc.

- How can I make snakemake consider if not the input files updated, but the executed program? Say I let snakemake run `./binary input output`, and `binary` changes.
  - If `binary` is listed in input, it will be considered in the same way as `input`
  - Indeed both the binary and the input files should be listed as dependencies of the target so when either changes, the target is recreated.

- My problems are caused by having installed pip before and now trying to follow with anaconda. I think in the info sent before only conda option would be more clear.
    - (I'm not sure what this refers to)
    - Good point. It is not easy to strike a good balance here since we know that participants use many different environments and we did not want to force those who are comfortable with virtual environments and pip to use conda. We can clarify this better. Whenever we mention `conda install`, you can use `pip install` and hopefully we manage to communicate the ideas and motivations which are essentially the same for `pip` and `conda`.

- What are workflow tools and how do they function?


### Exercise, Snakemake

https://coderefinery.github.io/reproducible-research/05-workflow-management/#exercise-using-snakemake


* The snakemake script is written for bash and does not work with the standard Windows shell. It works in Git Bash. Maybe we should note this in the exercise?
  - Thanks. I opened an issue on this: https://github.com/coderefinery/reproducible-research/issues/124

* When I opened Wordcount environment, there is no git installed by default? The archive command requires it and gave error. 'conda install git' fixed it though
    * We've seen this before: the git installs with its own "git bash prompt", and the anaconda prompt has a different prompt.
    * `conda install git` is probably a good idea to do.
    * Is this on Windows?

* what does .snakemake/ contain?
    * various metadata and cache files, that for example helps it remember what has run
    * Also using this metadata it does not have to recreate the dependency graph every time. It will only recreate it if the `Snakemake` file itself is more recent than the metadata.

- There  was a issue on snakemake on Windows (a litte more than a week ago). The issue is closed, but some participants where hit by this: https://github.com/snakemake/snakemake/issues/411
  - is this related to the issue I [name=Radovan] opened in our repository (124) [name=Bjørn] Not sure, but it seems related.
    - OK I will mention this also in the issue. Ah you have done that :-) thank you!

* Can you use snakemake with Matlab?
  - Yes, the rules in a Snakemake workflow can invoke any tool/language available on the system.

- What are declarative / imperative workflows?
  - An imperative workflow (like a shell script) describes the steps and their succession explicitly
  - In a declarative workflow (Snakemake, Make, many others) you do not program the series of steps explicitly but you program what depends on what and you let the tool figure out which step (target) should be done first, which second, which are dependent and which are independent.
  - [name=Rohit] To add to the excellent definition above, the utility is in the DAG generation, which otherwise would need to be listed explicitly. So, for example, in an imperative workflow you will need to have an implicit understanding of all the cases which can arise in the DAG and handle them in code.

- Comment: In snakemake exercise, second bullet point the (touch data/sierra.txt) is in the wrong place. Maybe helpful to add more of the commands in the exercise, if the point of the exercise is to understand whats happening. In my group also many people were very confused what they should observe in the exercise. Also having to scroll up and down ( also by the instructor during demonstration) was seen as very confusing and almost impossible to follow.
  - Thanks for feedback. Opening an issue: https://github.com/coderefinery/reproducible-research/issues/125
  - When noticing something like that is it ok to open an issue in github for everyone? Or better to let you (instructors) do that? :)
    - Yes, we really welcome and appreciate if you open an issue (or send pull requests) directly. This will help us to not forget these (although I am trying to lift some questions/feedback into issues). It will really help the project.
    - Some of the issues we only discover now that we have moved online to many participants. When being with 20 persons in one physical room, many of the questions are clarified in a different way but now we notice that some exercises are not clear enough.
    - as a helper I have also seen that, people are confused on what to do or why to do the exercise. I will take some time after the course and make issues of the experience

- An example of a project using Snakemake (snakemake badge), Zenodo and with Licenses: [PyPSA](https://github.com/PyPSA/pypsa-eur)


### Sharing code and data

https://coderefinery.github.io/reproducible-research/06-sharing/

- Should you tag a version before creating a release in GitHub?
  - When you create a release on GitHub, this will create a tag. Under the hood Github releases uses Git tags. So no need to create a tag first. But it's good to know that if you create a tag on your computer and push it to the GitHub repo, it will show up there as a "release".

- In Zenodo, can one remove a created DOI after we activated it in GitHub?
    - No, the point of DOIs is to be "permanent".  The Zenodo sandbox is used for testing to avoid making something permanent.
    - but actually it is possible in principle to remove a DOI in Zenodo, if a mistake has been made, by writing to Zenodo support
    - You can always update the metadata later (add/edit authors, description).

- Do we need to update / create a new DOI every time we update our repository? Because Thor talks about release...
    - Github has the concept of "release" (really, a git annotated tag), which is what creates the DOI.  So, not every new commit makes a DOI, but the ones you tag as important.
    - So whenever you create new releases on GitHub, Zenodo will detect it, pull the repository at that specific commit and create a new DOI



## Social coding

### Group work

#### Reasons for sharing code/data

Room 3:
 - sharing is caring
 - it gives credit
 - timestamping the research/work ("we did this at this time")
 - allowing others to build on your work

Room 5:
- Helps improve code by other commenting and improving it.

Room 6:
  - Pros:
     - Reproducibility
     - Simpler takeover of projects
     - Get more citations
     - Better review process
  - Cons:
     - Avoid embarrassment
     - Privacy (e.g. processing of clinical data, commercialization projects)

Room 8:
 - Able to get more feedback from reviewers
 - Actually sharing is suggested by the committee, and the paper can get a green badge after sharing and being verified
 - Increased impact of the work

Room 10:
- Being able to find mistakes, not being stuck for too long
- Fresh eyes on your code
- Others can find easier/different solutions if the code is available
- More and more publishers require this
- Get a timestamp for your implementation/idea so that you can later "prove" that you have done this
- Others who look for similar solutions can then extend instead of reinvent
- For tasks like data transformation somebody has probably already done something similar
- More collaborative and can create new contacts and collaborations
- If multiple versions/implementations are available, one can compare them
- Making it more available can make it more usable
- Making it more usable for others can make it more usable for one self

Room 14
- sharing is caring :D
- collaboration

Room 16:
- Pros :: It allows for more people to take part and drums up interest, and proves authorship online. It is also possible to keep contributing if you have a "platform". There is a change in perception, people are less toxic on open platforms (like Github).

Room 18:
- Reproducibility

Room 22:
- You get input from other people, like suggestions for improvements or spotting bugs.
- It increases the visibility of your work. Others may use your code.
- Reproducibility
- Journal asks for the source code!

Room 4:
- improvement by others made possible
- to check if it works on other systems


#### Reasons for not sharing

![](https://i.imgur.com/xWIcAGE.png)

Room 3:
  - too eager users try to use unfinished code that isn't yet working fully or missing documentation
  - possible embarrassment of unfinished product?
  - too much data could create more "noise" (but for published research paper the data should always be valuable)

Room 5:
- We share code for modelling, but not so much scripts for analysis/ generic enough to share it with others.
- Unsure if code/data can be shared, and then do not share it.
- Unsure if code will break others code, so chose not to share it.

Room 4:
- not feeling confident in own coding
- not allowed from higher levels (institutional / group policies)
- licensing issues (how to do it right? not to end up in legal issues)

Room 8:
 - Not allowed by rules e.g. patent application
 - Data privacy issues
 - Messy codes, not ready for share

Room 10:
  - Somebody else can follow-up unpublished ideas and get more credit than me
  - European data laws when working with human subject data. It can take a lot of work to convert the data to a form which can be shared.

Room 14
- Intellectual property rights
- ethical issues (code can be used for malicious purposes)

Room 22:
- Collaboration with private companies. They may provide data with NDA or have patents.
- Commercial interest in selling the software.

Room 7:
- citations (open) vs. collaboration (closed)
- sometimes trying to capture intellectual property
- if public: comment your code!

Room 16:
- Cons :: Patented code is difficult to work with, even if papers are written, people forget to cite them. It is difficult to have to maintain a community and hype. This is especially true in comparison with codes with a larger endowment (like a dedicated university team)

Room 13 and 19:
- Pros: get additional collaborators beyond your own group
- Cons: not suitable if  there is confidentiality issues


#### Why is software treated differently from papers?

Room 22:
- Software is a tool for producing the results. If others have access to the tool, there can e a feeling that
- they can compete. (But having a competitor is good.)


### Social coding continued

- Why should I care to share my bugs history when I can share a "cleaner" version of my code?
  - Good question. I [name=Radovan] think one problem can be that a "cleaner" version never arrives ("I will fix it next week" and then we are busy and move on to other projects). So at least I think we should share the version that we have used in a publication even though it is not cleaned up yet. A code is never "done" so we should not wait for it.
  - [name=rkdarst] If you want to share to meet some requirement, then that's enough.  But it won't inspire a community, so you won't expect to get contributions back or inspire confidence to have lots of people build on it.
  - [name=Rohit] One of the fun aspects of releasing online is that you will realize that no one will actually care about your release history! It shows growth and motivation, if you show that you have been improving your code. You can also use the history to prove ownership. "One clean zip file" tells viewers nothing about who when and how.

- [from zoom chat] If I put a project in github first private and then later when I submit my manuscript to public, is then the full history of uploads also published?
  - [name=Rohit] Not very proud of this, but this situation is why git remotes are a useful feature. Often development will continue on say, a Gitlab repo, and there will be a public Github repo, with issues stating which group is working on which feature.
  - Yes, if you share a repository on GitHub you share all branches and in this case all commits would become public.
  - Some projects work with two repositories, one public, one private. The public one contains the `master` branch which contains all published code and which other groups can use as a base for derivative work. All unpublished branches can be collected in a private repository.
  - The fact that opening up a branch opens up all commits is important because if the Git history contains code with incompatible license, you may have a problem and may need to clean up the Git history. This means that we should also be careful including code with a problematic license since it may prevent me from opening up my own code later.
    - [name=Radovan] anecdote: I am now spending a lot of time cleaning up the Git history in a project which we would like to open source. We have to take out some closed source code which was added years ago without much thinking about this aspect.
  - This is why I always am very careful to separate private data from the repositories that (will be/are) public.  Even before it's public.
  - [name=Enrico] With new projects, I try to work as if the repo is public even though is still private. I might win the lottery and disappear suddenly and others in the team can pick it up. Otherwise two repos (as written above) for those sensitive cases (patents, NDAs, ethics, etc)
    - [name=Radovan] I really like this approach, I need to remember this: work as if it will become public at some point.  +1
    - I opened this: https://github.com/coderefinery/social-coding/issues/50

- [name=Rohit] Why is changing languages considered to be derivative? In many cases a switch in language will change the underlying machinery. Eg. Writing something in Haskell will be completely different from the python implementation to the point where only the algorithm is preserved (and could be cited)
    - If you would break the code down into the basic ideas, and reconstruct something new from those ideas, that would not be a derivative work (see: https://en.wikipedia.org/wiki/Clean_room_design)
        - [name=Rohit] An issue with clean room design is that it is really an industry oriented approach in the sense that there is a product with functionality to be replicated. This is not the case for most academic situations where algorithms are front and center of the code.
          - [name=Radovan] indeed I haven't seen cases of clean room design being applied in the academic setting but it's something big tech companies do.
          - [name=Rohit] I believe, clean room designs actually are often different only in terms of the interface specifications (i.e. different language, same features)
        - [name=Rohit] To clarify, in the typical case for clean room design, you might say, I like this interface, from this product, and then you implement that, possibly with different algorithms from the original. However, in academic situations, you *must* have the same results to be comparable, so you are stuck immediately
    - but... there is a high likelyhood you are pretty directly inspired by the creative expression in what you watch, and thus use that creativity in your new code.  That is what makes it a derivative work.  To understand more, see the linked above wikipedia article.
    - Also when writing the new code you often use the old code as reference to debug functions, to create test cases, to compare intermediate values.
        - [name=Rohit] These values though, might be reported in a academic publiction (and therefore could be argued to be independent of the code)
        - Yes, that's a good way to ensure it's not derivative
            - [name=Rohit] However, many of these might be linked to tests in a code repository, which brings up the same concerns (regarding derivative codebases)

* Can you / should you cite code that you use in a scientific article and how to do it?
  - Yes it would be good, only the first level (no need to cite the code used by the code you use). Hopefully these codes have a recommended citation. Many don't but you could open an issue or contact them and encourage them to create a DOI and specify how they want to be cited. The authors are typically happy to hear this and answer this.
      - So I then add the code (or reference to it) in the reference list of my article?

* I guess the DOI is needed only with "publication ready" code?
  - For published code. But also many codes/scripts are used but never get "finished"/published so citability is only one aspect but another one is preservation/archiving.
  - [name=Rohit] By construction, it is linked to "release objects", but the definition of what is a release is fluid in and of itself

- cicero.xyz looks very interesting! Is it being used by many people already? Is it going to be maintained for a long time? I am interested to make all my future presentations via it. +1
  - [name=Radovan] disclaimer: I am one of the authors. I like it and use it and encourage contributions. What I like about it is that you throw markdown sources into GitHub/GitLab and that's it, slides get generated on the fly. They are also branchable and versionable. https://github.com/bast/cicero. It's running on AWS, currently does not cost much and I plan to keep it alive hopefully "forever". The plan is also that talks once published remain working and accessible. No more "can you please email me the slides"? To be fair, Figshare is a really nice alternative since there you get a DOI.
      - Big thanks for this work [name=Radovan]! I assume a good alternative with a DOI could be Cicero + the Zenodo-GitHub connection.

- can you change the license after one is chosen to start with in Github?
  - If you are the copyright holder you can change the license. Note that you cannot change the license for already published code but you can change it for current and future versions. If the project has collaborators, the collaborators may be copyright holders and you may need to get agreement from anybody so changing license for large projects later can be organizationally tricky.


## Feedback

As usual, one good thing and one thing to improve

- PRO: very nice introduction to sw licensing, very much needed, in my opinion. CONS: too little time for breakout sessions, especially the hands on part. The discussion on Conda was a bit too fast and the installation conflict for `pandas` hindered the resolution of the exercise (this comment may be a bit out of scope).
- Really enjoyed the discussions. These were valuable to me. This session was a good overview and for that intention it was suitable. However, I do not feel that I would be able to use the proposed solutions after today's session.
- PRO: I really liked the presentation about social coding, especially the section about licenses since I did not know much about it and nobody in my lab was able to help
- PRO: nice to have some discussions also in breakout rooms

- PRO: sw licensing session was very good!
- PRO: Discussions and writing results, are often more useful then doing exercises (both is ideal, but takes too long).
- PRO: now I understood the licences and its importance, I'll add it to my existing code repos retroactively. CON: I need to familiarize snakemake but it seems at the moment bit a mountain to climb. To develop: How about cython code, does snakemake understand pre-compilation of pyc stuff. Very good session again. Thanks!

- CONS: We only scratched the surface when it came to the use of conda and also containers. This is something I would like to learn more about, perhaps with another dedicated 1/2 day Code Refinery workshop?
- CON: anaconda, docker and snakemake session was a bit too fast to follow (if you have never heard about these before), especially because of a lot of scrolling up and down in the document. Maybe it would help to do a bit of an introductory session before where all tools are presented together and example use cases are discussed. And more specific details later.
- PRO: Very good information retrieved today both in lessons and in the informal discussions
- CON: The breakout room sessions were too short for both exercises and
  discussion. Perhaps it would be good to have separate breakout room sessions
  for discussion and for exercises. If both are in the same session some kind of
  greediness happens (at least for me) and I try to finish the exercises and
  discuss if I have time (probably not). Also, point-by-point instructions for
  the exercises would be beneficial. So that you do not need to scroll up and
  down the web page and also wonder what is the correct command at this point.
  This more challenging approach (no point by point instr.) is probably more
  educative, but it requires clearly longer breakout room sessions, at least
  for me. Or perhaps instruction for the breakout room such that use 10 min for
  exercises and then discuss 5 min no matter if you finished the exercise or
  not.

- Not really feedback, but I wasn't sure where to ask this: I won't be able to attend tomorrow's session. Will I need to prepare/practice something on my own for Thursday or will I be able to follow?
  - The topics we will discuss on Thursday will not depend on the topics discussed on Wednesday. We will practice with testing (we will use Python as an example). The second lesson on Thu will be more watching a live demo of writing a project and commenting/suggesting changes via HackMD.


### What will you change in your project based on what you learned today?

- try out snakemake for processing chain
- try out licensing before making the repository public
- consider using snakemake, not just bash and python scripts
- Try to implement Docker in addition to conda environment, start using snakemake, add licence info to my repos.
- I will definitely attempt using snakemake and maybe conda environments.
- I will try to be more careful about the licensing, for the things from others that I use, and for what I produce myself
