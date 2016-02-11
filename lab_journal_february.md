##**Lab Journal**
####**_February_**
###**_Alice Minotto_**

#####1 and 2/2/2016

* corrected firmula in <code>mutation()</code> in the new model (also updated the code in github)

* launched again simulations for DT10000 NTO=5 an NTO=10 with the right formula (should be the same anyway). REMEMBER that in the server i made a mistake and the folder named nto10 is actually NTO=5 and viceversa (the zip file are ok instead).

* PREVIOUSLY forgot to note here:
  * from github created webpage for the project. The branch for the webpage is <code>gh-pages</code>
  * quite heavily modified the theme: changed header background, color theme, add navigation bar on the left that moves up in small screens, changed footer, add contacts, add horizontal ruler between sections, add images in the section and instructions to use the codes (with links). also created a nice preview for the website in social network changing the <code>head</code> part.
  * all this is now in the temporary <code>contents</code> branch, need to be merged as soon as carlos look at it and says is fine
  * to change the html file without committing it all the times i need to use **Jeckill** (installed it, it needs ruby -already on mac-, and rubygems for github, easily found instructions on github).
    ```bash
    bundle exec jekyll serve
   ```

* galaxy training -see other file-

* NOTE: i can use this [link](http://htmlpreview.github.io) to see a preview of the page in a branch.

#####meanwhile

* fork Dan's github repository for the training webpage of the lab, copy-pasted content from the previous website.
  Added <code>.html</code> files for the buttons in the navigation bar.
  added links in the navbar and make the right tab active at a given time.
  Added a CSS file to define <hr/> to use to divide sections and footer in the website.

* changed the README file in a branche for the genome size evolution project so that it doesn't say anymore that nothing is working, as i really hope is not true anymore.

#####10 and 11/2/2016

* wrote a file using the <code>csv</code> python module to order the data from the second model simulations in a huge csv file like following:  
  DT,NTO,ETA,RUN,JUMP,STRAIN,EFFECTOR,TARGET,SCORE,FITNESS,FIRST_APP,TIME,SIZE
  The code name is <code>tidy_table_second_model.py</code> and it is in scripts.
