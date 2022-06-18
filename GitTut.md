# Git and Github -- A Version Control System and Remote Repository

## Git

### 1. Git Introduction

Git is a version control system, it can track down the editting history of the source code and trace back to the previous version. Also it allows the developer add edit code in parallel.

Following is the structure of a local Git System
![Stage Area and Repository](https://www.runoob.com/wp-content/uploads/2015/02/1352126739_7909.jpg)

Working Area: As the name suggests, it is where we edit the source code.

Staging Area(Index): We can add the CHANGE we made on working area to the staging area using command `git add <file>`, this area is assigned to store the alterations before they are pushed into repository.

Repository(master): The place git truly store the versions of the code. Git will automatically generate a pointer HEAD pointing to the branch master once the repository is initialized. We can commit out alteration on the code to repository using command `git commit -m <comment>`.

### 2. Init Add and Commit

Here are some commonly used and basic operation:

1. The git init command adds a local Git repository to the project.

```console
$ cd /learngit
$ git init
```

![learnGit](Source/Screenshot%20from%202022-06-14%2017-32-45.png)
![git.init](Source/Screenshot%20from%202022-06-14%2017-35-32.png)
You can see that there is .git directory in our current file folder

2. When we create, modify or delete a file, these changes will happen in our local and won't be included in the next commit (unless we change the configurations). We need to use the git add command to include the changes of a file(s) into our next commit.

```console
git add <file>
```

To add everything at once:[](https://www.liaoxuefeng.com/files/attachments/919022363210080/l)

```console
$ git add -A
```

3. Command `git commit` commit all the changes in the staging area to the repository.

```console
$ git commit -m <comment>
```

### 3. Branch and Merge Operation

The magic of Git is its' branch management, git branch allows the developer add code to the same repository in parallel.

The branch works independently from the main branch, we can add new feature or debug on the branch and merge to the master once all the work is done. It won't change master until you merge the branch to master.

![branch](https://static.runoob.com/images/svg/git-brance.svg)

At the first, the head points to the master and master point to our last commit.

![merge1](https://www.liaoxuefeng.com/files/attachments/919022325462368/0)

When we create a new branch dev and switch to it using command `git switch -c dev`, the HEAD will point to dev
and dev point to our last commit.

![merge2](https://www.liaoxuefeng.com/files/attachments/919022363210080/l)

Then we make new commit on the dev, now the HEAD points to the commit.
![merge3](https://www.liaoxuefeng.com/files/attachments/919022387118368/l)

Once we think dev finish our work, we can merge dev to master branch, the easiest way to do this is letting the master point to the last the commit on branch dev. We use command `git merge <branch>` to make this happen.

![merge4](https://www.liaoxuefeng.com/files/attachments/919022412005504/0)

Then we can switch back to the branch master and delete the branch dev, it looks like we just directly commit on the branch master.

### 4. Git Log

Git log is a utility tool to review and read a history of everything that happens to a repository. The command is
`git log` or `git log --graph --pretty=oneline --abbrev-commit`, the latter will make your commit history looks like an commit chain.

```console
*   870e579 (HEAD -> master) conflict fixed
|\  
| * a7dacd1 (dev) git is perfect
* | 799e100 git is good
|/  
* 7356221 quick switch
* 4629721 add branch
* c24a2f6 the first commit
* 
```

The unix number ahead of the comments is the unique version id of each commit. Version id is extremly useful when we want to reverse version.

### 5. Fix Conflict

When the same file is changed on different dev and finally they are merged together, conflict appears. The situation is common when more than one person are working on the same project.

When there is conflict, we need to fix the conflict in the file and re-submit it to branch.
![conflictfix2](https://www.liaoxuefeng.com/files/attachments/919023031831104/0)

## GitHub

### 1.Github -- Remote Repo

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/91/Octicons-mark-github.svg/2048px-Octicons-mark-github.svg.png" alt="github icon" style="width:100px;"/>

Git is convenient for team developing, usually a team establishes a central server to store version repository as back up,if any team member want to retrieve code, all he/she has to do is pull the repository from the central server. Github is a kind of central server that allows you pull or push code 24 hours a day and it is ONLINE ! We usually call it a remote repository.

Noticeably, interacting with remote repo makes no difference from interacting with local branch.

### 2. Link to Github

Here I suggest use ssh protocol to link to Github.

1. Check SSH key, change to your home directory, for Windows, it is in the user/username/.ssh. For Linux, it is on the dir ~/.ssh

```console
(base) george@george-XPS-13-9343:~/Documents/learnGit$ cd ~/.ssh
(base) george@george-XPS-13-9343:~/.ssh$ ls
id_ed25519  id_ed25519.pub  known_hosts
```

2. cd to .ssh filefolder mentioned above. Type command 

```console
$ ssh-keygen -t rsa -C "youremail@example.com"
```

to generate your own ssh key.
When you are prompted to "Enter a file in which to save the key," press Enter to accept the default file location.

```console
> Enter a file in which to save the key (/home/you/.ssh/id_ed25519_sk): [Press enter]
```

When you are prompted to type a passphrase, press Enter.

```console
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

3. After the key is generated, we need to add the public key to Github account. Which looks like this: 
![addsshkey](https://docs.github.com/assets/cb-24796/images/help/settings/ssh-key-paste.png)
For more details, please refer to [How to add SSH key](https://docs.github.com/cn/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).

4. Once the key is added to the account. We can link the local repo to remote repo(github repo). cd to your local repository filefolder and use the command.

```console
$ git remote add origin git@github.com:username/reponame.git
```

You can use the command below to test the link.

```console
$ ssh -T git@github.com
```
If you see the text below:

```console
> Hi MDmoonheart! You've successfully authenticated, but GitHub does not provide shell access.
```
you are ready to go.


