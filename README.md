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
    #ignore all .a files  
	*.a  
	#but do track lib.a, even though you're ignoring .a files above  
	!lib.a  
	#only ignore the TODO file in the current directory, not subdir/TODO  
	/TODO  
	#ignore all files in any directory named build  
	build/  
	#ignore doc/notes.txt, but not doc/server/arch.txt  
	doc/*.txt  
	#ignore all .pdf files in the doc/ directory and any of its subdirectories  
	doc/**/*.pdf  


	Viewing Your Staged and Unstaged Changes  
	answer these two questions: What have you changed but not yet staged? And what have you staged that you are about to commit?   

	git diff =>  That command compares what is in your working directory with what is in your staging area. The result tells you the changes you’ve made that you haven’t yet staged   
	git diff --staged  => This command compares your staged changes to your last commit  


	Committing Your Changes  
	git commit:  
			Now that your staging area is set up the way you want it, you can commit your changes. Remember  
			that anything that is still unstaged — any files you have created or modified that you haven’t run  
			git add on since you edited them — won’t go into this commit. They will stay as modified files on  
			your disk. In this case, let’s say that the last time you ran git status, you saw that everything was  
			staged, so you’re ready to commit your changes  

	git commit -a : 
	                Adding the -a option to the git commit command makes   
                    Git automatically stage every file that is already tracked before doing the commit, letting you skip   
                    the git add part  


	Removing Files    
	git rm  :   
	         remove a file from Git  
			 also removes the file from your working directory  
			 If you modified the file or had already added it to the staging area, you must force the removal with the -f option  

    git rm --cached :   
	         keep the file in your working tree but remove it from your staging area  
			 In other words, you may want to keep the file on your hard drive but not have Git track it anymore  
			 You can pass files, directories, and file-glob patterns to the git rm command   

	Moving Files  
	git mv file_from file_to :  
	                        this is equivalent to running something like this:  
	mv README.md README    
	git rm README.md    
	git add README    


	Viewing the Commit History    
	git log   :   
	           -p  =>  One of the more helpful options is -p or --patch, which shows the difference (the patch output)  introduced in each commit   
			   -2  =>  using -2 to show only the last two entries   
			   --stat =>  if you want to see some abbreviated stats for each commit, you can use the --stat option   

	Unstaging a Staged File   
	git reset HEAD CONTRIBUTING.md  :   
	                  The command is a bit strange, but it works. The CONTRIBUTING.md file is modified but once again unstaged.   
					  It’s true that git reset can be a dangerous command, especially if you provide the --hard flag   

	Unmodifying a Modified File   
	git checkout -- CONTRIBUTING.md  :   
					It’s important to understand that git checkout -- <file> is a dangerous command.   
					Any local changes you made to that file are gone — Git just replaced that file with   
					the most recently-committed version. Don’t ever use this command unless you  
					absolutely know that you don’t want those unsaved local changes.   
	       
	Working with Remotes  
	Showing Your Remotes:  
	git remote :  
	            To see which remote servers you have configured, you can run the git remote command. It lists the   
                shortnames of each remote handle you’ve specified. If you’ve cloned your repository, you should at   
				least see origin — that is the default name Git gives to the server you cloned from   
	git remote -v:  
	            You can also specify -v, which shows you the URLs that Git has stored for the shortname to be used   
                when reading and writing to that remote   

	Adding Remote Repositories  
	git clone :    
	           git clone command implicitly adds the origin remote for you  
	git remote add <shortname> <url>:  
	           To add a new remote Git repository as a shortname you can reference easily, run git remote add <shortname> <url>  


	Fetching and Pulling from Your Remotes   
	git fetch <remote>:  
	                   The command goes out to that remote project and pulls down all the data from that remote project   
						that you don’t have yet. After you do this, you should have references to all the branches from that   
						remote, which you can merge in or inspect at any time   

						If you clone a repository, the command automatically adds that remote repository under the name   
						“origin”. So, git fetch origin fetches any new work that has been pushed to that server since you   
						cloned (or last fetched from) it. It’s important to note that the git fetch command only downloads  
						the data to your local repository — it doesn’t automatically merge it with any of your work or  
						modify what you’re currently working on. You have to merge it manually into your work when  
						you’re ready.  
	git pull    :  
	            If your current branch is set up to track a remote branch (see the next section and Git Branching for  
				more information), you can use the git pull command to automatically fetch and then merge that  
				remote branch into your current branch. This may be an easier or more comfortable workflow for  you  

	git clone :  
	           by default, the git clone command automatically sets up your local master branch to track  
				the remote master branch (or whatever the default branch is called) on the server you cloned from.  
				Running git pull generally fetches data from the server you originally cloned from and  
				automatically tries to merge it into the code you’re currently working on  

	Pushing to Your Remotes   
     git push <remote> <branch> :   
	                             If you want to push your master branch to  
								your origin server (again, cloning generally sets up both of those names for you automatically),  
								then you can run this to push any commits you’ve done back up to the server  
								This command works only if you cloned from a server to which you have write access and if  
								nobody has pushed in the meantime. If you and someone else clone at the same time and they push  
								upstream and then you push upstream, your push will rightly be rejected. You’ll have to fetch their  
								work first and incorporate it into yours before you’ll be allowed to push  


	Inspecting a Remote    
	git remote show <remote>:  
	                        If you want to see more information about a particular remote, you can use the git remote show <remote> command  

	Renaming and Removing Remotes    
	 git remote rename : git remote rename pb paul   (pb -> paul)   
	                    You can run git remote rename to change a remote’s shortname.   
						It’s worth mentioning that this changes all your remote-tracking branch names, too. What used to   
						be referenced at pb/master is now at paul/master.   
	gitremote remove or git remote rm:   
	                    If you want to remove a remote for some reason — you’ve moved the server or are no longer using  
						a particular mirror, or perhaps a contributor isn’t contributing anymore — you can either use git  
						remote remove or git remote rm  
						Once you delete the reference to a remote this way, all remote-tracking branches and configuration  
						settings associated with that remote are also deleted  


	Tagging   
		Like most VCSs, Git has the ability to tag specific points in a repository’s history as being important.    
		Typically, people use this functionality to mark release points (v1.0, v2.0 and so on). In this section,    
		you’ll learn how to list existing tags, how to create and delete tags, and what the different types of    
		tags are  .  

	Listing Your Tags  
	git tag (with optional -l or --list):  
	                     This command lists the tags in alphabetical order; the order in which they are displayed has no real importance.  
	git tag -l "v1.8.5*"   :  
	                    You can also search for tags that match a particular pattern. The Git source repo, for instance,  
						contains more than 500 tags. If you’re interested only in looking at the 1.8.5 series, you can run this  
						you’re supplying a wildcard pattern to match tag names, the use of -l  
						or --list is mandatory  
	Creating Tags  
	Git supports two types of tags: lightweight and annotated  
	lightweight tag:  
	               A lightweight tag is very much like a branch that doesn’t change — it’s just a pointer to a specific commit  
	Annotated tags:  
	              Annotated tags, however, are stored as full objects in the Git database. They’re checksummed;   
				  contain the tagger name, email, and date; have a tagging message; and can be signed and verified   
				  with GNU Privacy Guard (GPG). It’s generally recommended that you create annotated tags so you   
				  can have all this information; but if you want a temporary tag or for some reason don’t want to   
				  keep the other information, lightweight tags are available too.  

	git tag -a v1.4 -m "my version 1.4":  
	              Creating an annotated tag in Git is simple. The easiest way is to specify -a when you run the tag command.    

	git tag -a v1.2 9fceb02 :  
					Now, suppose you forgot to tag the project at v1.2, which was at the “updated rakefile” commit. You  
					can add it after the fact. To tag that commit, you specify the commit checksum (or part of it) at the  
					end of the command  

	git show v1.4:  
	             You can see the tag data along with the commit that was tagged by using the git show command  

	Lightweight Tags  
	git tag v1.4-lw:  
					This is basically the commit checksum stored  
					in a file — no other information is kept. To create a lightweight tag, don’t supply any of the -a, -s, or  
					-m options, just provide a tag name   


	Sharing Tags  
	git push origin <tagname>:  
							By default, the git push command doesn’t transfer tags to remote servers. You will have to explicitly  
							push tags to a shared server after you have created them. This process is just like sharing remote  
							branches — you can run git push origin <tagname>.  
	git push origin --tags:  
	                      If you have a lot of tags that you want to push up at once, you can also use the --tags option to the  
						git push command. This will transfer all of your tags to the remote server that are not already there.  


	git push pushes both types of tags  
	Pushing tags using git push <remote> --tags does not distinguish between  
	lightweight and annotated tags; there is no simple option that allows you to select  
	just one type for pushing  

	git tag -d <tagname>:   
						To delete a tag on your local repository, you can use git tag -d <tagname>. For example, we could   
						remove our lightweight tag above as follows  
						Note that this does not remove the tag from any remote servers. There are two common variations  
						for deleting a tag from a remote server.  

	git push origin :refs/tags/v1.4-lw:  
						The way to interpret the above is to read it as the null value before the colon is being pushed to the  
						remote tag name, effectively deleting it  

	git push origin --delete <tagname>   