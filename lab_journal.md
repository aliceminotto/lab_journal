##Lab journal  
####_Alice Minotto_

#####29 and 30/09/2015

* downloaded Anaconda (already with the numpy library).
* updated Ipython (use the command _jupyter notebook &_ to open the tab)
* set up a git[hub] account and read about how to use it

* took a look at Carlos' scripts and tried them in the notebook to get plots.  
 **need to use the line _% matplotlib inline_ somewhere at the beginning of the script to make pictures display in the browser**

#####1/10/2015

* read markdown tutorial and began the journal lab (i hope)   
* lab journal is now online in my github account (remember that i had to change the file name adding *.md to make it be displayed in the right way)  
 _notes for myself to remember: it looks like I have to committ deleted files too unless i want to pull and merge each time, plus this way should prevent me to dlete it manually online_
* read some vim tutorial to have an alternative to gedit (still to be downloaded), and of course used it
* catch up w/ some of the stuff on basecamp, downloaded some items to be read

#####2/10/2015

* so the data in A (carlos' file) were an array w/ two lists, one with the number of genes and one with the length
* reading this paper:
  
 > Large-Scale Genomic Analysis Suggests a Neutral Punctuated Dynamics of Transposable Elements in Bacterial Genomes
  
 _notes on this:_
 > _Estimations of the fitness cost of IS elements by comparing a simple model with the genomic data available for the IS5 family [28] have found that the fitness cost is small enough to assume that, in practice, IS may be neutral or almost neutral for the host genome._
* looking at the last C's script to plot the final figures and run it on the cluster
 to get in the cluster i need to write in the terminal: **_ssh hpc.tsl.ac.uk_**
* go trough C's simplest model:
 ![model] (https://cdn.rawgit.com/aliceminotto/lab_journal/master/transformsnew2.svg)
 
 basically we have Np (pathogen population, fixed), and Nh (host population, fixed). In Np we are considering Nte, the # of TE, and Neff, the # of effector genes. what we want is a simple model that shows how the genome length of this kind of pathogen is getting longer in the evolution (the model in theory should be fine for animals too, the thing is that in this last case things are more complicated, here we have that plants can;t move, so the pathigen has to do it, and doing this it should be able to change host species quite often, that could drive a faster evolution and a larger genome size). the size of the genome is calculate d Neff+Nte, considering their length (infact each gene or TE has its own list of characteristics like length, score for fitness).
we can have a series of events (shown in figure), each w/ its own probability (given in the model after read some paper on real data set). note that we are not considering, at the moment, events of TE mutations, because we're supposing they basically just get disrupted after a mutation, cause they just have transposase activity. Plus we are considering the event a TE is inserted in an effector gene, and here we could or not consider the effector in the count (this issue is being considered right now).
there will be a more complex model that for instance will consider pathogen effectors and their target, so we don't just get a fitness number (that by the way changes each jump), but it's a matching model. Moreover it will be considered the possibility that a mutation or an effector gene after a jump is not just worst than before, but it can harm the pathogen, causing its extinction.
* running mprocstest.py to get the data, looking at the code:

 _notes for myself to remember: floor (in math lib) return the biggest int number <= of its argument_

 _rng in pygsl it's the random number generator, and it needs a seed to be set. if u give the same seed multiple times u'll end up w/ the same results again and again_

 _m1 to m8 are the different probability for each event considered in the model, just look at the comment lines to get which one_

 _uniform(low, high, size) returns a sample from a uniform distribution

 _the line **Lth=floor((RXCLRPTS[0]+CRKPTS[0]+TES[0])*(1.0/3.0)*(av1+av2+av3))** is calculating a treshold value, the last part is an average of avrages then multiplied for the total number of genes, see at the drawing in the exercise book to get what this treshold is

####_work in progress/to do list_

* read C's paper
* find a way to fix git issues
* get gedit on the cluster (ask m?)
* get trhough C's scripts and run them in the cluster (in progress, will take a few days), then try to change some numbers, eg the probabilities or the seed and run again
* run the last notebook script to get the final graphs 
* install pygsl locally
