# Introductionn

Git is a useful platform for managing multiple versions of a file. Writers can work on a project independently, and contribute their work once it's ready to be shared. This page describes my workflow for writing documentation with Git and Github.

## Git Workflow

Each day, when you begin working, it is good practice to change to the main branch, and pull down the newest version to your machine. First, navigate to the folder where your repository is located using the `cd` command. Then, enter the following commands:

```
git checkout main
git pull
```

Once you've pulled down the latest version of main, you can create a new branch for the page(s) you are working on. It is best to name the branch after a Jira ticket, for example, DOC-3000.

To create a new branch called doc-3000 and switch to it, type:

`git checkout -b doc-3000`

The `-b` tag creates the branch and the `checkout` command changes to it. You could also perform this process in two steps, like so:

```
git branch doc-3000
git checkout doc-3000
```

Once you have a new branch, you can make changes to the relevant files. Once they are finished, you can `add` then `commit` them, before you `push` the branch to the remote repository.

You can `add` changes using the `git add .` command, which stages all the files that git notices have changed. This can be a dangerous command, however, because if you have navigated to the wrong folder and you thoughtlessly do `git add .`, you might inadvertantly stage a huge number of files you didn't intend to. For this reason, I normally use the following two commands first:

`ls` shows you the files in the folder you're currently in.
`git status` shows you which files git is paying attention to. If only the files you have worked on show up, then you are safe to proceed:

```
git add .
git commit -s -m "DOC-3000- Made Changes to X"
```

This stages and commits your change. The -s tag signs off on the commit, and the -m tag leaves a message. Commits must have a message; try to make it clear so your change can be easily identified later.

To push the branch and create a **pull request**, type `git push`. You will receive an error message that provides you with the correct command. Copy, paste, and click enter. Then, go to github.com and navigate to the repository you sent a pull request to. Your new pull request will appear at the top of the page in a green box. Click into it, write a more detailed description if necessary, and submit it. Your colleagues will review the pull request, and may request changes. Also, the pull request may need to be updated if it is out of sync with the main branch. Once these changes are made, and the pull request is approved, it can be **squashed and merged**.

## Hugo

When you edit or move a page, you may wish to see what the changes look like before you create a PR. This is where hugo comes in.

Open a new tab in Terminal, and use:

`hugo serve`

This will spin up a locally hosted version of the web-page. Navigate to the page you are editing to see your changes. Continue writing and save the file to see the page reload with your changes.

### Broken Links

Sometimes, moving a page will result in broken links. To resolve this before you create PR:

1. Start the `hugo` server

`npm run serve-for-checker &`

2. Run `muffet` to look for broken links:

`muffet http://localhost:1313/en -e ".*.js.*" -e ".*.gif.*" -e ".*png.*" -e ".*.css.*" -e ".*.icon.*" -e ".*.jpg.*" -e ".*/_print/.*" --ignore-fragments -i ".*localhost.*" --skip-tls-verification -c 10`

Any broken links will show up as a 404. Use VSCode's search to find and replace them with the new path.
