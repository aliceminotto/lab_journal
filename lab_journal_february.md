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

* the table is getting to big (more than 150GB for the first simulation)==> gave up on this.

#####12/2/2016

* worked w/ c on the manuscript, it has to be shorter. correct some typos, add tables, delete some sentences and add some comments.

#####15/2/2016

* working on modifying the population dynamics images. instead of one plot with all the jumps for each DT I should get one plot made of four subplots: the first one will dysplay just the first jump, the second one the first two jumps, than the first five jumps and all the twenty jumps. The plots will have to share the y axis to save space and have a common title.

* created 4 subplots and plotted the right number of jumps in a loop.
added black stem with:
  ```python
markerline, stemlines, baseline=subp.stem(ts,Rs,linefmt='--', markerfmt='.', basefmt='',stemlineswidth=0.1)
        plot.setp(stemlines, 'linewidth', 1, 'color', 'k')
```
  To save space i used <code>plot.tight_layout()</code>.
  To share the y axis i added <code>sharey=ax1</code> whe naming the subplot, to hide the y axis in the second column:
  ```python
  if subp==ax2 or subp==ax4:
            plot.setp(subp.get_yticklabels(), visible=False)
```

#####16/2/2016

* going on with the figures. I have to hide the offset in the second column.
  After tryng lot of options that didn't work, the best solution in this case was to get rid of <code>sharey=ax1</code> because it will be shared anyway as I'm setting the <code>ylim</code>, then adding the following line to the previous code:
  ```python
if subp==ax2 or subp==ax4:
            plot.setp(subp.get_yticklabels(), visible=False)
            subp.yaxis.set_major_formatter(mtick.FormatStrFormatter('%.0f'))
```
  I also made the line thicker for visualization purposes.

* i could also fix these: increase the font-size of the labels as they are very small and i don't think you can read them on paper. Add the x axis and y axis label.

* fixed the label size. I think not to put labels because they are going to be repeated and to take space, so it would probably be better put a note in the description. (anyway the population dynamics is probably not going to the paper after all??).
  These would be the new plots:
  ![DT 500 population dynamics](https://www.dropbox.com/s/lewhypl7vusqbty/0popdyn_500.png?dl=1)
  ![DT 1000 population dynamics](https://www.dropbox.com/s/1gq3zk878zp736h/0popdyn_1000.png?dl=1)
  ![DT 5000 population dynamics](https://www.dropbox.com/s/y5o0l8ned9ba7zg/0popdyn_5000.png?dl=1)
  ![DT 10000 population dynamics](https://www.dropbox.com/s/cg4xhjp34qbxmls/0popdyn_10000.png?dl=1)

#####17/2/2016

* goign o w/ the tsltraining website: added folder with the badges pages and the needed pages.

* TO IMPROVE: ~~Add in css a style for the anchor (actually just change the position of <code></a></code>~~, as i don't want them to show as link. The category finder in the main page is empty. no badges found for molecular biology nor sterile practice. ~~also it would be nice to relocate all the badges images in the website itself~~.

* added an additional navigation bar in the footer with styling

#####18/2/2016

* added a contact form with formspree.io, added a twitter follow button  
  i used formspree instead of PHP cause github pages are static and do not allow the use of PHP (there are a lot of tutorial to create a PHP contact form but it woouldn't work).

* note that bootstrap column are nested (so in my case i have a div that span 7 col, the div inside it still go up to a sum of 12)

* deleted the twitter button cause the account is not active anymore (the code is still there commented)

* try to add the TSL logo in the top navbar before the button but it looks very ugly to me (the code is till there commented)

* added a thank you page for when you submit a form

#####22/2/2015

* launched new carlos' version of <code>clusterV.py</code> for the derivateves and changed the plotting script accordingly (it is just a trial in <code>change_DT_Qi/</code> folder at the moment) over the weekend.
  Still miss the results for the case without jumps cause the hpc node died.

* switching to slurm cluster. After *several* crazy errors I finally have one <code>submit.sh</code> script and a <code>command.sh</code> script. The first one contains the list of resources needed, while the second one is actually launching the script with <code>srun</code>.
  Here's the final version. *submit.sh*:  
  ```bash
  #!/bin/bash
#SBATCH -p normal
#SBATCH -N 1
#SBATCH -n 1
#SBATCH --mem 32768
#SBATCH -t 0-5:00
#SBATCH -o slurm.%N.%j.out
#SBATCH -e slurm.%N.%j.err
#SBATCH --mail-type=END,FAIL
#SBATCH --mail-user=alice.minotto@tsl.ac.uk

srun $@
```
  The *command.sh* script:
  ```bash
  #!/usr/bin/bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/tsl/software/testing/gsl/1.16/x86_64/bin/lib; \
source python-2.7.4; \
python /usr/users/TSL_20/minottoa/change_DT_Qi/clusterV.py /usr/users/TSL_20/minottoa/new/ 50 10
```
  To run it i need to do  
  ```bash
sbatch submit.sh command.sh
```
  This way i can just change the second part reusing the first one as many times as i want.

* so i'm finally running the new version of clusterV on the <code>new</code> folder.
