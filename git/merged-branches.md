# Check what branches are merged/not merged into current branch

I thought this was pretty damn cool: `git branch --merged` will list the branches merged into the current branch. This is a nice way to keep track of what needs merging or what might need to be thrown away if there a ton of branches sitting around in your local. `git branch --no-merged` will show the branches not merged. By default this shows only local branches. The `-a` flag shows local and remote branches and `-r` shows only remote. 
