## How to Edit Docs  

### Objective

Learn the process of editing docs by adding some content to a test document.

### Markdown, MkDocs, Mou

The Mynewt documentation you see on the Apache incubator website is a bunch of HTML files generated using MkDocs which is a simple static site generation tool geared towards building project documentation. You can read about it at [http://www.mkdocs.org](http://www.mkdocs.org). Documentation source files are written in Markdown, and configured with a single YAML configuration file. Markdown is a lightweight markup language with plain text formatting syntax designed so that it can be converted to HTML and many other formats using a tool (which in our case is MkDocs).

You do not need to install MkDocs unless you want to actually render your documentation in HTML in order to preview it before pushing your content to the remote repository. Typically, using a Markdown editor such as [Mou](http://25.io/mou/) is enough to check how it will look after the document has gone through MkDocs. Go ahead and download [Mou](http://25.io/mou/). If you are on a Windows machine, download the [editor of your choice](http://alternativeto.net/software/mou/?platform=windows).

Currently someone in the project is designated to use MkDocs to generate the HTML pages periodically after changes have been reviewed and accepted into the master branch.


### Access to the Apache repo

Get an account on Apache. You do not need a committer account to view the website or clone the repository but you need it to push changes to it.

If you are not a committer, you may follow the proposed non-committer workflow to share your work. The direct link to the proposed workflow is [https://git-wip-us.apache.org/docs/workflow.html](https://git-wip-us.apache.org/docs/workflow.html). You will find the steps described in more detail later in this tutorial.

### Making a local copy

* Copy the document source files into a local directory and look at the contents of the copied directory to get an idea of the directory structure. Use http instead of https if you are a non-committer.
```no-highlight
        $ git clone https://git-wip-us.apache.org/repos/asf/incubator-mynewt-site.git
        Cloning into 'incubator-mynewt-site'...
        remote: Counting objects: 330, done.
        remote: Compressing objects: 100% (263/263), done.
        remote: Total 330 (delta 120), reused 0 (delta 0)
        Receiving objects: 100% (330/330), 4.34 MiB | 830.00 KiB/s, done.
        Resolving deltas: 100% (120/120), done.
        Checking connectivity... done.
        $ ls
        incubator-mynewt-site
        $ ls incubator-mynewt-site/
        docs		images		mkdocs.yml
```
* Create a new branch to work on your documentation and move to that branch.
```no-highlight
        $ git checkout -b <your-branch-name>
```

### File to be edited

The file you will edit is named try_markdown.md. It is in the incubator-mynewt-site/docs/os/tutorials/ directory.

### Editing an existing page 

* Open the application Mou.

* Open the file incubator-mynewt-site/docs/os/tutorials/try_markdown.md in Mou.

* Edit the last item on the list.

* Save and quit the application.

### Adding a new page

If you create a new file somewhere in the `docs` subdirectory to add a new page, you have to add a line in the `mkdocs.yml` file at the correct level. For example, if you add a new module named "Ethernet" by creating a new file named `ethernet.md` in the `modules` subdirectory, you have to insert the following line under `Modules:` in the `mkdocs.yml` file.
```no-highlight
        - 'Ethernet': 'modules/ethernet.md'
```
### Pushing changes to remote as a committer

If you are not a committer yet, skip this section and proceed to the [next section](#sharing-changes-as-a-non-committer).

* Check whether your remote git repository is set up. If you see the remote location as shown below you can skip the next step.
```no-highlight
        $ git remote -v
        origin	https://git-wip-us.apache.org/repos/asf/incubator-mynewt-site.git (fetch)
        origin	https://git-wip-us.apache.org/repos/asf/incubator-mynewt-site.git (push)
```
* If, however, you do not see your remote repository, then set it up as follows.

```no-highlight
        $ git remote add origin https://git-wip-us.apache.org/repos/asf/incubator-mynewt-site.git 
```       
* First check the git status. It will show you that the `try_markdown.md` document has been modified. So you will stage a commit, and then commit the change. Finally, you will push the changes to the remote repository. 

  During staging below using `git add`, we use the `-A` option indicating you want to stage all your modifications. Instead, you can choose to specify only the files that you want to. The commit message (specified after `-m`) should summarize what your changes are about.
```no-highlight
        $ git status
        $ git add -A 
        $ git commit -m "My first doc change as a trial run"
        $ git push -u origin <your-branch-name>
```   
* You can see the changed Markdown file if you traverse the tree on the git repository [ https://git-wip-us.apache.org/repos/asf/incubator-mynewt-site.git]( https://git-wip-us.apache.org/repos/asf/incubator-mynewt-site.git).

* A commit notification automatically goes out to the commits@mynewt.incubator.apache.org mailing list. The "upstream" manager pulls the notified changes, reviews it, and merges it to the master branch if all is well. Otherwise you get an email for further changes.

### Sharing changes as a non-committer

We suggest you follow the proposed non-committer workflow at Apache to share your work. The direct link to the proposed workflow is [https://git-wip-us.apache.org/docs/workflow.html](https://git-wip-us.apache.org/docs/workflow.html). 

* Assuming you have made changes to the example file, you will first commit your changes.
```no-highlight
        $ git add -A 
        $ git commit -m "My first doc change as a trial run"
```
* Once you're ready to share your changes with the rest of the project team, you can use the git format-patch command to produce a patch file (or a nice set of patches in the future) and email the patch file to dev@mynewt.incubator.apache.org. Later on you may attach multiple files in your email to the mailing list as part of an existing thread or a new one. Remember to summarize the issue you have tackled and your work if the commit message is not detailed enough.

   If there is a JIRA ticket associated with your work you should post your patch files to the ticket.

```no-highlight
        $ git format-patch origin/trunk
```  

* Alternatively, you can use the mirror on github.com to submit a pull request. The mirror is located at [https://github.com/apache/incubator-mynewt-site](https://github.com/apache/incubator-mynewt-site). It is up to you to decide whether to create a fork or a branch to work in and submit pull requests from. Remember you cannot push changes to the master on the github mirror, so you have to create a fork or a branch first. Your pull request will be reviewed by a committer for docs and merged into the master branch when the changes are understood and accepted. 


### Conversion to HTML

The conversion of the Markdown files to HTML for the website happens manually and statically using MkDocs. You cannot see automatic and immediate rendering in HTML upon making a change in the Markdown file. You can choose to stop here and proceed to changing other Markdown files in your branch.

### Local preview of HTML files

However, you have the option to download MkDocs and do a local conversion yourself to preview the pages using the built-in devserver that comes with MkDocs. But first you will have to install MkDocs for that. In order to install MkDocs you'll need Python installed on your system, as well as the Python package manager, pip. You can check if you have them already (usually you will).
```no-highlight
        $ python --version
        Python 2.7.2
        $ pip --version
        pip 1.5.2
        $ pip install mkdocs
```
You will then run the built-in webserver from the root of the documentation directory using the command `mkdocs serve`. The root directory for documentation is `incubator-mynewt-site` or the directory with the `mkdocs.yml` file.
```no-highlight
        $ ls
        docs		images		mkdocs.yml
        $ mkdocs serve
```
Then go to [http://127.0.0.1:8000](http://127.0.0.1:8000) to preview your pages and see how they will look on the website! Remember that the Myself website itself will not be updated.
        
For more information on MkDocs go to [http://www.mkdocs.org](http://www.mkdocs.org). 
