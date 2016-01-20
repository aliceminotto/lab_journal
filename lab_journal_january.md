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

#####13/1/2016

* finished running what wrote yesterday, plus all the plots and additional DT (with already exaplined changes in NTO and MUs) 500, 5000 and 10000.

* observations: from yesterday runs it looks like, as it may be obvious, that at the beginning of the simulation if a strain has a very high r value (close to 1), and there is a jump, this results (almost always) in a huge decrease of the fitness. On the opposite if the jump happen at the end of the simulation for a strain with an equally high r value, this usually results in a more mild decrease in the fitness. I thought this is due to the fact that at the beginning of the simulation the number of genes is limited and an high r is due mainly to high specificity towards the target gene present in the host, while at the end all the strain tend to have higher r, probably due to an increase in the total number of effector genes. This was confirmed looking at the plots for the number of genes.

* other minor observations to check: after running the simulation for DT500 and others it looks that maybe the NTO and MU parameters have a more visible effect for low DT (this can be the case cause the strains have not enought itme to reach a good fitness before the jump happens). In particoular it looks like the slope to reach an average high fitness is decreasing when the mutation probability is >> than the probability to gain targets (or lose them).  
  Another observation is that at the end of the simulation less strains arise in the same DT (i see this comparing the new strains per jump), this is probably due to the implementation itself (as we thought it would have made sense like this), cause if a pathogen is already fixed the probability to mutate is lower AND we are just introducing new strands if they have a better r compared to the mother strain.

* to do next days: switch from this r calculation function to the other one (<code>g_p_mapa2</code>) as this one is linear, and the other one is semi linear (Hill function, will have to pass 1 as parameter so), so the r increase over the evolutionary time should be slower. (the same -more or less- could be obtained multiplying the present function for a factor that makes the result smaller)

* example plots for what i was explaining:
  ![genome evolution of different strains over time, DT1000 NTO=5 and mu coefficient=0.5](https://www.dropbox.com/s/uze2hgccrszvdhw/0typevol_1000_5_05.png?dl=1)
  fitness for the DT=1000,NTO=10 and mu coefficient=0.5 parameters:
  ![fitness nto 10](https://www.dropbox.com/s/xeipvr5bomxf8bh/0rratestyp_1000_10_05.png?dl=1)
  number of effectors:
  ![nuber of effectors nto=10](https://www.dropbox.com/s/492bkblwv3bjd4r/0typngenevol_1000_10_05.png?dl=1)
  For NTO=5. Fitness:
  ![fitness same parameters](https://www.dropbox.com/s/whcwvfct6naqhjw/0rratestyp_1000_5_05.png?dl=1)
  evolution of number of effectors:
  ![number of effector plot, same parameters](https://www.dropbox.com/s/8sfl5ysz5gwwhb2/0typngenevol_1000_5_05.png?dl=1)
  For NTO=3. Fitness:
  ![fitness for nto=3](https://www.dropbox.com/s/pi4pftxclnqh5lp/1rratestyp_3_05.png?dl=1)
  Number of genes:
  ![number of genes, nto=3](https://www.dropbox.com/s/qkrsvaewbcygfi9/1typngenevol_3_05.png?dl=1)

#####14/1/2016

* running the version with the hill function to calculate the fitness (at the moment I'm just doing DT=1000 to see the differences)

* trying to fix the branches problem, I think it is due to <code>deepcopy()</code> function not bing used anymore (???). Testing now for results.

* note: the verison of <code>hpmodel2_2.py</code> that uses the Hill function it's still running, being cosiderabely slower than the linear version (this is probably due to the fact the the linear function breaks at !, while this one never reaches 1 by definition, but is just asymptotic).

#####15/1/2016

* still looking at the branches problem, adding some <code>assert</code> to check if i can find when the duplication is happening

* FINALLY found the bug and fixed it (it was due to something very stupid, ie if the strain with the max id died in a jump is not going to be in the set of alive strains retained in the next jump and so the methid we were using to determine the id of the strain was a mess because it was based on the max id found in the cictionary at that time. we just needed to move this line outside of the for loop. (anyway the very very good news is that because the branch are due to this all the plots without branches, ie 95% are fine and we do not need to re make them).

* todo:
  * small table with average r after jumps for a serie of different parameters
  * semilog pot for old simulation
  * ~~figures for old simulation with the average fitness~~

#####18/1/2016

* created script in <code>scripts/plotting/</code> to generate plots for the first model simulation (DT5000, DT10000 and DT20000) with the average fitness over the simulation. (note: there's nothing interesting i can see here)
DT5000:
![DT5000 average fitness](https://www.dropbox.com/s/fhv4wvi6gbiuzuj/average_fitness_5000.png?dl=1)
DT10000:
![DT10000 average fitness](https://www.dropbox.com/s/aubdwhhy6961zlc/average_fitness_10000.png?dl=1)
DT20000:
![DT20000 average fitness](https://www.dropbox.com/s/zvadxcx3bmqnsjh/average_fitness_20000.png?dl=1)

* studying nodejs and plot streaming from sensor

#####19/1/2016

* i clearly made a mess with yesterday plots, so fixing it (i have the plot the whole time not an average over eah jump!!!)

* fixed it. Now the plots make sense. These are the plot for DT5000 for increasing values of c (the mutation rate).
  ![DT5000 c=0.1](https://www.dropbox.com/s/qvq45r8wj99zf76/average_fitness_n0_5000.png?dl=1)
  ![DT5000 c=0.2](https://www.dropbox.com/s/vorpd8my4wyav4s/average_fitness_n1_5000.png?dl=1)
  ![DT5000 c=0.3](https://www.dropbox.com/s/ckyhkht3gvunmgo/average_fitness_n2_5000.png?dl=1)
  ![DT5000 c=0.4](https://www.dropbox.com/s/qqzserlap2ly812/average_fitness_n3_5000.png?dl=1)
  ![DT5000 c=0.5](https://www.dropbox.com/s/guzgtfbdpdo878v/average_fitness_n4_5000.png?dl=1)
  ![DT5000 c=0.6](https://www.dropbox.com/s/enfxhzjetvj8blo/average_fitness_n5_5000.png?dl=1)
  i![DT5000 c=0.7](https://www.dropbox.com/s/xme5hiovndetrlz/average_fitness_n6_5000.png?dl=1)
  ![DT5000 c=0.8](https://www.dropbox.com/s/vupl7qhalolop9c/average_fitness_n7_5000.png?dl=1)
  ![DT5000 c=0.9](https://www.dropbox.com/s/d1246k08evv55at/average_fitness_n8_5000.png?dl=1)
  Here we can see an increase in the fitness during the simulation, ad more interesting (even if kind of obvious, but means that the simulation itself makes sense) there's a decrease in this value when there is a jump (see below the different pattern for DT10000 and DT20000 for the c value 0.5), and then it increase again.
  Moreover we can see the effect of the c value than increasing change the slope of the curve (it happens the same for DT10000 and DT20000, but I'm not posting here all the plots).
  DT10000 c=0.5:
  ![average fitness DT10000 c=0.5](https://www.dropbox.com/s/2vhmchmpecod9iu/average_fitness_n4_10000.png?dl=1)
  DT20000 c=0.5:
  ![average fitness DT20000 c=0.5](https://www.dropbox.com/s/50bgsfdqvsp8pvi/average_fitness_n4_20000.png?dl=1)

* the images are weird because the actual fitness, is 1-the value considered (moreover, as easily seen, there was a typo in the average function, cause the max value is 1. I plotted them again with 1-value and fixing the scale. I also plotted a typical run, and not just the average.
  The curve is good (meaning is what expected, cause after the jump there is a decrease in fitness, thean then increase until the next jump), but as it can be see in the next images, the overall fitness stays quite low.
  We so tried to run the simulation again for DT100 (new), DT20000 and no jumps, but changing the recombination rate by 100x. This results in the following changes in fitness.
  Typical run fitness for DT20000 and c=0.1:
  ![DT20000 c=0.1 typical run fitness](https://www.dropbox.com/s/k2rgcxl1euomzpm/one_fitness_n0_20000.png?dl=1)
  c=0.5:
  ![DT20000 c=0.5 typical run fitness](https://www.dropbox.com/s/yzol703yfx8m65u/one_fitness_n4_20000.png?dl=1)
  c=0.9:
  ![DT20000 c=0.9 typical run fitness](https://www.dropbox.com/s/27brhyeh69bixju/one_fitness_n8_20000.png?dl=1)
  Average fitness for DT20000 and c=0.1:
  ![DT20000 c=0.1 average fitness](https://www.dropbox.com/s/2xhrb24hi8yxxwq/average_fitness_n0_20000.png?dl=1)
  c=0.5:
  ![DT20000 c=0.5 average fitness](https://www.dropbox.com/s/kajxjf5ks0zp8n0/average_fitness_n4_20000%20%281%29.png?dl=1)
  c=0.9:
  ![DT20000 c=0.9 average fitness](https://www.dropbox.com/s/5x9ip3dlu38ph59/average_fitness_n8_20000.png?dl=1)

  For no jumps this is one run:
  ![no jumps one run fitness](https://www.dropbox.com/s/mgthdwqk3eoiima/one_fitness_n0_nojumps.png?dl=1)
  And this is the average:
  ![no jumps average fitness](https://www.dropbox.com/s/ei8etgtycaowbne/average_fitness_n0_nojumps.png?dl=1)
  These are oviously not very good beacuse this does not reflect a real situation, anyway this result is given by the model tself, tat is not considering host, and has max tresholds for number of TEs and Eff and lengths. This is the reason we try to see what happen changing the recombination rate (see below, better), and the reason this model had to be made better by the second model, that considers more and more parameters (more realistic).
  Other note is that the "strange" situation seen at the beginning of all the plots is due to an unstable state at the beginning of the simulation, should not be considered as a result.

  Increased the recombination rate. Rerun everything overnight with more runs (20 for DT100 and DT2000, 100 for no jumps). Will have results tomorrow.

#####20/1/2015

* the simulation finished overnight. run the scripts for the fitness plots.

* here the results for high recombination rate and nojumps:
  over one single run:
  ![high rec rate no jumps, one run fitness](https://www.dropbox.com/s/x9x199xp3epgxp4/one_fitness_n0_highmutation_nojumps.png?dl=1)
  averaged over 100 runs:
  ![high rec rate, no jumps, average fitness](https://www.dropbox.com/s/n8qeq1vq5zvf9q2/average_fitness_n0_highmuation_nojumps.png?dl=1)
  Because these run are complitely new (note that with this rec rate we have A LOT of extinctions, that's why the simulation is so fast compaed to the previous we had done), I also run the <code>clusterV.py</code> script to get the other figures.

* adding inset to the plots for high recombination rate and DT100 (this means 2000 jumps, so they're very noisy). This snippet of matplotlib will make the trick:
  ```python
  if c_value=='n0/':
        ax_inset=fig1.add_axes([0.5,0.5,0.3,0.3])
    else:
        ax_inset=fig1.add_axes([0.5,0.1,0.3,0.3])
    ax_inset.xaxis.set_major_formatter(mtick.ScalarFormatter(useMathText=True))
    plt.ticklabel_format(style='sci', scilimits=(0,0))
    ax_inset.yaxis.set_major_formatter(mtick.ScalarFormatter(useMathText=True))
    plt.ticklabel_format(style='sci', scilimits=(0,0))
    ax_inset.plot(range(100000,101000),plot_this[100000:101000],"k")
  ```

*

* TO DO LIST: 
  * fix all the position for the inset plots
  * change c's <code>clusterV.py</code> to plot averages with extinctions between two jumps
  * use it to plot all the <code>high_mutation*</code> simulations
  * get 40 more runs for DT100 high mutation rate to get better plots
