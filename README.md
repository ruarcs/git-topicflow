My Modifications
=======

I have added the idea of "topic branches", which are short-lived branches to support long running feature branches.
We use HubFlow to create feature branches. These can be a short-lived branch (such as a bugfix into develop), or a
long-running one (such as a project that goes on over several months). In order to support the latter we have added a
new  category of branches: "topic branches".

New calls:


`git hf topic [list [<feature name>]]`

*  Gives a list of available commands, OR
*  Lists the current topic branches associated with a feature. Uses the current feature if we do not specify one,
   or takes an feature name, minus the <i>/feature</i> prefix.


`git hf topic start <feature name> <topic name>`
 
*  Creates a new topic branch from the given project branch. The project branch <b>must</b> exist. If the name of
   the feature branch is <i>feature/myFeature</i> then we should just give <i>myFeature</i>. The name of the newly
   created topic branch will be <i>topic/$FEATURE/$TOPIC</i>.


`git hf topic rebase [-i(nteractive)] [<topic name>]`

*  Rebases the topic branch against the feature branch it is associated with. Begins interactive rebase if given
   <i>-i</i> as an argument. Uses the current topic if we do not specify one,
   or takes an topic name, minus the "topic/$FEATURE" prefix.


`git hf topic checkout <feature name> <topic name>`

* Checkout the topic branch. You must specifically give the feature branch name so
  that no confusion occurs between similarly named topic branches on different
  features.

  
`git hf topic cancel <topic name>`

* Abandon the topic branch, deleting it locally AND on Github if it has been
  published. The name <i>must</i> be explicitly supplied.
  
  
`git hf topic finish [-{k(eep)
                       i(nteractive rebase)}] [<topic name>]`

*  This command will:
   1. <i>rebase </i> against the feature branch, interactively if this flag is specified.
   2. <i>merge --ff-only</i> the topic branch into the feature 
   3. close the topic locally AND remotely, <i>unless</i> the keep flag is specified.
 
  
  
<i>The reason that we do a merge --ff-only is that we always want the history in the feature to remain linear.
This significantly reduces the level of complexity in the network graph later on when we merge back to develop.</i> 

HubFlow
=======

Adds the 'git hf' Git extension to provide high-level repository operations
for [DataSift's HubFlow branching model](http://datasift.github.com/gitflow/), which is based on [Vincent Driessen’s original blog post](http://nvie.com/posts/a-successful-git-branching-model/).

![](http://nvie.com/img/2009/12/Screen-shot-2009-12-24-at-11.32.03.png)

Installation
------------

1. `git clone git@github.com/datasift/gitflow.git`
2. `cd gitflow`
3. `sudo ./install.sh`

Windows users will need something like Cygwin in order to use this extension.

Upgrading To The Latest Version
-------------------------------

Upgrading to the latest version of the HubFlow tools is very easy:

1. `sudo git hf upgrade`

Getting Started
---------------

See our tutorial website to learn more about the [GitFlow](http://datasift.github.com/gitflow/IntroducingGitFlow.html) branching model and [how to use the HubFlow tools](http://datasift.github.com/gitflow/GitFlowForGitHub.html).

Changelog
---------

To see what's new in each release, see our [Changelog](http://datasift.github.com/gitflow/ChangeLog.html).

License Terms
-------------
HubFlow is published under the liberal terms of the BSD License, see the
[LICENSE](LICENSE) file. Although the BSD License does not require you to share
any modifications you make to the source code, you are very much encouraged and
invited to contribute back your modifications to the community, preferably
in a Github fork, of course.
