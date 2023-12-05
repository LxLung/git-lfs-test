# git-lfs-test
## About

"LFS" stands for large file storage. It stores pointers to large files rather than the large file itself. The large file will be stored in github's lfs database.
## What Git LFS Solves
Normal git repos have a soft-cap of 50 MB and a hard-cap of 100 MB, which is fine if you are working with text files that are smaller than this.
Each git commit stores a compressed version history of differences into the .git file, which means binary files (.exe .dll .a .etc) or frequently changing files images (.png .jpeg .psd etc.) 
would have lots of differences that all gets stored. For example, if you are working on a digital painting that is version controlled using git, then each change will stored a compressed version in the .git file. 

Suppose the file compressed file is 5MB, which you can check when you use the command "du -h", then 10 commits later, your .git file would be bloated to at least 50 MB!
Larger files = Slower "git clone" + slower collaboration speed + more memory usage

## Git LFS
Just follow the git-lfs website's directions
https://git-lfs.com/
1. git lfs init (first time only)
2. git lfs tracking *.txt (Or any *.FileExtension) -- This creates and adds it to a .gitattributes file
3. That's it! Push and pull like how you normally would!

## In case your .git is already bloated
Just follow the instructions from the BFG Repo-Cleaner
https://rtyley.github.io/bfg-repo-cleaner/
1. git clone --mirror git://example.com/some-big-repo.git
2. java -jar bfg.jar --strip-blobs-bigger-than 100M some-big-repo.git (Yes you need Java)
3. Clean up: <br>
$ cd some-big-repo.git <br>
$ git reflog expire --expire=now --all && git gc --prune=now --aggressive <br>
4. git push
