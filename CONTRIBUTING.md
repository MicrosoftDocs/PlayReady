# Contributing to the PlayReady documentation

Thank you for your interest in our documentation. We appreciate your feedback, edits, additions and help with improving our docs. This page covers the basic steps and guidelines for contributing.

> [!IMPORTANT]
> All repositories that publish to Microsoft Docs have adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any questions or comments.<br> 
>
> Minor corrections or clarifications to documentation and code examples in public repositories are covered by the [learn.microsoft.com Terms of Use](https://learn.microsoft.com/legal/termsofuse). New or significant changes will generate a comment in the pull request asking you to submit an online Contribution License Agreement (CLA) if you are not an employee of Microsoft. We need you to complete the online form before we can accept your pull request.

## How to make a change

| To suggest a change to the docs, follow these steps: | Screenshots |
| :------------------- | :--------: |
| 1. If you're viewing a Microsoft Docs page, click the **Edit** button in the upper right of the page.  You will be redirected to the corresponding Markdown source file in the [GitHub repository](https://github.com/MicrosoftDocs/playready). | ![Edit Button](docs/images/edit_button.jpg) |
| 2. If you don't already have a GitHub account, click **Sign Up** in the upper right and create a new account. | ![Signup button](docs/images/signup-for-github-button.png)|
| 3. On the corresponding GitHub page that opens, click Edit (the pencil icon). | ![Pencil button](docs/images/pencil_button.jpg)|
| 4. In the Edit file pane, use Markdown language to make changes to the content. ([How to write markdown.](https://help.github.com/articles/basic-writing-and-formatting-syntax/))| ![Edit File](docs/images/edit-in-github.png)|
| 5. Click Preview changes to verify the formatting looks as expected. | ![Preview changes](docs/images/edit-in-github.png)|
| 6. When you're done, scroll to the bottom of the page and click "Propose file change", you will be presented with a "Comparing changes" page, allowing you to verify your changes. Then click the "Create pull request" button to submit your changes. At this point you are finished! | ![Propose a change](docs/images/propose.jpg)|

After you submit changes (via a pull request), they will be reviewed by a member of the documentation team. If your request is accepted, updates are published to [PlayReady documentation](https://learn.microsoft.com/playready).

*For internal review only, you can see your changes on the [staging site](https://review.learn.microsoft.com/collaborate/?branch=main).

## Working with Branches

The [PlayReady GitHub repository](https://github.com/MicrosoftDocs/playready) utilizes two main parent branches: [Master](https://github.com/MicrosoftDocs/playready/tree/master), this content can be reviewed on the [staging site](https://review.learn.microsoft.com/windows/playready), and [Live](https://github.com/MicrosoftDocs/MicrosoftCollaboratePortal/tree/live), for content appearing on the [live site](https://learn.microsoft.com/windows/playready). 

When making contributions, please submit your Pull Request (PR) to the **Master** branch. This branch can be viewed on the staging site and should only contain contributions that are ready to be published live. You may also create and submit a branch with your own unique branch name which can be selected and viewed in the staging site. (The **Live** branch is only allowed for use by the content administrators.)

## Using issues to provide feedback on PlayReady documentation

To provide feedback, or point out a problem, rather than directly modifying actual documentation pages, [create an issue](https://github.com/MicrosoftDocs/playready/issues) and the content owners will do their best to address the issue in a timely fashion.

Be sure to include the topic title and the URL if you are creating an issue regarding a specific page.


## Making more substantial content changes by forking the repo

To make substantial changes to an existing article, add or change images, or contribute a new article, we recommend using Git commands to fork and clone the repo for authoring. If you are unfamiliar with using Git, try this [Git training](https://try.github.io/) to get started.

We also ask that before contributing a new article, to ask yourself the following questions...

* Have I included one, and only one, #-level title (equivalent to H1 in HTML)? 
* Is the verb tense (if applicable) in the title of my new article in the present tense and consistent with the other documentation?
* Is all of my grammar correct?
* Have I added my article - if contributing a new article - to the appropriate category as well as updated TOC.md?
* Have I properly formatted URLs to [look like this](https://learn.microsoft.com) instead of this: `https://learn.microsoft.com`?
* Have you had at least two people review your new article?
* Have you contacted [WindowsAuthoring](mailto:windowsauthoring@microsoft.com) if you're unsure about anything?

### Step #1
- Click the "Fork" button in the top-right corner of the [GitHub repo](https://github.com/MicrosoftDocs/playready)
- Create a local clone by clicking the green "Clone or download" button, copy to your clipboard, then in your commandline enter `git clone <paste your repo clone link>`).
- For more info, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/). 

### Step #2
- Once you have forked and cloned the repo to your local machine, you can begin authoring with the text editor of your choice.  We, of course, recommend [Visual Studio Code](https://code.visualstudio.com/), a free lightweight open source editor from Microsoft. For help with markdown authoring, check out this [Markdown is FUN for Everyone! Poster](docs/images/HowToWriteMarkdownPoster.pdf) with all of the basics you need to know. Print it and hang it on your wall as a reminder to contribute.
- Make any changes or additions to the content that you would like with your chosen text editor, then submit a "Pull Request" or "PR" to the original MicrosoftDocs repo. *Please be sure you are submitting your PR to the master branch, as we will not merge any PRs submitted to the live branch.
 
### Step #3 
- Once you are ready to submit a Pull Request so that your contribution will be staged for publishing, enter the following steps in the command line.
- `git status`: This command will show you what files you have changed so that you can confirm that you intended to make those changes. 
- `git add -A`: This command tells git to add ALL of your changes. If you would prefer to only add the changes you have made to one particular file, instead enter the command: `git add <file.md>`, where "file.md" represents the name the file containing your changes.
- `git commit -m “Fixed a few typos”`: This command tells git to commit the changes that you added in the previous step, along with a short message describing the changes that you made.
- `git push origin <yourbranchname>`: This command pushes your changes to the remote repo that you forked on GitHub (the "origin") into the branch that you have specified. Because you have forked the repo to your own GitHub account, you are welcome to do your work in the **Master** branch. 
- Go to your fork of the content repo: https://github.com/your-github-alias/playready.
- Click the "New pull request" button. (The "base fork:" will be listed as "MicrosoftDocs/playready", the "head fork:" should show your fork of the repo and the branch in which you made your changes.) You can review your changes here as well. 
- Click the green "Create pull request" button. You will then be asked to give your Pull Request a title and description, then click the "Create pull request" button once more.
- After pushing your contribution to the remote repo, you will be sent an email from *Open Publishing Build Service* informing whether your contribution built successfully and linking to any error warnings such as broken links, click the links to see your content staged on the site.
- Once your PR is submitted, a member of the documentation team will review your contribution and, if approved, it will be published to [PlayReady documentation](https://learn.microsoft.com/playready).

## Using issues to provide feedback on this documentation

To provide feedback rather than directly modifying actual documentation pages, [create an issue](https://github.com/MicrosoftDocs/playready/issues). Be sure to include the topic title and the URL for the page that your issue relates to.

## Additional resources
- [Getting started with writing and formatting on GitHub](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

## Additional resources for Microsoft employees
- [Connect your GitHub account and MS alias](https://review.learn.microsoft.com/windows-authoring-guide/github-account#2-connect-your-github-account-and-ms-alias-on-the-microsoft-open-source-portal)
- [Resources for writing Markdown](https://review.learn.microsoft.com/windows-authoring-guide/writing-guidance/writing-markdown)
