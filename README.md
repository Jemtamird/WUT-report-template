# Electro-Heat Engineering
What you will need to install:
- git
- a local latex editor (I use MiKTeX as a package manager and jetbrains IDE or TexStudio as an editor)
- GitHub CLI
## Using Git
### Initial Setup (You'll need to do this once ever)
First things you'll need to configure your git username and email which it will use to track the changes you personally made.
Open a command terminal (any will do) and set up using:

```
git config --global user.name "YOUR_USERNAME"
```
and
```
git config --global user.email "YOUR_EMAIL"
```
I recommend using the GitHub's private email for this.You can get it through your account settings in the email tab and checking the keep your email addresses private and copying the noreply email that appears in the box there

Next you'll have to log in into the GitHub CLI using
```
gh auth login
```
and following the instructions there. (HTTPS is usually preferred to SSH)
### Repo Usage
Now that this is done we can go through the actual git usage
1. Begin with the creation of your working folder anywhere that wouldn't be protected by the system is fine (this means not something like C: or C:\Program Files)
2. Open the folder using terminal
3. Clone the project using ```git clone <url> .```(Do not forget the dot) replacing the `<url>` with the url copied from the green Code dropdown menu on the repo in the HTTPS tab or using the GitHub CLI command copied from the GitHub CLI tab (add a dot after copying the command to not create another folder in your working one like in the previous command )
4. The files on the repo will now be copied to your local machine
5. Next to avoid having to use the url every time it's needed - use the ```git remote add origin <url>``` this will give the url the alias of origin

#### Branching
In order not to accidentally not break the main code line you don't want to add things directly to it instead branches are used.
we'll probably want to keep a branch with the template and branch that off into individual report branches so it stays unaffected.
We'll also want to further branch the report branches into a development and main branch just so if anything breaks we can revert it easier.

For fixing very specific things you usually create a branch all for it so that everything else is unaffected until you fix the issue.

First you can see all branches with
```
git branch -a
```
then you can switch to a chosen branch using
```
git checkout <branch-name>
```
If you want to create a branch you can use
```
git branch <branch-name>
```
or
```
git checkout -b <branch-name>
```
which will immediately switch you to that branch. Due to the way we'll be working a new branch will also need to have an upstream set
which is just a branch it compares itself to. So that the report branch you work on compares itself to the main report branch instead of the template's.
this makes so that you have less work later
#### Commiting
Git doesn't track changes live instead, manually chosen files are chosen (staged) to be commited then their current version is saved.
When you add or change a file you can use
```
git status
```
This will tell you how many commits have been made to the current branch compared to its origin and whether any files have been created or changed.

After you made some changes to a file, and you're happy with the results you could use
```
git add filename.ext
```
This would tell git to add this file to the list of files you will commit soon, however because I set up some options so git ignores some file types you can replace the filename and extension with a dot to tell it to add everything in the entire file without fear of adding junk files.

So `git add .` will do. Next you actually commit the files that means the state of the files when they were added will actually be saved.
To do this use
```
git commit -m 'Short message explaining changes(Fixed this/Added that)'
```
Finally, after you make one or more commits you can push those changes back into the repo with
```
git push
```
this will put all your local changes into the repository.
#### Fetching and Merging
It might happen that two people created some changes to the same spot in a file.To avoid conflict the second person could push their changes they need to download the changes made first.
This is done using
```
git fetch
git merge
```
This will first get the change list made to the files on the repo and then add them to your local file so that your change sits on top of the earlier possibly conflicting one.
`git merge` will also be later used to put the changes made to the development branches into the main report branch.
## GitHub specific features
### Issue Tracker
There's an inbuilt issue tracker on GitHub where you can describe issues in a project
these can be used to point out things that need to be changed or fixed and then marked as fixed later.
There's also a comment section specific to an issue.
### Pull requests
Instead of having a shared feature branch when one of us wants to change a thing. Instead, they could make a branch specifically do that commit and push the changes they want to make to it and then do a pull request either by going into the tab on GitHub and choosing from which branch to which to put changes into or using
```
gh pr create --base <main-branch-name> --head <feature-branch-name> --title "PR title" --body 'PR description'
```
These changes could then be discussed and then merged into the main branch if we want them as they are or tweaked by someone else slightly before.

After merging the branch made just for that change could then be safely deleted using
```
git branch -d <branch-name>
```
### Workflows
There's a workflow added that each time someone pushes changes onto the repository will compile the tex file into a pdf which we can download from the actions menu. 
There IS a limit to how much these can run, but I doubt that we'll be running 30 hours of compilation in a month.
