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
* catch up w/ some of the stuff on biocamp, downloaded some items to be read

#####2/10/2015

* so the data in A (carlos' file) were an array w/ two lists, one with the number of genes and one with the length
* reading this paper:
  
 > Large-Scale Genomic Analysis Suggests a Neutral Punctuated Dynamics of Transposable Elements in Bacterial Genomes
  
 _notes on this:_
* looking at the last C's script to plot the final figures and try to run it on the cluster
* go trough C's simplest model:
 ![model](https://raw.githubusercontent.com/adam-p/markdown-here/master/src/common/images/icon48.png) (file:///.file/id=6571367.22800420)
 basically we have Np (pathogen population, fixed), and Nh (host population, fixed). In Np we are considering Nte, the # of TE, and Neff, the # of effector genes. what we want is a simple model that shows how the genome length of this kind of pathogen is getting longer in the evolution (the model in theory should be fine for animals too, the thing is that in this last case things are more complicated, here we have that plants can;t move, so the pathigen has to do it, and doing this it should be able to change host species quite often, that could drive a faster evolution and a larger genome size). the size of the genome is calculate d Neff+Nte, considering their length (infact each gene or TE has its own list of characteristics like length, score for fitness).
we can have a series of events (shown in figure), each w/ its own probability (given in the model after read some paper on real data set). note that we are not considering, at the moment, events of TE mutations, because we're supposing they basically just get disrupted after a mutation, cause they just have transposase activity. Plus we are considering the event a TE is inserted in an effector gene, and here we could or not consider the effector in the count (this issue is being considered right now).
there will be a more complex model that for instance will consider pathogen effectors and their target, so we don't just get a fitness number (that by the way changes each jump), but it's a matching model. Moreover it will be considered the possibility that a mutation or an effector gene after a jump is not just worst than before, but it can harm the pathogen, causing its extinction. 
