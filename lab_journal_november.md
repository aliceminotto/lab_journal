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
