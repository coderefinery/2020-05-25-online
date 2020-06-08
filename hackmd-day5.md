---
permalink: /hackmd-day5/
---

# day 5


## Questions from day 4

* Several times "FAIR" was talked about, but I still do not understand
  what this entails, and I guess that many use this word without
  realizing what there is behind. Are there worshops on the subject?
  If not, do you plan to prepare one?
  - I see FAIR as the latest buzzword for "things needed to be open"
	(edit:), though advertised in a more moderate way, saying you
	should be appropriate to the circumstances +1
	- I agree although it does not have to be open to be FAIR. Also it
	  took me a while until I found out that "R" does not stand for
	  reproducible.
	- R is for Re-usable, isn't it? I can't imagine reusable without
	  being open (4 rights). Or am I missing something?
	  - I agree, I also don't see how this can work in the long term
		without being open.
  - There is FAIR data and FAIR software. There are many workshops and
	material on the former, much less on the latter. It would be good
	to co-organize an event focusing on FAIR software.
  - Nice website with very brief summary: https://fair-software.nl/

* In the spirit of the "10-year challenge", if I forget the stuff that
  I learned on this course for a couple of years and the decide to
  start using, for example, git can I still find the course material
  somewhere (lecture web pages, hackmd, recordings to youtube)?
  - The HackMD discussion are added to the workshop page and we will
	keep them.
  - The lesson material will also stay online with its history but we
	haven't been disciplined creating "releases" to tag certain
	versions (since the material evolves). One thing we plan to do is
	to make the lessons citable using Zenodo and this way they will be
	preserved "forever", also with well-defined versions.

* Concerning the citing of code and software in a scientific
  article. Let's say that I use a code from some repository in Github
  in my article. Is there a standard way to cite this in an article or
  is it currently case by case depending on how the developers of the
  code want to be cited? Can you cite a code in an article similar to
  citing articles and does, e.g., google scholar calculate the number
  of citations that some software has received? Of course, if the code
  is published in an article then it is clear. But if I share some
  code do I need to publish it in an article to be able to collect
  citations for the code if people use it. Sorry for the many
  questions; I am just wondering how to be able to show some
  statistics for financers or in my cv etc. on how many people have
  used my code in their research. Would this be good option, at least
  it is very clear: https://github.com/dftlibs/numgrid#citation
  - great questions! To collect some metrics over time a DOI is a
	minimum. I use Zenodo for this but other alternatives exist. Later
	one can also publish an article focusing on the software aspect
	for instance on JOSS or JORS or SoftwareX. I think articles still
	matter more to hiring committees and the community is more used to
	citing articles. About the citation format: you could refer users
	to Zenodo where one can select a journal format and it will show
	the recommended citation text but I think it's still nice to make
	it as easy and as few steps as possible for readers/users to see a
	recommended citation. Sometimes I put this even into the code
	output when I am not sure the users will even visit the GitHub
	page. So when they browse the output for some result, they also
	see how to cite it. I am not sure there is one standard way to
	write the recommended citation and for this I shared a bibtex
	entry but it's not always correctly formatted. In short, I think
	users will cite the code if they don't have to do a lot of
	searching and a DOI is a must to be able to measure metrics. Of
	course there are also other metrics like whether other codes refer
	to your library (PyPI, conda) or download stats but not sure they
	matter and also they can be artificially high when the code is
	used in nightly tests, etc. Sorry for long text.


## Day 5 introduction

### Icebreaker: What's a good icebreaker question?
- What's a good icebreaker question?
- How is the weather where you live?
	- Helsinki: sunny!
	- Tampere sunny! :sun_with_face:
	- Sunny 30 km west from Helsinki! <- 40 km further as well :)
	- Bergen cloudy but mild
	- Sunny in Espoo too!
- Nice weather today! Shall we go out instead of learning cool stuff?
  :smile:
- Have you already used what you have learned in the course during
  your work? If so, what?
	- Yes, Git! My project is now a repo on GitLab.
- How are you doing?
	- well (this must be answered with an adverb, not an adjective)
	- yellow
- Are you happy to continue this workshop for another week?
	- yesish
	- yes, yes,yes!
- Is that an Iphone?
	- NO!
- If you could have anything what you want for dinner today, what
  would it be?
	- pizza!
	- gazpacho
	- salmorejo
	- makkara! (=sausage) :D
	- Weißwurst, Leberkäs and Brezeln with sweet mustard
		- einmal bier bitte auch?
		- +1 +1
- What cool thing/tool have you discovered/learned the past days?
  (independently of this course)
	- we have different types of bumblebees in the garden
	  (black,white,yello and black orange) and they actually live in
	  holes in the ground o.o
- Is this course part of your work? Or do you spend free time on it?
	- what is free time? (PhD student)
- Do you like olives?
	- Yes, I love green olives!
	- Yes :-)
- What's a good icebreaker question?
   - For example what would be a good icebreaker question.
- Are you annoyed at the size of anaconda
	- The actual snake or the download package? The snake can be
	  around 9 meters!
		- the software yes!
- What's your favourite pizza?
- Do pineapples :pineaplle: belong on pizza?
	- Yes!
	- ...*shaking head*
	- ... oh dear :)
- What did you have for breakfast?
   - Leftover pizza.
   - exploded eggs
- Do you like Python?
	- Yes <3
- Where’s your favorite place to nap?
	- Armchair
	- garden
- Do you use git or identify as one?


### Questions from previous days

- Unrelated: What is Anaconda actually for? In the coderefinery
  workshop it's introduced as a tool for managing dependencies, but
  their website is all about data science, etc.
	-  Anaconda is technically a for-profit company which deals with
	   data-science and things. They develop (maintain) a wrapper
	   around `python pip` which is `conda`. `conda` is essentially
	   `pip` with support for installing non-python dependencies. This
	   means that it is able to install some other language libraries
	   (like C++). Anaconda in particular refers to the `conda`
	   distribution which comes with a lot of packages installed in
	   advance. Miniconda is `conda` without many dependencies. Sorry
	   for the wall of text.
	- Thanks! this is very helpful! One more question - when they say
	  it can be used for other programming languages, does it mean it
	  can be adapted to anything or is there a specific list?
		- As I recall it mostly works for libraries (like say, BLAS,
		  which is in Fortran) but I should check.
	 - ok, to sum up: conda is a fancy tool for managing dependencies
	   and Anaconda is an environment on top of it. They talk about
	   data science because it started with python and data scientists
	   love python. Is it correct?
		 - Yup :+1:
	   - If your code is Python, then PyPI is a standard place. There
		 are also packages on PyPI which are written in something else
		 than Python but have a Python shell around it. But for
		 packages/libraries which are not Python packages, i.e. C++
		 libraries, C stuff, ..., they don't fit so well into PyPI and
		 then Conda can be a good way to package them and to track
		 dependencies. But it's also OK to put a pure Python package
		 on Conda. Some project place things on both PyPI and Conda.
		   - If one wants to maximise exposure, it's considerable to
			 provide packages in all these 3: pypi/cran/etc., conda,
			 and debian
			 - But doing this can also be quite a lot of work and
			   overwhelming for many researchers. But I agree that one
			   may need to share packages on multiple platforms (there
			   is also Spack and EasyBuild for more HPC-oriented
			   codes).
	- Anaconda actually has fundamental problems since it almost, but
	  not quite, is a container. It typically replaces some, but not
	  all, of the libraries of the host OS. An HPC cluster, for
	  example, typically provides its own version of MPI. This may not
	  correspond to the dependencies of, e.g., mpi4py in the Anaconda
	  environment. This may lead to very strange problems where
	  different, incompatible versions of a library are loaded. In my
	  view, one should choose between being a container (in which case
	  *all* dependencies should be provided by the container system)
	  and not being a container, in which case host libraries should
	  be used to the greatest extent possible.


## Documentation
<https://coderefinery.github.io/documentation/>

### Motivation and wishlist
<https://coderefinery.github.io/documentation/01-wishlist/>

#### What is good project documentation?

- The code should be well documented so that it can be understood when
  coming back to it. The structure of the project and data should be
  well described. This enables us to come back to the project after a
  lot of time has passed. Also it makes it more transparent to others
  who may wish to replicate the science or review it. Argument for
  collaborators: Good documenting from the start will make the road to
  publishing smoother.
- Some written document which provides "sufficient" information for my
  future me and other potential users/developers
- Regarding code documentation, some things can be documented by
  comments in the code, but having a document explaining general
  structure of a code and the concepts involved makes understanding it
  a lot easiser.
- Something you'll hardly find...
- Maybe add FAQ if you have enough users.
- Concise, not write-only!
- Explanation of what the code does, what are inputs/outputs as
  minimum
- Quick start guide on how to use the code
- Explaining magic numbers if they exist
- Clearly describes, what each function does, what are limitations and
  requirements for dataset.
- Appearing where users need it, in relevant concise portions: short
  text where applicable (in GUI and CLI - like git), --help options in
  CLI, mouse-over hints in GUIs
- Concise explanation of input, objectives, method and output
- Documentation with comment, commit and pictures.
- Comprehensive enough to also include various mistakes, issues in the
  data etc. one has rectified during the project. Sooner or later you
  start wondering about the same issues again and then it's helpful to
  check from the project documentation how they've already been
  figured out.
- Explain exceptional things in the code, not obvious things.
- Has a possible use example
- Explains what format of data and from what source it uses - this
  helps when coming back after 10 years.
- The better the documentation the less amount of people will ask
  basic questions about the code
- comment your code every second line
- don't assume implicit pre-knowledge


#### Wishlist for documentation
- How to make it compile and run
- How to use it in a basic form and where to look for advance use and
  modification
- References to algorithms/publications within code
- Not a mere description of the code or inputs/outputs but some
  explanation as to why/how things were done that way
- quick start guide on how to use the code (in its basic usage)
- 101 (what it is, why useful, where to start, ...)
- example piece of code to see
- Contain a test suite, demonstrating all features and testing them.
- installation instructions
- Coding variation in different languages
- Wiki, if possible on a platform.
- Hardware/software requirements (library versions etc.)
- one script showing major usecases of the projects
- Badges about test coverage, CI build status, available
  documentation, DOI etc. As a quick overview on the top of the
  README. This makes a good impression if there.
- Contains information about package versions
- Description of the code and the input/output files.
- Simple examples, ideally with images and test results.
- Short README file as introduction. Extensive documentaiton can be
  moved to wiki or ReadTheDocs.
- input and output clearly explained
- Has some demonstration with example data
- dataset download and preprocess
- references to papers and theory
- A tutorial
- A good and short summary of the documentation
- Documentation of classes and methods

### Popular tools and solutions
<https://coderefinery.github.io/documentation/03-tools/>

- what is markup / markdown? Very general explanation, please.
  - Markdown is the markup that we use in this document. "Markup" is a
	set of conventions for how to "mark up" lists (here using dashes
	or stars), paragraphs, tables, images, equations, code blocks.
  - Example: https://commonmark.org/help/
  - Thanks! Would be nice to explain in one sentence before what
	markup means, so everybody can follow.
  - If you are familiar with LaTeX, then LaTeX has its own conventions
	on how to "markup" tables, bold text, emphasized text, paragraphs,
	sections. So it's a bit like that.
  - Not yet, but thanks for the link.

- if I want to use markdown for documenting r code is possible to
  include this in git hub without having a paid version, which other
  alternatives are?

  - Are you using R Markdown and is the question about where/how to
	render HTML generated from the R Markdown?
  - yes, i would like to share my reports with my collaborators
	  - There is no need for a paid plan! RMarkdown is the best, you
		can use `bookdown` to create large, performant sites of
		documentation [like
		Stan](https://mc-stan.org/users/documentation/) and you can
		(as mentioned by Radovan) use pkgdown or the ROpenSci
		templates for packages (if your package is approved). CRAN
		also have great support for Vignettes (if you are making a
		package). There are some great links in yesterday's material
		on reproducible software (`rrtools` was mentioned I
		believe). You can also just directly share the generated
		Markdown in a repo. That will work too.
	- Not an R developer (so I haven't tried this yet) but I would use
	  GitHub Actions to generate the HTML and serve the result via
	  GitHub pages. Something inspired by this:
	  https://ropenscilabs.github.io/actions_sandbox/websites-using-pkgdown-bookdown-and-blogdown.html. I
	  am confident it can be done without any paid plans. If you like
	  we can look at it together later. Any R developer here who has
	  tried this and has an example? We will discuss GitHub Actions
	  tomorrow so it may make more sense then.

- Doxygen
	- no complaints, just a bit ugly template by default when compiled
	  in HTML format
		- Only the default though.. [this
		  is](https://docs.dseams.info) not too bad
			- thanks, that template is real nice!
	- Seems to be mostly used in the C++ community? Usually all
	  languages come with their own documentation generator, right?
		- There are (to my knowledge) no language-level specifications
		  for documentation, but different communities gravitate to
		  different tools. The JS community (or the React users) tend
		  to showcase components and so their documentation is
		  slightly different, and the same situation is reproduced in
		  other communities as well. Doxygen and Sphinx are more
		  geared towards being generalized (which is great)
	- Doxygen is fantastic! It uses an extended comment syntax and is
	  mostly used for R and C++, though it has extensions for Fortran
	  as well. That said, it's a nightmare to work with locally, since
	  things vary across versions. It hooks up nicely to continuous
	  integration systems like TravisCI and the output can be styled
	  well as well. It also gives you free HTML and LaTeX files.
	- Doxygen can generate a graphical interdependency tree between
	  program components (modules, subroutines), that can be difficult
	  to track by other means.

#### What do you use?

- I always end up starting with comments and some markdown, which
  later becomes Doxygen (for C++, Fortran, and R). I've *never* used
  ReST, though the pipe table syntax is neat. Mostly I use a lot of
  `pandoc` while going over documentation from other projects.
- I start with a readme file (rst) in every project (infrequently
  splitting to several files), later expand to sphinx if it is needed.
  Usually hosted on readthedocs.
- .txt
- rustdoc for Rust projects. They have a webservice that automatically
  builds rustdoc from published rust code, which is very useful.
  - Ah another Rust developer. Nice!
- Wiki on Git-hub (my project is on Linux mainly).
- .txt, which actually has very similar syntax as md (as I have now
  learned)
- README.md and README.rst for small projects (I tend to prefer the
  latter because it can autogenerate a table of contents which can be
  useful for longer READMEs). For anything that grows out of README
  files I use Sphinx and Read the Docs to serve the HTML
  documentation. Rustdoc for Rust projects.


### Sphinx and restructured text
<https://coderefinery.github.io/documentation/04-sphinx/>

#### Exercises: Sphinx
<https://coderefinery.github.io/documentation/04-sphinx/>

- Separate source and build directories (y/n) yes or no? I missed it.
	- no (we use the default here)
	- the exercise instructions didn't work when separating the source
	  & build. A pity this hasn't been emphasised in the beginning :(
	- what if you use yes (I think the recommended way for future was
	to separate the source)? how to use sphinx-build in this case?
	The command is :`sphinx-build source build` . Here `source` and
	`build` are subdirectories. You edit the rst file in the `source`
	subdirectory. You will find the index.html in the subdirectory
	build after the build is complete.


- The LaTeX creates permalink on equation number (visually $Pi$), is
  that compulsory or can avoid creation of those permalinks?--> now I
  read the last line, removing the label did the trick!


### Break
until xx:30


### Deploying Sphinx on ReadTheDocs
<https://coderefinery.github.io/documentation/05-rtd/>

- **FYI:** this is the same word-count repository we used in the
  reproducibility lesson yesterday
- Can you have a private repository and a public read docs webpage
  reffering to it?
  - Yes. Several options: either a paid plan, or you separate your
	repository into a public one (containing the master branch for
	instance) and a private one (all other branches) and Read the Docs
	builds the master branch (downside: perhaps you want to also have
	documentation for some unpublished branch), or you make Sphinx
	part of a GitHub Actions workflow (more about that tomorrow) which
	builds HTML and then you deploy the HTML yourself to GitHub Pages
	(or you do the same on GitLab using GitLab CI and GitLab
	Pages). Another option is to host your own Sphinx server if you
	don't want to use Read the Docs nor any of the GitHub/GitLab
	pages.

### Discussion

- If I want to only update the docs on a new release, but commit doc
  changes to my repo before that release, how do I prevent read the
  docs from updating, or make it update only on new releases?
  - You can tell Read the Docs (RTD) to build several versions based
	on branches or tags. You could have one version which renders
	`master` and another one that depends on a release tag. But maybe
	what you wanted was to not show documentation for unreleased code
	at all?
	- Possibly, yes. Might be confusing if the *latest* version of the
	  docs is not the latest released version.
	  - You can redefine what "latest" means and also make your
		released version the default one and make "master"
		non-default.
	  - Alternative would be to use GitHub Actions and only run the
		Sphinx step upon release/tag creation but would not be worried
		of showing too much documentation if it is clear what is
		latest and what is experimental and what is stable and you can
		define these on RTD.

- any use for the old gh-pages special branch?
  - gh-pages is a special branch name which will tell GitHub to create
	a webpage from the repository
  - this is covered in this lesson episode:
	https://coderefinery.github.io/documentation/06-gh-pages/

- Is ReadTheDocs alternative to GitHub wiki pages? Should I bother to
  write both of them? If yes, doesn't it fragment informations in many
  different places?
  - Good point. RTD is an alternative and there are many other
	alternatives. I would avoid fragmentation. I am personally a bit
	worried about wikis since they can have a disconnected history. So
	I would probably prefer a solution that goes with the code in the
	same repository. So that you can branch it and also go to some
	past version and rebuild the documentation as it was back then
	(reproducibility!).

- It worked and was really nice to click along the rtd demo!
  - Glad to hear! It's a really nice tool/service.

- what happens if I add documentation to master branch after
  branching? Can I easily get the documentation for development branch
  also?
  - You could merge `master` into the development branch (then you get
	all commits) or you could `git cherry-pick` just one commit or few
	commits. I do that sometimes when I accidentally committed to the
	wrong branch but cannot modify their history anymore.

- When would you prioritise using sphinx/readthedocs instead of a
  simple README.md on github?
  - As soon as the README becomes hard to browse (too long, too many
	sections). For people who have never seen GitHub or READMEs, a
	readthedocs page can look "nicer"/ more approachable but it's an
	extra step and I often start out with READMEs and only move to RTD
	later if I really feel that the README is not enough anymore, but
	also it does not take more than 1 hour or so to set RTD up.
  - There can be situations where the README is not accessible
	(private repository).

- Should the code version and documentation version be the same (for
  clarity)? +1
  - Yes, and probably it is a good idea that different versions of
    documentation point to its respective code version.


## Break

## Jupyter
<https://coderefinery.github.io/jupyter/>

- What is the advantage of using "jupyter-lab" versus "jupyter
  notebook" command? The lefthandside menu?
  - Internally, it's written in a more modern way.  For us, classic
	notebook was a one-page, one-notebook interface.  jupyterlab is
	more like an integrated development environment. :+1:
  - Was that in the browser window that is now shown?
	  - Just asking, I am familiar with "jupyter notebook", but never
		used "jupyter-lab"
		- Aha the latter is newer and the idea is to extend a notebook
		  and make it look more like an integrated development
		  environment with easier file browsing, and plugins for Git,
		  GitHub, etc. But everything that works in the more classical
		  notebook also works in the JupyterLab. :+1:

- When I click on the Python 3 in Notebooks (in the Jupyter Lab), I
  get error "Launcher Error e.rendermime is undefined" :( (Anaconda on
  Win)
  - Hmm ... researching the error ... I see this:
	https://github.com/jupyterlab/jupyterlab/issues/6681, unsure how
	to solve it.

- What does `ØMQ` mean?
	- It's a message passing system used internally between Jupyter
	  and the kernels.

- There is a latex extension in the Extension Manager, what could be
  this for if it seems that LaTeX is already supported inside
  markdown?

  - The extension is for including `*.tex` files as part of what a
	jupyter notebook can process, not only LaTeX inside your
	markdown. You can go to the extension page to see more details
	<https://github.com/jupyterlab/jupyterlab-latex>

- Does it support bash code?
  - Yes you can run shell commands also:
	https://coderefinery.github.io/jupyter/04-extra-features/#shell-commands. But
	I would be a bit conservative when accessing local files with
	shell commands because once you publish the notebook and others
	try to rerun it, the files and hard-coded paths may not be
	there. But it can be useful for prototyping.

* C++ kernel: https://github.com/jupyter-xeus/xeus-cling
* running of the code in notebook does not work. Instead of [1] I have
  [ * ] on the left and no output
	* It is getting stuck in running the cell/kernel.  It will take
	  some debugging/screen sharing to see what's wrong.  Though, do
	  you see any messages in the terminal that started JupyterLab?


### First computational notebook
<https://coderefinery.github.io/jupyter/03-basic-workflow/>

Type-along exercise.

- Can one set the size of the figure using this code:
```![Darts](https://coderefinery.github.io/jupyter/img/darts.svg)```?
	- Most likely so, but I don't know offhand.  That's markdown, so
	  we can check markdown syntax for that
	- Also, one can usually do raw HTML to control things as you want.

- how do I interrupt an ongoing computation
	- "Interrupt kernel" from either the Run or Kernel menu.  It's
	  possible there might be a button on there.

- it's very hard to follow the demo with the constant scrolling and
  switching
  - I understand, too quick probably to really type/click along. In
	this case I recommend watching and only focusing on what can be
	done, the "how" is then described in the material in case you are
	interested in the functionality.

- I could not install the git extension, I keep having "internal
  error"
	- We will have to look at installation issues later
	- What version of JupyterLab do you have?

- What if I add to existing repo jupyter-lab notebook, does it
  recognize to be inside git-repo and git add, commit, push would work
  correctly?
	- git is just git, it looks at the directory to detect if it's a
	  repository or not, if it is, then everything should work.

- How to set up *credential helper* for JupyerLab-git? So that we do
  not have to input our user and password every time we push.
	-  you can set up an ssh key or an access token using the console
	   (as with a "standard" terminal).

- I started git init but in the jupyterlab IDE my git extension tab
  does not identify the directory as a git directory.
	- I would have to take a look, hard to say without seeing more.

- Can you please explain a bit more about `%%prun` in JupyterLab?
  i.e. What is profiling?
	- profiling is analyzing the program to see how long it takes for
	  each function/line/etc.  When you care about speed, you always
	  need to profile first to understand *where* it's slow.

- can you explain what is magic quickly?
	- jupyter doesn't just limit to Python: these magics can do
	  something with the cell itself.  for example, `%%timeit` runs
	  the whole cell and times the execution, which you *can* do in
	  just Python code, but it's convenient to be able to do these
	  special operations on code blocks.

-  on the extension manager page
   (https://jupyterlab.readthedocs.io/en/stable/user/extensions.html)
   there was some disclaimer saying something like "Danger: Installing
   an extension allows it to execute arbitrary code on the server,
   kernel, and in the client’s browser. The code may be
   dangerous. Therefore we ask you to explicitly acknowledge this."
   Wondering if this is really something to be taken seriously or just
   accept and continue..
	- It should be taken seriously, but if you are installing
	  well-known and well-maintained extensions, then it's safe
	  enough - just like installing things with pip/conda.


### Exercise: Jupyter stuff
<https://coderefinery.github.io/jupyter/05-exercises/>


- What is the difference between line magics and cell magics?
  - Found this again in the material:
	- Line magics: commands prepended by one % character and whose
	  arguments only extend to the end of the current line.
	- Cell magics: use two percent characters as a marker (%%),
	  receive as argument the whole cell (must be used as the first
	  line in a cell)

- How do we set/change the conda environment in the jupyter notebook
  terminal?
	- JupyterLab does not seem to pick up the conda environent used
	  when starting the application. Can you specify this inside
	  JupyterLab?
	- You need to install it as a "new kernel": `ipython kernel install
	--user --name nameenv python -m ipykernel install --user
	--name=nameenv`

	where nameenv is the name of your conda environment.

- The interactive exercise didn't work... just got a figure, no
  interactivity
  - This means that an extension was not installed or enabled (we have
	instructions in there for how to enable this). We have also seen
	cases where it was correctly installed but required restarting the
	Jupyter notebook/lab.

- We copied the solution for the first exercise (in the exercises'
  page) but it showed only a graph in the screen after executing the
  code (not interactive). `![](https://i.imgur.com/JwGPYh1.png)`
  - Possibly same as the point just above. We can also screenshare
	later and try to debug this.

- Does binder run things on their own server, or does it execute the
  notebook on the client?
  - Runs on their cloud servers. You can visit the page then even with
	your phone, without any Jupyter client, just a browser.
	- Who pays for that?
	  - Binder does, of course there is some limit so for really heavy
		notebooks you may need your own server (it's open source).
	  - Non-profit:
		https://mybinder.readthedocs.io/en/latest/about.html

- Is `binder` free?
  - Yes, see point above. It's also open source so you can run it
	yourself (your organization can), too.

- Is `binder` safe?
	- Yes. It creates a container (uses repo2docker)

- is binder inherently public or can I create a password protected
  notebook there?
  - My understanding is that it's public and if you wanted to control
	access, you would need to run an own binder instance
	(https://mybinder.readthedocs.io/en/latest/faq.html).

- Can I launch 'ipcluster start' on another of my computers?

- when I shut down jupyter lab, my command prompt seems to get
  stuck. I am using win 10 and Anaconda prompt. Ok, control-C seems to
  work...


## Feedback day 5

- Really interesting day. The only feedback I have is to make sure to
  explain concepts/jargon briefly before diving in. Also in exercises
  be clear to specify what we are expected to execute.

- Good material and training again. The documentation needs to in my
  personal to-do list as it is painful to read my own code after a
  half a year. Pro: Very interesting topics. Con: too short time to
  work on material.  -

- I really enjoyed the Jupyter, learned a lot and managed to do the
  exercises well, but for the documentation I think it was very slow
  to start with and then there was a huge flow of information making
  it difficult to follow. I will have to revisit the training material
  on my own.

- I liked the demonstration of whole process from srt to rtd, adding
  apidoc would have been a plus. Although this, the whole
  documentation section was a bit too abstract to me. I think a user
  will learn Sphinx (or another engine) once he/she has something to
  write. So, why can't we create the "need" to write documentation in
  ordere to teach it? An idea that came to my mind is to structure the
  whole workshop around the development of a very simple tool: in the
  first day listeners could come and start to write some code (even
  cloning from a template and just "fill in the blanks"). This, would
  generate the need of version control, so the opportunity to teach
  git and github. Once pushed to a repo, then, publicly available code
  calls for documentation, so, sphinx. To demonstrate the usage of a
  tool, then, a jupyter notebook could be implemented in order to
  share the analysis flow and so on. Of course there are limitations,
  such as some basic coding skills but the kind of people that attend
  these courses,usually know a little bit how to do it. I this this
  would make the course more interactive and could help in fixing
  ideas into listerners minds.  -

- General: It would be good to specify in type-along sessions and also
  exercise sessions which results will be reused later ( so if someone
  had trouble, he/she knows what he/she should focus on to make
  work). Both ways, so also mention/write if the results are not
  crucial for rest of lesson.
