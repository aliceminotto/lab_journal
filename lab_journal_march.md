##**Lab Journal**
####**_March_**
###**_Alice Minotto_**

#####1/3/2016

* created image for TSL training website email (so that the email can't be targeted from html), use this to substitute the previous code.

* ```git diff name_file``` gives me the difference between the present file and the previous commit
  ```git log``` to see previous commits
  ```git show HEAD``` displays everything as git log but for the HEAD commit
  ```git checkout HEAD filename``` restore the file to the last commit
  ```git reset HEAD filename``` resets the file in the satging area to be the same as the HEAD commit
  ```git reset SHA``` this works with the first 7 chars of a previous commit (you can see the SHA with log)

#####3-4/3/2016

* ```git branch``` to know the branch you are on (with a *)
* ```git branch new_name``` create a new branch named ```new_name```
* ```git checkout branch_name``` to switch the branch you are on
* after resolving a merge conflict, i need to commit the changes to the staging area, BUT not commit [file] -m blabla, i have to commit -m (cmmit everything), this way i'm commit the merge resolution
* to delete an old branch i don't need anymore that it has already been merged ```git branch -d [name_branch]```

* ```git clone url name_of_the_copy```
* ```git remote -v``` lists the name of the remote and its location
* ```git fetch``` brings changes from the origin t the local repo
  Despite this the changes ar not on te local master, but on origin/master, so i also need to merge them with ```git merge origin/merge```
* ```git push origin my_branch``` to push a branch to remote

#####7/3/2016

* SQL

#####8/3/2016

* to smooth data i can calculate the average value of a point wiith its two neighbours
