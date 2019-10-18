# StudyEveryDay

##         ****study git****       [book:E:\D\study\git\progit.pdf]
(1)Git thinks of its data more like a series of
snapshots of a miniature filesystem. With Git, every time you commit, or save the state of your
project, Git basically takes a picture of what all your files look like at that moment and stores a
reference to that snapshot. To be efficient, if files have not changed, Git doesn’t store the file again,
just a link to the previous identical file it has already stored. Git thinks about its data more like a
stream of snapshots

(2)Git has three main states that your files can reside in: modified,staged, and committed  
• Modified means that you have changed the file but have not committed it to your database yet.   
• Staged means that you have marked a modified file in its current version to go into your nextcommit snapshot.    
• Committed means that the data is safely stored in your local database   
This leads us to the three main sections of a Git project: the working tree, the staging area, and the Git directory   

(3)git config
git config --global user.name "John Doe"   
git config --global user.email johndoe@example.com   
git config --list    
git config user.name     (You can also check what Git thinks a specific key’s value is by typing git config <key>)    
git config --show-origin rerere.autoUpdate     (Since Git might read the same configuration variable value from more than one file)

chapter two: Git Basics
   You typically obtain a Git repository in one of two ways:
       1. You can take a local directory that is currently not under version control, and turn it into a Gitrepository, or  
       2. You can clone an existing Git repository from elsewhere  

   Initializing a Repository in an Existing Directory 
   cd /home/user/my_project
   git init

   Cloning an Existing Repository:Git receives a full copy of nearly all data that the server has. Every version of every file for the history of the project is pulled down by default when you run git clone   
   git clone https://github.com/libgit2/libgit2  
   git clone https://github.com/libgit2/libgit2 mylibgit

   Checking the Status of Your Files   
   git status   
   git status -s or git status --short   (There are two columns to the output — the lefthand column indicates the status of the staging area and the right-hand column indicates the status of the working tree)   

   Tracking New Files  
   git add README   
   The git add command takes a path name for either a file or a directory; if it’s a directory, the command adds all the files in that directory recursively  
   git add is a multipurpose command — you use it to begin tracking new files, to stage files, and to do other things like marking merge-conflicted files as resolved. It may be helpful to think of it more as “add precisely this content to the next commit” rather than “add this file to the project”    
   Git stages a file exactly as it is when you run the git add command   


   Ignoring Files : .gitignore file
   In the simple case, a repository might have a single .gitignore file in its root
	directory, which applies recursively to the entire repository. However, it is also
	possible to have additional .gitignore files in subdirectories. The rules in these
	nested .gitignore files apply only to the files under the directory where they are
	located
   
   
    
   An asterisk (*) matches zero or more characters   
   [abc] matches any character inside the brackets (in this case a, b, or c)   
   a question mark (?) matches a single character  
   brackets enclosing characters separated by a hyphen ([0-9]) matches any character between them (in this case 0 through 9)  
   You can also use two asterisks to match nested directories; a/**/z would match a/z, a/b/z, a/b/c/z, and so on  

   sample .gitignore:  more examples(https://github.com/github/gitignore)
    # ignore all .a files
	*.a
	# but do track lib.a, even though you're ignoring .a files above
	!lib.a
	# only ignore the TODO file in the current directory, not subdir/TODO
	/TODO
	# ignore all files in any directory named build
	build/
	# ignore doc/notes.txt, but not doc/server/arch.txt
	doc/*.txt
	# ignore all .pdf files in the doc/ directory and any of its subdirectories
	doc/**/*.pdf


	Viewing Your Staged and Unstaged Changes
	git diff  =>  answer these two questions: What have you changed but not yet staged? And what have you staged that you are about to commit? 
