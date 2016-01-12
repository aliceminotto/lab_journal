##**Lab Journal**
####**_January_**
###**_Alice Minotto_**

#####7/1/2016

* took a look at <code>functools</code>. nothing i can use at the moment.  
* read:
  > Subset selection of high-depth next generation sequencing reads for de novo genome assembly using MapReduce framework
  at http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4682372/
  notes: not enough infor on the trimming alg and results (there's the name of the program used by the way), i think this could make a big change in the results of using a subset of data or not, especially cause i don't think i have ever kept in my trimming program read with such a low minimum quality score as described in the article. the other thing is that for large genomes they are using allpaths, and so not just paired end reads, but also mate pair. looks like they are just making the subset selection on the paired reads, so i'd like to know the effect using velvet, for example, and just pe.

* TO DO LIST:
  * ~~comment the style for all the plots, to eliminate background colors.~~
  * ~~for the first plot in the **new** folder, fix the layout of the scale for both axis to make it consistent with other figures.~~
  * ~~save all the plot with high definition adding these lines when saving:~~
    ```python
    fig.patch.set_alpha(0.5)
    plot.savefig(namefig,dpi=100,bbox_inches='tight')
    plot.savefig(namefig+'.svg',bbox_inches='tight')
    ```
  * ~~for all the last plots with the comparisons between all the simulations do the same and set max values for the x axis as in carlos' mail~~
  * ~~remove 'Eff' from title~~ (8/1/2016, also removed 'TE')
  * ~~for the TE plots decrease the bin number so that the figures are less messy~~
  * ~~eliminate legend from 4.7 to 4.10~~ (8/1/2015 actually positioning it inside the plot and substituting alpha channel, usig marker instead of lines to be more compact)

  * all done on <code>comparison_plot.py</code> and <code>comparison_plot_derivatives.py</code> and launched.

#####8/1/2016

* moved **CDATAV.p** from **old_images** to main **new** folder to get images again with yesterday changes.

* re launched last two because i forgot to change the launch files and i moved tthe scripts to **scripts** repository.

* fixed images for paper. (note on matplotlib, to use marker instead of line in a scatterplot just use legend, but to have just one point instead of 3, need to use <code>scatterpoints=1</code>

#####11/1/2016

* launche 10 more runs for the first model simulation to save an average curve of the fitness, that is probably going to be requested for the paper. (will take this week probably)

* in the meanwhile went back to the code without classes cause it appears to be more effiv=cient (anyway i was probably saving more stuff in the classes one, that we don't need). there's one problem to fix here cause it's hanging (after finish anyway), could be the <code>os.fork</code> or the function jumps. if the second one it should work tomorrow just changing the seed.

* to address the possibility that it's the first one i looked through the doc for <code>multiprocessing</code> module in Python. not so simple cause i have to pass multiple varibales all different in the processes and i'd want them to run all toghether. for now i'm not satisfied wit the solution i tried.

* will need to talk about the results of the model. maybe also try to use a loooooot of jumps to make a coparison and see if the fitness stay below 1 (now it's almost always reaching 1).

* interesting: from the model it is seen that the ratio between targets that can be targeted in the pathogen and the ones actually present in the host converge after some evolutionary time, meaning that the host is actually becoming adapted.
* to do: semilog plot for some of the images already created on the y axis.

#####12/1/2016

* the problem was that the code was hanging cause it took tooooo much time to create a suitable pathogen for the host (i.e. with r>.5). the possible solutions to this were:
  * changing the treshold value to a lower one, starting with a pathogen that is less fit, like it just jumped from a different host.
  * create an initial pathogen in a not complitely random way, being able to create it with r>.5 much faster.
  At the moment we are using the first solution with <code>r>.1</code>, and launching 10 processes at a time.

* modified c's notebook to have a python code running on the server to obtain the plot.

* launche the simulation for:
  * DT1000
  * DT5000
  * DT10000
  * DT20000
  All of these had <code>r>.1</code>, <code>MU1=1.0/3</code> and <code>MU2=2.0/3</code>.

* we also need to address (^ time gap between host jumps), the role of the parameter, so I'm rnning other simulations changing NTO (maximum number of gene targeted by an effector) (values 10, 5, 3), MU1 and MU2. MU1 and MU2 are used in the random choice of having the gain of a link (number<mu1), nothing, or removal of a link (number>mu2). I'm changing this value simmetrically (at the moment), after added some coefficient eta and beta: beta is going to be 3-eta (mu2 resulting has to be <=1, so beta has to be between 1 and 3 to have a right increase), and i'm changing eta from 1 to 0.5 to 0.1.
  I'm now addressing the possible combination of these parameters for DT=1000. All the results (and images when ready) are stored in the cluster in the **results_second_model/** folder, inside subfolders, each of contains a meta file with all the parameters used in the simulation.

* changed NEO=3 insted of 5 to avoid probability problem during the caclulation. Rerunning everything

* beta=1.5-eta and not 3 cause it went over 1.0. Anyway this way is not simmetrical, but the opposite (tell c tomorrow).
