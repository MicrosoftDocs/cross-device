# Contributing to the Project Rome documentation

Thank you for your interest in our documentation. We appreciate your feedback, edits, additions and help with improving our docs. This page covers the basic steps and guidelines for contributing.

## Sign a CLA

If you want to contribute more than a couple lines and you're not a Microsoft employee, you need to [sign a Microsoft Contribution Licensing Agreement (CLA)](https://cla.microsoft.com/). 

## Propose a minor change

To suggest a simple change to the docs, follow these steps:

1. If you're viewing the Docs.microsoft.com page, click the **Edit** button in the upper right of the page.  You will be redirected to the corresponding Markdown source file in the [GitHub repository](https://github.com/MicrosoftDocs/project-rome). If you are already in the GitHub repo, you can just navigate to the source file that you would like to change.
2. If you don't already have a GitHub account, click **Sign Up** in the upper right and create a new account.
3. From the GitHub page you would like to change, click the pencil icon. 
4. Modify the file and use the preview tab to ensure the changes look good.
5. When you're done, commit your changes and open a pull request.

After you create the pull request, a member of the Windows 10 docs team will review it. If your request is accepted, the updates will be published to [https://docs.microsoft.com/windows/project-rome/](https://docs.microsoft.com/windows/project-rome/).

## Make more substantial changes

### Fork the GitHub repo

To make substantial changes to an existing article, add or change images, or contribute a new article, we recommend forking the repo into your GitHub account (click the "Fork" button in the top-right corner of the [GitHub repo](https://github.com/MicrosoftDocs/project-rome), and then creating a local clone (click the green **Clone or download** button, copy to your clipboard, then in your command line enter `git clone <paste your repo clone link>`).

For more info, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).

If you are unfamiliar with using Git, see the [Lynda.com Git Essentials training](https://www.lynda.com/Git-tutorials/Git-Essential-Training/100222-2.html).

### Author your contribution

Once you have forked and cloned the repo to your local machine, you can begin authoring with the text editor of your choice. We recommend [Visual Studio Code](https://code.visualstudio.com/), a free lightweight open source editor from Microsoft.

### Submit your contribution by issuing a pull request (PR)

Once you have saved the changes to your local git repo, enter the following commands in the command line to commit and push them to your local forked repo:
- `git status`: This command will show you what files you have changed so that you can confirm that you intended to make those changes. 
- `git add -A`: This command adds all of your changes to the change index. If you would prefer to only add the changes you have made to a particular file, enter the command: `git add <yourfile.md>`.
- `git commit -m "your commit message"`: This command tells git to commit the changes that you added in the previous step, along with a short message describing the changes that you made.
- `git push origin <yourbranchname>`: This command pushes your changes to the remote repo that you forked on GitHub (the "origin"), in the branch that you have specified.

After pushing your contribution to the remote repo, you will be sent an email from *Open Publishing Build Service* informing you whether your contribution built successfully and providing links to any errors or warnings in your repo, such as broken links. Click the links in the report to see your content staged on the site. When your changes are cleared of errors and warnings, you are ready to submit a PR.
- Go to your fork of the project-rome repo: https://github.com/**\<your-github-alias\>**/project-rome.
- Click the **New pull request** button. The "base fork:" will be listed as "MicrosoftDocs/project-rome", and the "head fork:" should show your fork of the repo and the branch in which you made your changes. You can review your changes here as well. 
- Click the **Create pull request** button. You will then need to give your PR a title and description. Finally click the **Create pull request** button once more.

Once your PR is submitted, a member of the Windows 10 docs team will review it. When it is accepted, you will be able to view your changes on the [staging site](https://review.docs.microsoft.com/windows/project-rome/). These updates will eventually be published live to [https://docs.microsoft.com/windows/project-rome/](https://docs.microsoft.com/windows/project-rome/).

## Using Issues to provide feedback on Project Rome documentation

To provide feedback rather than directly modifying the documentation pages, [create an issue](https://github.com/MicrosoftDocs/project-rome/issues).

Be sure to include the topic title and the URL for the page in question.

## Additional resources
- [Getting started with writing and formatting on GitHub](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

## Additional resources for Microsoft employees
- [Connect your GitHub account and MS alias](https://review.docs.microsoft.com/windows-authoring-guide/github-account#2-connect-your-github-account-and-ms-alias-on-the-microsoft-open-source-portal)
- [Resources for writing Markdown](https://review.docs.microsoft.com/windows-authoring-guide/writing-guidance/writing-markdown)