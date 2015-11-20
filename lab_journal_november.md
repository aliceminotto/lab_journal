##**Lab Journal**
####**_November_**
###**_Alice Minotto_**

#####2/11/2015

* going on reading matplotlib tutorials and documentations
  NOTES:
  * **import matplotlib.pyplot as plt**
  * if u provide a single array/list to plot plt will assume it's y values and generates x auto
  * the third parameter you can give indicates the type of line in the graph and its color (default **b-**, ie simple blue line). -- is a dotted line, o circles, s squares ^ triangles.
  * **plt.axis([xmin,xmax,ymin,ymax])**
  * you can plot multiples arrays of values w/ the following synthax **plt.plot(list1, list2,line, list3, list4, line2...)**
  * all current commands will aplly to the current axis/figure
  * to add a title to an ax (or a title to the plot) **t = plt.xlabel('my data', fontsize=14, color='red')**. u can also use math expressions surrounded by $. with an r in front of the expression tho avoid python interprete \ as escapes.

#####3/11/2015

* talked w/ c about the new model and looked at the code. the structure og the Go (genome of the pathogen) will be a list of effectirs gene, each of it is ideally linked to a list of 0 and 1 for each target in the set of targets. In relaity it is implemented as a list of target w/ score > than 0 that are key to a dictionary w/ their scores. Moreover the score is not going to be really 1, but is going to be a score between 0 and 1. btw this is a binomial distribution so the probability to have n successes (1) over k trial (the targets) is described as such.
  the average number of successes will be lambdak +- the fluctuation (standard deviation, that is the same under sqrt), where lambda is the probability of success (how much the trial is biased). in our simulation labda has to be quite small cause we expect that the majority of the gene in the target pool will not be targeted. the code will get a random number from the binomial distribution and use it to determine the number of effectors of the host.
the problem now is to determine how to calclate the value r (same as in the previous dynamics population simulation), by the scores of each effector gene, so that it makes biological sense. the average is not really a good idea, cause it doesn't sense the additional vales. c had a formula that for each effector gives a scoe=re w that is a sigmoid, so we have a treshold (below the effector is not good), and a maximum (can't be better than that). these ws has to be synthetized in the score r i was talking about.

#####4/11/2015

* thinking about the score problem, i couldn't come out w/ anything. ros problems=nothing is working today

#####5/11/2015

* going trough **longest increasing subsequence** algorithms

* seminar on new technology (other file)

#####6/11/2015

* writing new code for plotting results of simulation for same DT or same Qi in different runs.

* useful example from tutorial to display standarc deviation as a colored area in plot:
  ```python
  mu1 = X1.mean(axis=1)
sigma1 = X1.std(axis=1)
mu2 = X2.mean(axis=1)
sigma2 = X2.std(axis=1)

# plot it!
fig, ax = plt.subplots(1)
ax.plot(t, mu1, lw=2, label='mean population 1', color='blue')
ax.plot(t, mu1, lw=2, label='mean population 2', color='yellow')
ax.fill_between(t, mu1+sigma1, mu1-sigma1, facecolor='blue', alpha=0.5)
ax.fill_between(t, mu2+sigma2, mu2-sigma2, facecolor='yellow', alpha=0.5)
ax.set_title('random walkers empirical $\mu$ and $\pm \sigma$ interval')
ax.legend(loc='upper left')
ax.set_xlabel('num steps')
ax.set_ylabel('position')
ax.grid()
  ```

* w/ the following draft code i created the following plots where we keep a constant value of c comparing the DTs (need to check the code w/ c cause im not 100% sure about how he's storing the data).
  ```python
  import pickle
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.ticker as mtick
import argparse
import os
plt.style.use('bmh')
parser=argparse.ArgumentParser(formatter_class=argparse.RawDescriptionHelpFormatter,epilog=("""
""")) ###*
########each directory has a different DT
parser.add_argument("p1",help="path to the right directory")
parser.add_argument("p2", help="path to the second directory")
parser.add_argument("p3", help="path to the third directory")
parser.add_argument("p4", help="path to the last directory")
parser.add_argument("r", type=int, help="number of runs for directory")
###*parser.add_argument("j", type=int, help="number of jumps")###*
args=parser.parse_args() ###*
pth1=args.p1
pth2=args.p2
pth3=args.p3
pth4=args.p4
RUNS=args.r
main_path=[pth1,pth2,pth3,pth4]
print pth1,pth2,pth3,pth4
###*xi=range(1,(args.j+1))###*
##############files with data##########################
n1=pth1+"CDATAVcomp.p"
n2=pth2+"CDATAVcomp.p"
n3=pth3+"CDATAVcomp.p"
n4=pth4+"CDATAVcomp.p"
print n1, n2, n3, n4
f1=open(n1,"rb")
NOPE1=pickle.load(f1)
f1.close()
f2=open(n2,"rb")
NOPE2=pickle.load(f2)
f2.close()
f3=open(n3,"rb")
NOPE3=pickle.load(f3)
f3.close()
f4=open(n4,"rb")
NOPE4=pickle.load(f4)

#######plot same Qi different DT#################
#print NOPE1[0][1], 'tempo?'
#print NOPE1[0][2]
'''fig, axesa = plt.subplots(1,figsize=(10, 8))
fig, axesb = plt.subplots(1,figsize=(10, 8))'''

'''axesb.set_ylabel("$< Number$ $of$ $units >_{Ens}$", fontsize=40)
axesb.set_xlabel("$Time$ $(Evolutionary$ $events)$",fontsize=40)
axesb.xaxis.set_tick_params(labelsize=20)
axesb.xaxis.set_major_formatter(mtick.FormatStrFormatter('%1.e'))
axesb.yaxis.set_tick_params(labelsize=20)
axesb.yaxis.set_major_formatter(mtick.FormatStrFormatter('%1.e'))'''

#Data=[t,LAV,NAV,STDN,STDL]
T1=NOPE1[0]
T2=NOPE2[0]
T3=NOPE3[0]
T4=NOPE4[0]

pts1=NOPE1[1].keys()
pts2=NOPE2[1].keys()
pts3=NOPE3[1].keys()
pts4=NOPE4[1].keys()
#print pts1, pts2, pts3, pts4
if pts1==pts2==pts3==pts4:
    print 'ok, proceed'
    c=0.1
for x in pts1:
    fig, axesa = plt.subplots(1,figsize=(10, 8))

    axesa.set_ylabel("$< Lengths >_{Ens}$", fontsize=40)
    axesa.set_xlabel("$Time$ $(Evolutionary$ $events)$",fontsize=40)
    axesa.xaxis.set_tick_params(labelsize=20)
    axesa.xaxis.set_major_formatter(mtick.FormatStrFormatter('%1.e'))
    axesa.yaxis.set_tick_params(labelsize=20)
    axesa.yaxis.set_major_formatter(mtick.FormatStrFormatter('%1.e'))

    axesa.plot(T1,NOPE1[1][x],label="$\Delta T=5.0\\times 10^3$")
    axesa.plot(T2,NOPE2[1][x],label="$\Delta T= 1.0\\times 10^4$")
    axesa.plot(T3,NOPE3[1][x],label="$\Delta T= 1.5 \\times 10^4$")
    axesa.plot(T4,NOPE4[1][x],label="$\Delta T= 2.0\\times 10^4$")

    axesa.legend(loc='best', fancybox=True, framealpha=0.5)

    val_c=c
    titstr='$c=$'+str(c)
    print titstr
    c+=0.1
    axesa.set_title(titstr, fontsize=40)

    #axesa.set_xscale('log')
    axesa.set_xlim([0,20000])
    #axesa.set_xlim([0,80000])

    fig.savefig(pth1+'trail_plot'+str(c-0.1)+'.png',format='png' ,dpi=1200, bbox_inches='tight')
  ```

  Here are the resulting plots:
  ![plot for c=0.1](https://www.dropbox.com/s/j62wtkk8z8fc4p8/trail_plot0.1.png?dl=1)

  ![plot for c=0.2](https://www.dropbox.com/s/vveewdh0a6j0vdv/trail_plot0.2.png?dl=1)

  ![plot for c=0.3](https://www.dropbox.com/s/a6piwy7wt2t0i43/trail_plot0.3.png?dl=1)

  ![plot for c=0.4](https://www.dropbox.com/s/9viylsfl2nhr56e/trail_plot0.4.png?dl=1)

  ![plot for c=0.5](https://www.dropbox.com/s/f7w9tu6hxptcpfi/trail_plot0.5.png?dl=1)

  ![plot for c=0.6](https://www.dropbox.com/s/zta38ws2po0vb9n/trail_plot0.6.png?dl=1)

  ![plot for c=0.7](https://www.dropbox.com/s/qmnyqrk6xlqo2jx/trail_plot0.7.png?dl=1)

  ![plot for c=0.8](https://www.dropbox.com/s/ixq44bfp6py8vz6/trail_plot0.8.png?dl=1)

  ![plot for c=0.9](https://www.dropbox.com/s/jrtfxx5e4p11jnl/trail_plot0.9.png?dl=1)

  NOTES: 
  * fixed the syntha of the title so that it all fits Tex and it's fancier
  * in the final version will need to fix the axes labells as in clusterV.py so that they can't be repeated

  OBSERVATIONS:
  * from these graphs it looks like the c value doesn't have such a great impact as i expected (actually none, how is this even possible? will talk to c, maybe i plotted something wrong, or it could have an effect visible just when we plot separately effectors gene and trasposable elements?). Regarding the impact of the jump frequency it looks like in all the cases DT5000 and DT10000 populations behave in the same manner, while the eveolution is slowed down in the case of DT15000 and DT2000 (other important question: how is it possible that i can't see the plateau phase i saw in the compV plots? this shouldn't happen, i need to check the plot code).

* read article from **Nathure Methods**
   > **_Assembly and diploid architecture of an individual human genome via single-molecule technologies_** (_Pendleton etal._)
   > Molecular maps have the potential to span regions of high simi- larity at great depth, as individual molecules can exceed 1 Mb in size. However, their nonrandom breakage can lead to systematic failures in detection. This limitation can be mitigated by creating multiple genome maps that use distinct recognition sequences (using high-quality sequence contigs to bridge across maps). Resolving repetitive regions is more than simply an issue of ‘com- pleteness’; these regions have been shown to mediate large-scale rearrangements in the genome
   > This study provides a framework for integrating multiple platforms: high-quality short reads for SNVs and indels, long reads for structural variation, and long-read assembly and genome maps for large-scale genome rearrangements. By using a collection of technologies, we can finally begin to circumvent biases induced by overreliance on a single reference genome

* very useful python synthax: **\*args** send to a function a variable number of NON-KEYWORDED variables. on the other side **\*\*kwargs** does the same but allows to send NAMED ARGUMENTS to a function (i.e. x where 2 was assigned to x). then u can iterate over **args** or **kwargs**. Note that only the synthax is needed (the one/two star/s), but is common practice to keep these names (so do it). they could be used when calling a function, too, but i find this case less useful.

#####9/11/2015

* NOTE on python: ***for key in d** is the same as **for key in d.keys()** but w/ a better perfromance.

* NOTE on python: Dictionaries have a 'get()' method. If you do d['key'] and key isn't there, you get an exception. If you do d.get('key'), you get back None if 'key' isn't there. You can add a second argument to get that item back instead of None, eg: d.get('key', 0).

* changed the **comparison_plot.py** code so that it produces two sets of images, the first one just like the previous week, the new one plotting not just the total length over time, but the length of effector genes and the length of the TEs over time.
  Again i see the same as the last week, so there is no (or almost no) difference between c values, while there is a small difference depending on the DT between jumps. (not necessarely in the order u can imagine). Moreover i can't see the plateau phase i was expeting (why this? i looked at clusterV code and it looks like I'm plotting the right arrays????)

* IMPORTANT NOTE i forgot on the model: it will be interesting to see if pathogen A jumped to host 2 from host 1 can return after some DT to the original host and w/ which fitness value (better? worse? there will be another pathogen at his place? can he defeat it?).

* 3 of the 4 (all except DT5000) simulations at the very last run crushed w/
  ```bash
  IOError: [Errno 122] Disk quota exceeded: '../RUN49/n8/pts13plotdata.p'
963 377
../RUN49/n8/pts13plotdata.p
  ```

#####10/11/2015

* so the cluster had a problem (run out of space?), so i killed the programs runnig and launch them again just for the remaing runs (47 to 49 for DT5000, just 49 for the other three) w/ a different seed (the old seed are in meta files).

* example of the plot for TEs and Eff length created yesterday (just one cause they're more or less the same)
  ![trial plot for length of Eff and TEs over time for different time gap between jumps](https://www.dropbox.com/s/1af9j8qrem8s96m/trial_plot_eff_te0.5.png?dl=1)

* i made a mistake launching the simulation for DT5000, so for the way the code is wrtitten is doing again RUN46, BUT it's saving data proceedeng w/ the numbers in plot, i'll need to erase the plot w/ numbers>40 (or put them in another folder w/ different run number).

* in **comparison_plot.py** added part to plot number of units (total and differentiating between effector genes and transposable elements) over time, keeping the same C value and comparing different DTs.

* the plot are fine, in the previous code **clusterV.py** i was just plotting more time on the x axis. I can change this (i should as I'm only plotting 20000 evolutionary evenets that is the same interval as the last jumping strain I'm considering)
  here is another example for 50000 evolutionary events:
  ![length of eff and TEs for different DT](https://www.dropbox.com/s/j7cczpo4gm8gfz5/trial_plot_eff_te0.1.png?dl=1)

#####11/11/2015

* so the code i run yesterday for DT5000 started at RUN46 instead of 47 (my bad). as said it didn't overwrite the previous results, so i just manually created folder **RUN49** and moved there the new files, then renamed them so that the numbers go from 1 to 40 and not from 41 to 80. that said RUN49 is actually the forst run w/ the third seed, 47 is the second and 48 the third. (if for any reason i need to recreate the same exact results of this simultaion).

* the plotting **comaprison_var.py** code finished and here as some figures (always just on the firs 20 runs for each DT, will do more today)
  plot for the same c, comparing different DTs, total number of units over time (just one cause they all look the same for different c values)
  ![plot number of units over time](https://www.dropbox.com/s/v9vvfhhazzqkwqs/trial_plot_unit0.5.png?dl=1)
  note the strange swap between the blu and magenta lines: i see that one for all c values, if it's a seed artifact it should go away at least in some plot when i run the code over the whole 50 runs. (i will add the simulation with no jumps too)
  ![same but distinguish tes and effector genes](https://www.dropbox.com/s/lrsgxlgtqzgdmkj/trial_plot_unit_eff_Te0.5.png?dl=1)

* modified the code **comparison_plot.py** so that the color stays the same in different plots for the same DT. added part to plot number of units of TEs and effector genes in differentc c vakues but for the same DT (expected 4 plots). (i made a mostake here cause i din't tell to make dotted line for tes, but i'll wait to see if the code is fine and chiange it later). All the plots generated are now going to the **~/images/** folder.

* NOTE: RUN **CLUSTERV.PY** BEFORE **COMPARISON_PLOT.PY** FOR THE 50 RUNS!!!

* modified the code again to get the nice color stay the same for each c despite being te or eff data. (don't have previous plot cause of a type mistake)

* TO DO:
    1. ~~check how many n/ are in **new** folder and determine how to use it~~
    2. ~~when it's fine insert that simulation in **comparison_plot.py** too~~
    3. ~~run **clusterV.py** for each DT for all 50 runs to get CDATAV for comparison_plot.py~~
    4. ~~run comparison_plot on everything!!!~~

* inserted after #* and till line 78 lines in code to add **new** to the plots

#####12/11/2015

* the code sropped w/ error 1 ValueError: x and y must have same first dimension
  I'm adding assert at the biginning to check if the assumption T1=T2=T3=T4 is correct (should be). Well actually it raised an AssertionError and that should be because we approximate for DT15000 number of jumps to 13 (closest integer). I changed the assert to compare just the other three values and that should work i believe. I changed the lines so that they consider the time of the y values and not just the same value for all the data. (the new assertion works so that was ht eproblem!!) i added infinity to the plots comparing DT.

* looking for a way to calculate the derivatives

* changed line style for TEs from '--' to ':' to meake plots more clear

* given the result about the length it looks like for the same DT the length forthe effector genes is constant for any value of c, while, as it makes sense, the length of the TEs is more randomic, even if it possible to see an average that goes to a max value.

* trying to plot the derivatives for each plot in a new figure w/ np.polyfit function --> need to check i'm doing it right and creating a new plot for this.

* changed the config.mk file so that clusterV.py consider 50 runs

* got back to dashed line cause it was better, derivateives was not correct, strted again, will ask c for the last plots

* matplotlib tutorial at http://www.labri.fr/perso/nrougier/teaching/matplotlib/

#####13/11/2015

* clusterV.py on the four DT folders is completed. I've just launched the **comparison_var.py** on all the runs (i think it will take at least a couple of hours), the old images are in **images/images_first_20_runs/**.

* added plot for derivatives of each plot as c explained (stop just launche docde to check faster for error). added labels to the two series of data of TEs and effectors (check this when output the first image!!!). Also, I changed the time on the x axis so that it plot result to 200000 evolutionary events (that is the length of the simulation).

* i'm using the numpy function diff to calculate the derivatives (before doing that I'm making the lists numpy arrays). The funcion on a list X=[x1,x2,x3...xn] calculates a new list Y=[x2-x1,x3-x2,...,xn-xn-1], of course Y will have one element less than X, so I had to change the time list to be plotted and I used T[1:].

* //Arduino meeting//

* got Overflow error (don't get why given I'm using more or less the same data and in the same quantity as before, looked in the web and there is not real solution to this except sampling before plotting -this would be fine given the large amount of data i have-, anyway i'm trying overcome the program closing the images after saving (i wasn't doing that).

* i'm keeping the first serie of plots (commented it before running again).

* so i still get the overflowerror, I'm now trying to sample the derivatives list averaging over 10 values each time. (i deleted the T in plotting for semplicity, cause it should work automatically).

#####16/11/2015

* i had again OverflowError during the weekend, I diveded the script in two (**comparison_plot.py** and **comparison_plot_derivatives.py**) so that in the meanwhile I try to fix that i can proceed working on labels and so on in the main code.

* using the averaging function: no more overflowerror. Fixing labels in the plots, with white alpha channels. The derivative plot is not very informative as it is so i'm setting the limits of the axis to see better just the interesting part

* finally here is a list of all the full name colors available in matplotlib: http://matplotlib.org/examples/color/named_colors.html

* fixed (hopely) annotations w/ position, size, background color (white w/ alpha channel .5) and shape. changed names of y axis for derivatives plot in Delta over T.

* branched master of **model_scripts** for the two separate files for plotting data and their derivatives (name **separate_plottig_der**)

* now i get (on both codes): **ValueError: width and height must each be below 32768**. since the only "important" thing i changed, except for annotations that i don't think can be the problem was adding plt.close() after each plot as suggested in the web to make it faster i deleted it and i'm trying again (on both).

#####17/11/2015

* fixed the ValueError (the annotation were pushing the image size to be wrong, that cause i was using -1000 on all the plots but the y axis range is actually changing).

* launched both codes on 50 runs (will put the code toghtther? or meybe not for velocity reasons?). Changed yaxis limits (and x too) for derivatives plot so that we can se better the interesting part. Again, it looks like c as no effects.

* started to write code to plot distribution of length of effector genes and TEs (starting from pts#plotdata.p), it is **~/model_scripts/histogram_plots.py**.

#####18/11/2015

* fixing problems in **histogram_plots.py** script. Note that the properties of hist are a little different form the ones of the other plot i used, so c is not ok to define a color and '--' is not ok, but i should use 'dashed'. changed figsize, added common title with **suptitle** (one figure w/ two subplots), using **normed=1** to scale the frequency among different DTs (also, this way i can just ignore the different number of jumps for each time interval, that caused DT5000 to seem much higher in all frequencies).

* stored the full list of images and derivates in a zip file in dropbox for c to see them

#####19/11/2015

* going on w/ **histogram_plots.py** script. I need to add a common legend to the images. (note  that the scripts take a lot cause it is unpickling a huge number of files).

* note i forgot yesterday: i changed the number of bins in histogram, that is the number of frequency classes in the plot, default is 10, too low for this purpose. Now I'm creating a new class for 100 intervals.

* from the very first plot created (c=0.1) distribution of length for effector genes and TEs I can already see that:
  1. as already observed it doesn't look like there is a significant difference caused by c value and DT has his main effect on v, as it could be expected
  2. the effectors length reach a maximum and it is more or less a gaussian with center in 0 (need to check is gaussian and not some other curve but it looks like this and it agrees w/ lot of other biological observations), while the TEs lengths has a maximum (I think it is due to the simulation length itself), but the frequencies appear to stay the same for all the classes considered.

* created another version of the script that only consider the frequencies obtained at the end of the simulation time (i thought it would make more sense, especially for the TEs), the script is in the same folder as the other one and it's **histogram_plots_endtime.py**, the plots are saved in the subfolder **images/histograms/end_of_simulation_time/**

* fixed a bug and launche d both version again (assignment of new file name to check in the **new** folder was wrong due to forget change c_value to 'n0/' after copy paste the snippet of code). (noticed cause the curve for new was different in c=0.1 and other plots and it shouldn't)

* changed the script so that it creates a plot 2x2 where the first row is the beginning of the simulation frequency plot, and the second row the end of the simulation frequency plot, all comapring the different DTs used in simulation.

* changed the number of steps for TEs (still looks misleading to me), so that they are the same number as the steps for Effector genes.

#####20/11/2015

* modifying the code as c wrote me, ie we need histograms for every jumps (ill try doing a plot for each DT w/ all the jumps plus maybe some plots comparing the DTs for certain times (not all cause we have different number of jumps)). Second c suggested to use scatterplots. (will modify last plot to scatter too at the end).

* my idea 4 the plots:
  1. eff plot w/ 5 plot each one for a different DT, in each of them are dyspleyd all the jumps (each jump is a tick on the x axis)
  2. same but for TEs
  (will take huge amount of time to process all pickled files)

* of course there are too many that for that kind of plot, so otion two: i'm calculating frequencies and plotting a scatterplot for frequencies/time for each DT and c value comparing jumps (look from violet to red)

* so now **scatter_plot_jumps.py** is just a trial version that plot for DT5000 9 plots for the different c values considered but run just on RUN0.
  example of figure:
  ![plot frequencies DT5000 c=.1 RUN0 40 jumps](https://www.dropbox.com/s/7t9z4bt4sqlwicq/lendistribution_plot_eff0.1_5000.png?dl=1)

* the other script (**version2**) is plotting after reading all the file that correspond to the same jump in doifferent runs (again, same DT and c). I'm then dividing the frequency value for the number of runs considered, the plots look quite different (and i had to set a limit to x axis cause i had outlyers that didn't allow to see the plot as it should).
