This is a tutorial for user to get familar with `git` tools.

> On Oct 16 2020, we had a seminar on *CFD source code management with Git and GitHub*. This is repository includes all the materials and tutorials in the seminar. If you are a beginner and want to learn more about `git` and `GitHub`, you are welcome to vist the [Zmeng Blogs](https://openfoam.tech/2020/06/GitUsage/). It shows you how to install, config, and use `git`.

# Install Git
```shell
sudo apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev
sudo apt-get install git
git --version
git config --global user.name "[name]"
git config --global user.email "[email address]"
```
# Use git

## Init a repository
```shell
mkdir tutorial
cd tutorial
git init
```

## Add files to repository and commit changes
create an empty `codeCFD.h` file

In `codeCFD.c` add these lines
```C++
#include <iostream>
#include "codeCFD.h"
int main()
{
	std::cout << "codeCFD.h" << std::endl;
	return 0;
}
```

```shell
git status
git add codeCFD.h codeCFD.c
git status
git commit -m "wrote initial files"
```

In `codeCFD.h` add these lines
```C++
void basicCombustionModel()
{
	std::cout << "a basic combustion model" << endl;
}
```

```shell
git status
git diff codeCFD.h
git add codeCFD.h
git status
git commit -m "add basic combustion model"
git log --oneline
```
## Time machine shuttle
```
rm codeCFD.c
git restore codeCFD.c
rm codeCFD.c
git reset --hard 1541955
git reflog
git reset --hard HEAD
git reset --hard HEAD^
git reset --hard HEAD~2
git reset --hard 1541955
```

```
┌────┐
│HEAD│
└────┘
   │
   └──> ○ add basic combustion model
        │
        ○ wrote initial files

┌────┐
│HEAD│
└────┘
   │    ○ add basic combustion model
   │    │
   └──> ○ wrote initial files
```


In `readme.txt` add these lines
```C++
we have now a basic combustion model
```

In `codeCFD.c` add these lines
```C++
basicCombustionModel();
```

commit the changes
```shell
git add -A
git commit -m "add a readme file"
```

In `readme.txt`
```C++
This is a hand shaking error
```

```shell
git add readme.txt
git diff
git diff HEAD
git diff HEAD -- readme.txt
git restore --staged readme.txt
```

## Tag management
```shell
git tag v1.0
git tag
git show v1.0
git tag -d v1.0
git tag -a v0.1 -m "version 0.1 released" 1541955
```

## remote repository
```shell
git remote add origin git@github.com:ZmengXu/learngit.git
git push -u origin master
```
