---
permalink: /hackmd-day6/
---

# Day 6 questions and feedback


## Left-over questions from day 5

- Is there a binder for particularly for JupyterLab?
    - It runs a jupyter server inside which has both notebook and lab enabled.  you can configure the URL to start JupyterLab by default, or change `/tree` to `/lab` in the URL.
    - binder examples https://github.com/binder-examples and for jupyterlab (https://github.com/binder-examples/jupyterlab)

- Which tools do you suggest to use Jupyter for teaching? With automatic grading which does not have security and privacy issues?
    - [name=Richard] has done a lot with this, contact me later and you can join our discussion.  I don't have any perfect answers yet...
    - I use nbgrader for automatic grading of jupyter notebooks (https://nbgrader.readthedocs.io/en/stable/)
        - [name=Richard] this is what has privacy and security issues, if you aren't careful...

- In `binder` can you for instance, instruct installing Homer or bedtools in the `requirements.txt`?
  - I am not familiar with these packages but are they on PyPI or Conda? If yes, then yes. But even if no, you probably can if they can be pip-installed or conda-installed from a GitHub repository or a custom Conda channel.
  - There are many different way to set up the environment: requirement.txt, conda environment.yaml. R requiremest, julia, dockerfile, rawspace postBuild script. So anything should be possible, it's a matter of how hard it is to figure out.


## Icebreaker: What from CodeRefinery are you going to use in the near future?

- Git, automated testing, possibly snakemake
- Jupyter + binder for teaching
- use of git and github, also the jupyterlab looked very handy and its integration with git.
- Jupyterlab, and hopfully integration JupyterLab + GitHub, for course material/tutorial
- Several git functionalities I wasn't aware of, Jupyter, code documentation tools
- wishful thinking: everything. reality: git, jupyter
- Git and JupyterLab. I'd also like to learn more Sphinx.
- I will definitely use git and github more consistently (now that I know what best practice is for collaborative work), also with the integration into Jupyter that will make my life much easier.
- Git and Jupyter more systematically. Hopefully create and teach good computational practices to the rest of the research group
- Workflow languages. Prefer Nextflow over Snakemake.
- Sphinx, Readthedocs, git graph (using already all the time), branch restrictions, git-jupyter plugins, Snakemake (hopefully it gets more stable on win, too), maybe Cicero and reveal.js, Click
  - [name=Radovan] don't hesitate to reach out if I can help with the Cicero-reveal setup or if you find problems or room for improvement.
      - Thank you!
- Git and Github/gitlab to share my code for colleagues and department
- Organize my project: folder structure, git, github, documentation, code using jupyter notebooks. Also snakemake will definitely make my work more efficient.
- git and gitlab, documenting and paying attention to FAIR
- Git, GitHub, JupyterLab + Git, maybe Sphinx.
- Git/GitHub and more usage of FAIR practices
- Already yesterday I started using Sphinx
- Git and Github, somestatic page generation (not sure if sphinx), change from jupyter notebooks to jupyterlab.
- JupterLab, Git, GitHub, Code documentation
- Git and GitHub for sure, perhaps JupyterLab
- I am not convinced about the use of snakemake and sphinx, but I will use git/github/jupyter from now on
- Git, in Hub or Lab, as apart the project development work
  Jupyter(Lab) looks promising for documenting and testing
  Snakemake for standardising workflows
  Now only need time to implement all these...
- I will use version control definitelly, also  I would like to experiment with integrative workflows by using snakemake. I also will use tools for documenting my work. This was a great course, I will go slowly again through all the material.
- Decentralized development using GitHub at its most
- Git, GitHub, Docker, Jupyter Notebook, at least
- Previously used Git, now I will start using also GitHub
- Already used git tags to make a release of an existing repository
- Github, jupyter, hope to use snakemake more
- I will continue to learn to use version control with git for sure, and I think I will start to make use some of the other tool as well
- Will start making better use of git and version control in general.
- Git: diff, bisect, tag, feature branches. Snakemake & licensing.
- Snakemake, Licensing, CI
- Better using git, maybe also sphinx!
- Git and more systematic documentation.
- Git branches, better documentation than I have done so far, try start releasing my own work in GitHub, learning how to make CI working with my code, Try to get benefit from parallel notebook, add licence to my projects... a lot of stuff can be started to use. I still hesitate with snakemake, but I just need to learn it.
- Use git and Github for developing programs/tools, documentation tools to documentation tools and distribute training materials, jupterlab to deploy and run some tools.
- jupyterlab & git, thank you very much!


## Automated testing

<https://coderefinery.github.io/testing/>


### Motivation

<https://coderefinery.github.io/testing/01-motivation/>

- haha, had the same (or similar) problem with unsorted files on ubuntu.

- what are "interpreted dynamically typed imperative languages", "compiled languages", "legacy code"?
  - compiled languages are languages like C, C++, Java, Fortran, Rust, Fsharp ... where a compiler translates source code to machine code. Disadvantage: extra step. Advantage: compiler can catch many problems before the code is run and has the chance to generate more optimized code.
      - which languages are not compiled to machine code? Hard to imagine for me.
        - Python, Julia, Matlab, R, Bash, Lua, ... but they are also translated but "just in time" or "on the fly" or implictly at runtime. They are interpreted when I run the code/script, not before I run it.
        - is there an option to let it compile before? For detecting errors before long runs..
          - what I wrote above was a bit simplified. Python can detect many problems at startup time but cannot detect all problems because of its dynamic nature. Looking at Julia, while it can be regarded as just-in-time compiled, it can detect many more problems before the code starts because it has strong typing and can make sure that types match up.
  - interpreted languages are interpreted "on the fly", there is no explicit compilation step visible to the user. In other words instead of a compiler complaining about problems, sometimes problems show up at run time.
  - Dynamically typed languages: language like Python where you don't have to specify the type (integer, float, boolean, string) of a variable but the language will dynamically infer the type. Advantage: convenience and flexibility and readability. Downside: some problems show up only at run time.
  - Legacy code: code written over longer time, typically by others, typically a lot of code. You enter the project and lots of code is already there and it may be too late or too much work to change things. But the code is still used and useful.

    - Thanks a lot for the extensive explanations!

- Is there a list of tools for testing in other languages?
  - we will mention few after this exercise: https://coderefinery.github.io/testing/04-frameworks/
  - with c and c++ I recommend valgrind for memory leak checks. https://www.valgrind.org/


## Exercise

<https://coderefinery.github.io/testing/03-pytest/>

Question about the exercise: I understand how a simple test in a small code can be implemented, but we work with very large codes (hundred thousand lines) and just to compile this already takes time on an HPC (then any run takes also time). What sort of test can be made in this case?
  - If the testing takes a long time perhaps it can be done asynchronously? (over night or on a branch)

- Can we add to the repo what we added in the hooks (so collaborators share the hooks)? Is it possible to push to GitHub for example?
  - I probably misunderstand the question but we added this:
```
#!/bin/bash

pytest example.py
```

- Is the name `pre-commit` important to the functionality? If so, what other names exists?
  - Yes the names are important and for other samples have a look in `.git/hooks`, also see: https://coderefinery.github.io/git-collaborative/05-hooks/

- How do we locate (which line) errors in big code chunks ?
  - If you have a "trace" like the one below, then I typically read it from the end up. So first question: when you experience an error, do you see a "traceback" like the one below?

- Within conda with pytest installed:
```
  $ pytest -v example.py
Traceback (most recent call last):
  ...
  File "/usr/lib/python2.7/dist-packages/pytest.py", line 13, in <module>
    from _pytest.fixtures import fixture, yield_fixture
  File "/usr/lib/python2.7/dist-packages/_pytest/fixtures.py", line 842, in <module>
    class FixtureFunctionMarker(object):
  File "/usr/lib/python2.7/dist-packages/_pytest/fixtures.py", line 844, in FixtureFunctionMarker
    params = attr.ib(convert=attr.converters.optional(tuple))
TypeError: attrib() got an unexpected keyword argument 'convert'
```
  - Browsing the net shows that this is probably a problem in an older pytest version. This was fixed in more recent pytest. If you are a Python developer, I would upgrade the Anaconda to Python 3. But I would not worry now too much if you are not because for rest of the exercises we can do without running pytest locally (it will be auto-tested in the cloud).

- Maybe the exercise boxes could have tabs for windows and linux?
  - Good idea!

- In windows 10, anaconda prompt: The command ...\pytest-example>move pre-commit.bat  /hooks gave this output: Access is denied. 0 file(s) moved.
    - This seemed to work: move pre-commit.bat .git/hooks

- Does creating a function test_someFunction() automatically try and find the someFunction() function and test it, because of its name?
  - No, pytest will find `test_someFunction()` and run it but you need to define what happens inside that one. Pytest will only check whether `test_someFunction()` ended successfully.
      - So, just a naming convention then, thanks!
        - Yes, it will run all functions starting with `test_`. But up to us to fill them with meaningful testing code.


### Exercise: full-cycle collaborative workflow

<https://coderefinery.github.io/testing/05-gh-actions/>

- [name=Matus] This was really fun, I felt like a sports commentator :D And it was no problem that we all worked on a different pace. It even self-organised itself into a nice loop, where x+1st person done with the issue, fixed xth person's bug (and the 1st waited for the last to close the loop).

- In GitHub actions I don't have python as an option.
    - scroll below to more workflow options button

- Is the workflow that we selected in github similar to what snakemake does locally? I mean is it comparable to submitting jobs?
    - I'd say it's sort of a different concept, github actions workflows are more like scripts that run things in sequence.  of course snakemake can do that, but snakemake is more about complex dependencies.

- instructions on how to do pull request would be nice (I do not remember anymore)


## Modular code development session

We will follow https://github.com/coderefinery/modular-type-along


### Questions to the audience


#### What does "modular code development" mean for you?

- Having several functions with one specific purpose which I can reuse across analysis steps / projects.
- Having many small modules of functionality that can be plugged together.
- Having several layers of code.
- classes , functions
- Separate interface from implementation in a way that allows the engineer to choose different implementations.
- Having the possibility of putting everything as a library that I can use in my future work or others can use easily
- API's and abstractions
- That I can copy-paste code into another project and it still works. That I can compose and combine. +1
- Having a lot of really small parts, that can be reused. Mostly it means calling functions inside bigger functions (sometimes can be slower in python, no problem in C/Fortran)


#### What best practices can you recommend to arrive at well structured, modular code in your favourite programming language?

- Use the abstractions provided by the programming language. Try to write generic code.
- create a lot of subfunctions which are generic (not specific to the analysis step you created them for)
- many functions with comments
- descriptive function and variable names
- Libraries


#### What do you know now that you wish somebody told you earlier?

- Design your workflow first on paper, in very detail. Create a flow chart, discuss it first, make changes, only then start programming.
- Think about the big picture but don't try to do everything from the beginning, start with something that works, then build on that to get to the more general functionalities of the code instead of trying to plan EVERY aspect of the code from the moment you write the first line.
- write pseudocode before starting to code, or workflow diagram, add this later also to documentations
- code can be always improved, just do something which is not maybe ready now, but comment it well so that someone can benefit from my code.


#### Do you design a new code project on paper before coding? Discuss pros and cons.

- I only started now doing it. It takes a lot of time..
- It depends on the complexity.
- It's often difficult to anticipate all aspects beforehand.
- I can do that, but not always the best way, since other people in bigger projects can have different ideas or habbits.
- yes! or whiteboard is even better, if its for a 'client' I also do that together with them or show it to them (simplified version depending on person) before starting to code to avoid misunderstandings


#### Do you build your code top-down or bottom-up? Discuss pros and cons.

- Bottom up allows early testing.
- With top-down you have the overview and can get a more efficient code.
- Both, sometimes building framework and then fillin it in with features and functions. Sometimes implementing first functions and then combining those as functional app.
- top down, to keep big picture in mind


#### Would you prefer your code to be 2x slower if it was easier to read it?

- Readability and Performance are not necessarily opposites. See e.g. Rust. Modern languages should have the goal to compile readable code down to fast code, such that the developer does not need to bother with microoptimisations.
- If there is an optimized and unreadable part of my code, I want to be able to test it against the unomptimized but readable version.
- It depends on what 2x slower means. If it's 1 minute instead of 2 it's ok, if it's 2 weeks instead of 1 month, then I'd prefer the speed
- I would prefer it to be faster. I could then document it better to facilitate readability.
- 2x is not bad, but I see no contradiction here, unless we go to extreme obfuscated-c.
- Depends on in which language it is. E.g. programming on GPU is a different discipline, there probably speed is more importany. On CPU code, readability is preferable.
- If speed is essential, then no. If not, then yes.


### Comments during live-demo

- sorry I misunderstood, do we type-along now?
    - Probably it's best to watch, it will go fast.

- make a method from each commented section
  - Great suggestion!

- Why `python -m env env`? Which one is the name of the environment?
  - The second is the name chosen by me.

- Does python -m venv venv activate automatically the environment?
  - It does not, activating is a separate step (which I forgot on stream)

- What about reading a _config_ file which contains the number of repetition? i.e. 25, 100, 500...
  - Great suggestion. Either config file or a command line interface (or both).

- Read input csv data only once.
  - Great suggestion. I was reading it multiple times which would be a problem for large files.

- By the way, the file has a header, so when we import `25` measurements via `csv` package aren't we really importing `24`?
  - Thanks! I need to fix that.

- Just a comment: very nice to see this! It is like what I would normally do on a working day, nice seeing it done live!
  - :-) I am wondering whether it is useful but hopefully managed to bring the approach and thinking across.

- How to get the cool feature that when you type in the terminal, there is a updating hint of the previously typed command/frequent used command? is this terminal-dependent feature? I use iTerm under MacOS.
    - I think he is using this: https://github.com/denysdovhan/spaceship-prompt
    - [name=Radovan] I am using https://fishshell.com/ with https://github.com/oh-my-fish/oh-my-fish, customized like this: https://github.com/bast/config/blob/04d7c8733c6a249ac4d64e9f93a928f1818d0166/install.sh#L7-L14. I really like that fish has context-aware history and great autocomplete suggestions functionality.
    - Thanks a lot,[name=Radovan]! :thumbsup:

- How to take care of function overhead if we have many functions? Takes time to call, keep stack, ...
  - If there are too many functions, you can organize them into separate files (modules).
  - Ah it's about the call overhead. I would only worry about this if the profiler shows me that I spend significant time in calling functions. Only then I would do something about it. One can then "inline" functions and other tricks.

- In `compute_mean`: `len(temperatures)` --> `len(data)`
  - Thanks! I missed that :-)

- What should I test? Should I always aim at testing all my functions? Should I prioritize some functions over others?
  - I would not test all functions but would test those that are non-trivial or broke recently. Sometimes you know what a function should do but don't know yet how to program it and then you can start with a test and it will inform you once you are done with the implementation.

- How should I handle tests when performing exploratory analysis?
  - If I can start with a test, I do. But sometimes it's difficult and then I add them later only for the non-trivial code.

- you forgot to change the second temp... to data
  - thanks - indeed :-)

- this Click looks really nice!
  - I like that with Click I can define command line options very close to where they are used.

- How to import files into other projects folders?
  - You can import modules (files) within a project by having them in the same folder.
  - But importing across projects, you could organize them into packages and publish the package on PyPI or Conda, but also possible to pip install from github.

- can you quickly summarise why you used click?
  - You mean why adding a command line interface? To be able to configure the code without changing it.
  - If this question is about why Click and why not Optparse or Argparse or Docopt - then just personal preference :-) I like that with Click I can define command line options very close to where they are used.


## Feedback

One good thing and one thing to be improved.  Focus on how to improve.


### About our material

- extrememely well organized, easy to access and understand
- Fantastic workshop, well organized and very useful
- Material was great, I really liked that you had examples within your lesons to type along
    - +2
- .Comprehensive material covering the major topics addresssed
- Too Python- centric.
  - [name=Radovan] We have the ambition to make this more general. I admit right now it's too much focused on Python but we thought that if we need to show something specific, Python is probably the easiest to read/ even if one hasn't seen Python before. But would be nice to offer more examples which one can pick depending on language/background.
- Good: everything is there ready to be run. Improve: I cannot think of anything.
- In general, really good! Especially the type along sessions and the last session were excellent.
- Material is excellent! Will share it in the lab and use it as primer
- Material was great! Very comprehensive.
- I believe the workshop videos will be available on youtube permanently.
- Very well prepared, documented, organized and explained course as a whole. Thank you.
  It would be nice to have quick 'catch-up' sections on lessons if something was missed during the lesson. Just the listings and scripts, if possible.
 - Great material. Easy to follow and a great asset for future self-study.
 - I wasn't always sure if I have installed right packages and enviroments. Also, quite many commands differ between windows and unix and the unix version was in material but that was fine for me. On the other hand, usually if something was missing, it was easy to install with pip before doing exercises. Overall, the material was good and it was very easy to use in breakout rooms.
 - Very well structured and prepared material. I will definetly revisit it. Many thanks!
 - Excellent material and well organized. Develop: some topics would have benefit form 101-primer before jumping to full speed.
 - Perhaps slightly less material and longer breakout room sessions could be one way to improve.
 - In type along, it would be beneficial if the command history could be seen from a separate window (or split the command window into too parts). Now it was too easy to drop if you missed command or two.
 - In one of the first days, there was a point in the exercise that you could clone (download) the right answer to the exercise so that you were able to continue even if you got stuck earlier. This is a great property!
 - In general, the material was very good. Week 1 (Git) went very smoothly. Perhaps including .gitignore into practicals would have helped for week 2. Week 2 was a bit more patchy because some concepts were qualitative (sharing code, licences, etc) and others quite advanced, with little background offered (snakemake). It was not so helpful to discuss for 10min how we write manuscripts (we all use overleaf) when lots of my group got stuck on snakemake because they never use makefiles in practice and didn't know what they are, how they work, how to write one, and why they would use them. The cyclic exercise on automated tests (Day 6) was also a problem: circular pattern of forking confused a lot of my colleagues, and forced idling while people caught up. Exercising in pairs would enable people going at a similar pace to progress faster. We never got to discuss constructing tests, which is also important. Perhaps cutting a bit on introductions (quite basic) and some discussion would free up more time for group exercises, which were a great hit. Lastly, congratulations to the organisers and instructors - this is an impressive event and resource.
 - the material was a tiny bit conda-centric. None of the people in my group use it, and we found the instructions with virtualenv but it tooks us a little longer to complete the exercises. Maybe some introduction to virtual environments would help.


### About the day-to-day mechanics (registration, breakout rooms, helping)

- Breakout rooms was an enjoyable part of the experience. I learned a lot from group discussions
- Registration and helpers both very good. Sometimes the breakout rooms were quite silent and without much collaboration, maybe this can be avoided with some informal ice breakers or something within the group...
- Difficult to follow at the same time the zoom session, the training material (web browser), the chat and any terminal (or other browser) at the same time, on a small screen.
- The breakout rooms worked out very well. Useful with discussions
- .I think it all worked very well.
    - +2
- Breakout rooms were good! Very positive experience! Having the whole breakout room coming from a single lab, it helped also in building realationships with others.
- Add some quick breaks in between longer lectures
- The breakout rooms were the best. Without them the learning experience would have not been so good.
- I think the logistics of the course worked very well and it didn't feel like a massive workshop. I feel like I got all the personal interaction that I needed. However, I would prefer to attempt the exercises on my own first and discussing afterwards in the breakout rooms/exercise sessions. I felt that when one person shared the screen and did the exercise, the discussion became too centered around that persons solution, not general.
- Breakout rooms worked quite well. Our helpers were very dedicated and helpful. Team exercises, when we had to do it in coloborative way were the best. I wish more of these would be present.
- Everything went very smoothly. This was world class training. Helpers were excellent, even if they didn't always know the correct answer, they showed how to deduct the right answer. I noticed that when I started reviewing next day material on the previous day, I was able to follow much better what was explained. If all-learning is left for the teaching moment, I felt there were too much to absorb for one session.
    - I had the same experience on checking the material before the lesson
- Very nice way of working. Switching between lessons, type along and breakout rooms kept mind fresh.
- Excellent organisation, and well-chosen tools. At times, it was a little confusing to switch between browser material, HackMD, terminal, and zoom, but I do agree this makes for a dynamic environment. HackMD was at times hard to follow, but it was a highly flexible and fast solution to the required chat, and it is possible to use it as a resource later.


### From learners

- Try to explain "jargon" in one sentence before. Doesn't have to be too detailed, like "a snake belongs to animals".
- Include every tiny little step to the exercise description. Don't have to be visual. Maybe a drop-down: here are the veeery detailed steps for beginners :p
    - +1
- .I am not a python user, so I was not fully aware of what was going on, but it was interesting and educational anyway. I think this is something you are aware of though.
- compared to face-to-face workshops, I even think this was better due to the breakout-rooms making it possible to reduce number of participants per group. I prefer this format - especially when the organization is as spot-on as this.
- potential improvement (in part you did this already): stick with one particular small coding project which we keep reusing. avoids having to clean up 10 repositories, and may help holistic understanding
- for non-multitaskers, hack-MDing, coding along and listening at the same time can be a challenge
- The exercise sessions could be extended by default to be more than 20 minutes. There's always 'overhead' when groups get into the breakout rooms and when any issues arise there may not be really time to solve those.
- Personally, more type-along exercises would be good. Keeping a focus on a remote lecture breaks easily after while, especially when following all different feeds and related links.
- I would prefer a slower pace even if that means that less material in covered. Some of the lectures were great in participant interaction by having type-along exercises or discussions/surveys. Some sessions were a bit exhausting to follow, if the lecturer just breezed through the material.
- I liked the last session which concluded many topics we've learned during the workshop. More these concluding .
- This training was to the point for me. I was the right audience. I would have liked more exercise time with Helpers and CR personnel. Last day last break-out room exercise was superb, when we had both helper and CR in the meeting.
- - Based on the installation instructions, I had the feeling the anaconda prompt would be better than git bash in Windows. And so I chose Anaconda. However, during the workshop I got hints from CR personnel that some problems that I had would perhaps not be a problem in git bash. And that git bash can be installed in addition to anaconda. Perhaps you could give more information on this so that Win users would have a better idea on best practices.


### From helpers

- The installation instructions don't explain conda very well, it was unclear that one needs to make an environment, and some outdated conda versions work differently, but are still installed on our universities managed laptops.
- I think that the set up instructions (for linux) worked well, everything went smoothly when I followed them, and in case of problem there were pre-workshop sessions to ask questions. Great effort.
- Everything worked well. The idea of teams made the breakout rooms work very well. More time would have been useful in many breakout sessions (but there was usually enough time to get the main point, even if not complete all the practical steps). Especially the collaborative exercises were great in breakout rooms. It's great that the material remains out there for learners to revisit.
- Following the instructions was always enough to be able to run the sessions. No problems whatsoever (OSX). My team was almost always combined with some other, which was a bit unnerving at first, but as we got some work done, things were more comfortable. Maybe give a heads up before first combining teams & if combine, keep the combinatios as stable as possible.
- Sometimes, learners were complaining about having to go back to earlier lessons to check for commands ( for some everything was so new that they just could not process everything as fast as it was going, this is not a negative thing, just something to keep in mind, memort capacity is limited with totally new things), especially because the amount of windows open during breakoutroom on one screen was bit overwhelming if you want to follow everything
- The workshop was great! The installation instructions to prepare for the workshop were very detailed. The only issue that I noticed is that in the instructions doesn't say explicitly that conda is a requirement, it only shows it as an alternative to pip, to install some of the other requirements. The instruction material was very good! Even if a person is not able to finish the exercise during the breakout rooms it is possible to go back later and do the exercise at their own pace. Because of the many operating systems and configurations necessary to install the requirements, I have a suggestion: preparing a virtual machine with, for example, a lightweight linux distro with everything properly configured. With this, people that were not able to install everything on their computer could download this virtual machine as an alternative to do the exercises. Instructions on how to use/install the virtual machines, would also have to be added to the software installation instructions, but would be easier to deal with during the ongoing workshop.


### From people watching the stream

- Thanks a ton, guys! I originally intended to sign up for this, but put it off as I am mostly working alone and do not really know where to find a group. Then I was working against a deadline and completely forgot about signing up. Fortunately you were streaming! :) One thing to keep in mind is that the stream resolution was 720p. While most text was easy to read, some of the finer print on webpages did not show. A different thing is about hack md. I am not sure whether it would "blow up" if you shared one single page for everyone, but that could perhaps be done (like yesterday on day 5). All in all, I would say a workshop like this would be useful for me every 3-5 years. While I have been doing software development and used some of the tools you presented, most of them had features I was not aware of that I intend to incorporate into my work. Also, having us actually do the implementations is much more effective for learning than just following along. I have previously been on a live CSC workshop on using their computing cluster, but I think this online format is better.
- Thank you very much for streaming and sharing this workshop! The course material is really good, and the fact that the course and the lessons followed the material so closely made it very painless to follow remotely. I got even more out of this than I expected and will definitely start using a lot of this stuff in my work.
- One thing to that could perhaps be improved from my perspective is that three hour intense lectures with type-alongs and many different topics is very draining. I would prefer two hour lectures spread over more days or even two hours in the morning and two in the afternoon, but these preferences are of course different for everyone:)
- All in all, thank you for a great course!


### From instructors and CR staff

- Some sessiosn were more of a "show" than training but overall fantastic instructors.


### Other topics/workshops/lessons you are interested in

- yes more workshops! +3
- More on modular coding
    - +7
- Docker containers +4
    - This sounded like something that would be useful for personal computer upkeep/restoring as well
- As I was relatively familiar with git already, I would have wanted more on the other topics, especially modular coding, documentation and automated testing. This functioned as a good starting point however, so not wasted. And git section also had something new. Maybe there could be a "getting familiar with git" part first for those who are completely new to the topic.
- idea: this type of workshop (maybe even in an extended form) would be the ideal kick-off for most natural-science PhDs. If it would be possible to offer this as a course I believe many PhDs would have a smoother experience during their later time
- Tried to containerize environment but better specs and tests are needed. For instance, I didn't test conda environments and they didn't work.
- Maybe bit more on automated tests, this was very short intro to the topic.
- Is it OK now to remove GitHub repos which were either forked, or someone was forking during exercises? Or is there "archive" where to hide test repos?


### Can you join us in [CarpentryCon2020@home](https://2020.carpentrycon.org/)?
- We sent a [proposal of a panel session about this Mega-CR workshop](https://github.com/carpentrycon/carpentryconhome-proposals/issues/32). We would like to invite you who are interested in joining as a panelist to present your experiences as a helper, learner, or as a viewer of stream.
    - Also, if there is a high interest, there is a plan to submit a proposal for either informal meetup or breakout discussion for Carpentries instructors, instructors-to-be, or anyone interested in Nordic countries.
    - Please contact to Naoe if you are interested in knowing more details, or comment in that issue linked above.

- I believe the workshop videos will be available on youtube permanently.
    - Correct: https://www.youtube.com/channel/UC47aupE7HKGduAjXKt1Gwrg
    - There will be a playlist of them

- Is to still possible to join this hpc course?
    - Please sign up here: <https://scicomp.aalto.fi/training/scip/summer-kickstart/>
    - We are about to decide how to handle everyone, I guess worst case we direct extra people to the stream.  But do sign up!
