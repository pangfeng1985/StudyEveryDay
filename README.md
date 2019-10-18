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
