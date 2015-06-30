# The three types of version control

The first type of version control was developed with the premise that only one
person could be working on a file at a time. Developers would have to acquire a
lock on a file, 

Obviously there are a ton of problems with that work flow.

The second generation of version control was premised on centralized management
of files. Prior to ~2005 this was the most common form of version control.

Most recently the idea of distributed version control systems have become
popular. The three most popular are Git, Mercurial, and Bazaar. (talk about
where you find these).

## Common misconception
Having a distributed version control system means you cannot have a centralized
work flow.

Not true. Distributed version control makes centralized version control a
social issue instead of a requirement for use.

Some Benefits:

* Private Workspace
* Offline & Fairly fast
* Flexible Workflows

Drawbacks:

* Administration Support (permissions, account management, etc.)
* No Locks - Sometimes this is important when working with binary files
* Large Repositories - If your have terrabyte size repos, DVCS is not what you
want-- remember: it clones the whole repo
* Does not handle binary formats well.


# History of Git

Came out around 2005

Originally developed by Linus Torvalds, the creator of the Linux kernel. He
wrote it to replace BitKeeper because the die-hard free software movement fans
refused to use it.


## Terminology
heads - a named reference to commits (aka branches)
working tree - the current set of checked out files
HEAD - the current head of the working tree
remote - an upstream git server used for synchronizing (can have multiple)
object - a unit of storage for git
hash - (sometimes called an object name) is the SHA1 identifier for an object
index/staging area - the place files go before they are committed

## Basics

Act as a local file system:

* Initialize
     `git init`

Before adding, git has files in a few states:
    * Up to date
    * Untracked
    * Modified
    * Staged

* Adding
    `git add`

* Commiting
    `git commit` -- commits staged changes only

## Undoing things

### checkout

`git checkout <file|folder>` - Restore file changes to head state
`git checkout -p <file|folder>` - Restore interactively 

** `git checkout` is also used for switching branches

### reset

Reset has a LOT of use cases, but, most useful are for removing changes from the index:

`git add .`
`git status`

"Oh no! I don't want to commit the app.js changes"

`git reset app.js`

Now app.js is not longer staged for commit.

### reset --hard

## add

`git add .` - adds all files in the current directory and sub directories (not parent directories)
`git add app/` - adds all files in the app directory and sub-directories
`git add -p` - add changes interactively, this lets you add only parts of files without adding all changes


## Upstreams (remotes, etc)

Once you want to collaborate with other users it is helpful to have a bare centralized remote. 
A remote can be:
    * A hosted git service (GitHub, GitLab, BitBucket)
    * Your own git server
    * Another folder on the same machine

> You do not actually need a remote server to collaborate. You can set remotes to be a working git repository on another devs machine and pull directly from them. Pushing however, does not make sense in this context.

`git remote` - Lists remote names
`git remote -v` - Show remotes and urls they are associated with
`git remote add <name> <url>` - Adds a remote called <name>. The default behavior when cloning a repository is to call the remote server 'origin'
`git remote remove <name>` remove the upstream 

## Branching

* Branches are just different working trees
* Allows you to develop in parallel

git branch


## Merging

There are two camps for merging:

* git merge 
* git rebase

** Whitespace is not your friend

## Submodules

Submodules are nothing more than a way to declare other repositories as dependencies of your repo.

Benefits:
    * Allows you to keep separate libraries as dependencies
    * Garuntees the version of the library you want is consistent

Drawbacks:
    * Does not handle merging
    * Requires a little extra work to keep things in sync (i.e. git submodule update)
