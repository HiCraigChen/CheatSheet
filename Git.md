Revert the status to last commit you have. (Maybe write a bunch of codes which is not useful and  want to revert to the original code)  
`git checkout -- <bad filename>`

View file diff in git before commit
If you want to see what you haven't git added yet:  
`git diff myfile.txt`  
or if you want to see already added changes  
`git diff --cached myfile.txt`
