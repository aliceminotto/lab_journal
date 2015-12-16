##**Lab Journal**
####**_December_**
###**_Alice Minotto_**

#####1/12/2015

* finishing HTML tutorial

* reading:
  >_Review. Random walk models in biology_  
  > E. A. Codling _et al._

* fixed images in the **new** folder w/ c 4 the paper: changed the dimesion of the zoom insert in **randomwalk.png**, make it black and with dots instead of circles, commented the style so that all the plots are as plain as possible. Changed the axis format to be scientific and without repetitions ('%2.1e' means 2 digits before the dot and one after), corrected a typo in legend. Zip all the folder. These are going to be used as references for the model, because they represent the "standard" behaviour.

#####2/12/2015

* downloaded and installed components (node.js and others) for tomorrow workshop, looking at the basic documentation

* reading:
  > **_Oxford Nanopore sequencing, hybrid error correction, and de novo assembly of a eukaryotic genome_**  
  > Goodwin _et al._  
  > [...]The advantages of this approach include potentially very long and unbiased sequence reads, because neither amplification nor chemical reactions are necessary for sequencing[...]  
  > This device, the MinION, is a nanopore-based device in which pores are embedded in a membrane placed over an electrical detection grid. As DNA molecules pass through the pores, they create measureable alterations in the ionic current. The fluctuations are sequence dependent and thus can be used by a base-calling algorithm to infer the sequence of nucleotides in each molecule[...]both strands are sequenced, a consensus sequence of the molecule can be produced; these consensus reads are termed “2D reads” and have generally higher accuracy than reads from only a single pass of the molecule (“1D reads”).[...]
  > However, both the “1D” and “2D” read types currently have a high error rate that limits their direct application [...] and necessitates a new suite of algorithms.  
  > _after alignment w/ different sofware just a minority of 1D reads aligned, and just a little more than half of the 2D reads_  
  > [...] fragments longer than 80 kb are virtually unalignable.[...]  
  > For longer reads (>50 kb), only portions of the reads can be successfully aligned, which suggests that reads are composed of both high- and low-quality segments. However, this local variability in quality does not seem to be position specific, and on average the per-base error rate is consistent across the length of a read [...]  
  > Between 20% and 60% GC content, the coverage is essentially uniform,[...]  
  > To demonstrate the utility of the long reads, we attempted to assemble the yeast genome de novo using the Celera Assembler, which can assemble low-error-rate reads up to 500 kbp long. However, when raw nanopore reads were given to the assembler, not one single contig was assembled, and it became apparent that error correction was critical to the success of the assembly. Consequently, we developed a novel algorithm called Nanocorr to error correct the reads [...]  
  > Nanocorr uses a hybrid strategy for error correction, using high-quality MiSeq short reads to error correct the long but highly erroneous nanopore reads. It follows the design of hybrid error correction pipelines for PacBio long-read sequencing [...] although in our testing none of the available algorithms were capable of utilizing the nanopore reads [...] Nanocorr begins by aligning the short MiSeq reads to the long nanopore reads using the BLAST sequence aligner [...] Nanocorr uses a dynamic programming algorithm based on the longest-increasing-subsequence (LIS) problem to select the optimal set of short read alignments that span each long read [...] The error-corrected long reads can be used for any purpose, especially de novo genome assembly [...] the N50 contig length for the Oxford Nanopore-based assembly is 678 kbp compared to ∼60 kbp for the Illumina assembly [...]  
  > We then assembled those reads with the Celera Assembler, which follows an overlap-layout-consensus approach without decomposing the long reads into k-mers as is used in de Bruijn graph assemblers. [...] Upon alignment to the reference sequence, we found that >99% of the reference genome aligned to our assembly and the per-base accuracy of our assembly was >99.78%. [...]  We find that the best result was achieved by using the data from just the top three flow cells, representing ∼30× raw coverage of the genome [...]  
  > The results of this study indicate that the Oxford Nanopore sequence data currently have substantial errors (∼5% to 40% error) and a high proportion of reads that completely fail to align (∼50%). This is likely due to the challenges of the signal processing the ionic current measurements [...] as well as the challenges inherent in any type of single-molecule sequencing [...] ionic signal measurements are not of individual nucleotides but of ∼5 nt at a time. Consequently, the base calling must individually recognize at least 45 = 1024 possible states of ionic current for each possible 5-mer. We also observed the potential for some bias in the signal processing and base caller, particularly for homopolymers. [...]

* going through C++ tutorial. This is very interesting:
  ```c++  
a>b ? a : b      // evaluates to whichever is greater, a or b. 
  ```

#####3/12/2015

* **C++**: i can do this
  ```c++
  #include <iostream>
#include <sstream>
using namespace std;

int main () {
    string a;
    string b;
    getline (cin, a);
    cin >> b;
    cout << a << "\n";
    cout << b << "\n";
    int intero;
    stringstream(b) >> intero;
    cout << intero+10 << "\n";
}  
  ```
  but note that if i give b a string of letters instead of a number the last passage doesn't raise an error, it just returns 10 (b is considered to be 0 confermed by the fact i get an error if i try to divide by b="word").

  Interesting syntax: ```do statement while (condition);```, in this case the while loop will be executed at least once cause the condition is evaluated after the first execution.
  In a ```for``` loop i can skip all the three fields: initialization, condition or increase, note that with no initialization or increase this is basically a ```while``` loop. a ```for``` loop w/ no condition is equivalent to python ```while True```. to execute more than one expression in a field they need to be saparated by comma. Another available synta is ```for ( declaration : range ) statement;``` that is the same as python ```for element in iterable```.
  If i want to moduify a variable (global) from inside a function that received it as a parameter, i will need to put an ```&``` after the type in the parameter declaration. This will actually change the value of the global variable.
  ALSO keep in mind that usoing references instead of values can result in a big improvement in case the program has to create a copy of some big object (like long lists).

#####4/12/2015

* **C++**: a function can be called with optional values, ie tha last parameter has to be given a default value to be used IF the function is called w/ less parameters. So for example:
  ```c++
#include <iostream>
using namespace std;

int somma (int a, int b=1)
{
int res;
res=a+b;
return (res);
}

int main ()
{
cout << somma(5) << "\n";
cout << somma(5,4) << "\n";
return 0;
}
```
is going to print to standard output ```6``` and ```9```. Tha last return 0 is optional and just means that main terminated w/ no errors (main returns an interger, and it is 0 if everything was fine).

* **Javascript**: 
  > Since || returns first operand if the first operand is truthy and the second operand if the first operand is falsy, the construct value || defaultValue returns value if value is not undefined and defaultValue if value is undefined.

  > Trying to access a property of an object that doesn't
// exist returns undefined (it does not throw an error).

  > you can access elements 
// beyond the length of the array without
// having any error thrown; it simply returns
// undefined.

  > http://overapi.com/javascript/

#####7/12/2015

* had a long meeting about the new model to code in the new simulation. started the code w/ c. wrote the main function (parallelized with ```os.fork```), the import script and the two function ```NEWHOST()``` and ```NEWPATHOGEN()``` to create the new host and the new pathogen. the new pathogen is just created at the beginning of each simulation, while, also at the beginning, we are creatin a list of hosts, one for each jump. each host is characterized by a list of effector enes randomly selected from the pool (random length in a certain defined range).
  Each pathogen is implemented as a dictionary of effector genes, each one is a dictionary with keys the targeted genes and values the score of this connection. Will need to have a funciton for the evolution of the pathogen and one to calculate the fitness, the fitness will depend on how many and how much the genes present in the host are targeted by the pathogen, BUT each gene can be targeted wioth a maximum score of 1, despite the number of effector genes that are linked to it (because more makes no biologicalk sense anyway), at the end we can weigth the score considering the length of the list of target genes.

#####8/12/2015

* went on with the writing of the code w/ c, wrote the functions for the evolutionary process: mutation (this include mutation of the score of a given effector for all its target, possibility of gain a new target with random score, and possibility to lose a random target), deletion (this is also influenced implicity by the probability of a given effector to be silenced by the movement/gain of a TE), duplication and horizontal gene transfer.
  There's always the need to keep track of the previous population, so took care of deep copy the dictionary representing the pathogen genome before manipulating it with these functions (that are all stored in another file, imported by mda).
  The probability of gaining or losing a target for an effector are given in the code in the probability array but can be changed as wanted.
  Will need to calculate the probabilities for every transformation to happen (think about how to do this!!!).
  Wrote also the function to calcuate the scores, fopr each target in the host genome, for each effector in the pathogen genome (store them in two different dictionaries). For the first one I have two different implementation to be tested, what I thought and what c did: they are qualitatively the same but have some quantity difference with each other, they return the same kind of object (as I said, a dictionary), so they can be exchanged easily.

* as the main program is in the ```main()``` function that was called at the end of the main file, i added the line ```if __name__=="__main__": main()```. this make the syntax works like in C or others programming language. Anyway in this particoular case it shoukldn't matter, but it is good preactice cause it prevents the main code being executed if for any reason I want to import the file as a module in another code to use its functions. (otherwise it would be immidiatly eecuted)

* arduino meeting.

#####9/12/2015

* put import at the beginning of all the modules instead of using dependency injection so that the modules can be tested by themself and it looks like:
  > it will not re-load the module but will add it to subtwo's namespace so subtwo can use it.
  (that was exactly what i was worried about)
  This is also suggested in the PEP 0008 guide, and for our Zen ```Readability counts```
  Moreover:
  > Imports are always put at the top of the file, just after any module comments and docstrings, and before module globals and constants.

* about the style: it is ok to break a long line w/ two different styles options, my favourite would be _hanging indent_, in this case remember that no arguments can sit in the first line (of course all has to be inside braces), and use 2 tab instead of one to make clear that this is not a block. For example:
  ```python
>>> def guida(
...             argomento1,argomento2,
...             argomento3):
...     print argomento1,argomento2,argomento3
...
>>> guida('ciao','a','tutti')
ciao a tutti
```
  Moreover:
  > Use ```''.startswith()``` and ```''.endswith()``` instead of string slicing to check for prefixes or suffixes.
  > ```startswith()``` and ```endswith()``` are cleaner and less error prone. 

  > For sequences, (strings, lists, tuples), use the fact that empty sequences are false.

* so sent c an idea about how to handle the transformation probabilities. since the effector genes are organized in island just like the bacterial pathogenica island it could make sense (let's see what c says) to consider group of effectors genes as cluster and calculate the probabilty of transformation according to the score of the cluster and not that of the single gene. this would be both easier to code and would take into account **genetic draft** and **background selection**. Moreover i was afraid that then the need to another transformation (ie recombination) would arise, but in the same Kamoun's papaer it is stated that these islands are characterized by **mesosynteny**, ie conservation of gene content but not gene order or orientation (that we are not considering in this model).  
  INTERRRRRRESTINGGGG: mesosynteny is typical of fungi!!! From the dictionary of Genomics, Transcriptomics and Proteomics (and many papers online):
  > A special type of sequence conservation between fungal species, characterized by a retained gene content, but shuffled gene order and orientation. In the concept of meso-synteny, intra-, but not inter-chromosomal translocation are allowed.

#####10/12/2015

* update: the mesosinteny idea is originally from; http://www.genomebiology.com/2011/12/5/R45
  It also looks like the evolution is so fast in these organisms that can be actually observed in fields in seasons time (the generation time is ~hours? i previously read something very different about it stating that they are annual?).

* going on w/ the coding, add transformation function to define probabilities for the possible events (c formulas): mutation (w/ all its possibilities), duplication, deletion, hgt, nothing happens. Of course the last one will always be the most probable one. Also added the function, taken from my previous code, for the population dynamics (it depends from the size of population at time -1, size of host population, fitness of the pathogen and fitness of all the other strains).
  To do:
  * define when to introduce a new strain (note that in the formulas we are already considering a driven evolution cause we don;t care about all the mutations that case the pathogen to be less fit cause that it going to disappear in long term).
  * also call the function to define probabilities and events inside the transformation function and not one after the other for code stability
  * test the program (the function already are) and pay attention in particoular to the deep copy of the dictionary 
 
 Also. take a look here for the way we are defining which of the events (mutation-duplication-deletion-hgt-nothing) is appening for the given effector: https://en.wikipedia.org/wiki/Gillespie_algorithm

#####11/12/2015

* link to the Gillespie Algorithm (that btw is very expensive so it is usually semplified using next reaction method or tau-leaping <--look for them!!!): http://pubs.acs.org/doi/pdf/10.1021/j100540a008 
  From the paper:
  > [...]the stochastic approach regards the time evolution as a kind of random-walk process which is governed by a single dif- ferential-difference equation (the “master equation”.[...]the stochastic master equation is often mathematically intractable. [...] 

* TO DO: when c replies my email, rewrite the code w/ classes to make it more efficient!!!

* looked at **_namedtuple()_**, still i think classes would be better here

#####14/12/2015

* rewriting the model with classes so increase performance and readibility, need to add population dynamics and jumps too (in this order)

#####15/12/2015

* going on w/ yesterday job

#####16/12/2015

* still working on the code. Main problem now: the code is working, but for some magic, even if given a <code>random.seed()</code> in the main file, before calling any other function in other modules, the results of the simulation are not always the same (??????????????????????????????????????????????????).  
  Worse, they are the same in the previous code i wrote, and i kept all the function in the modules almost the same (except to have the need t use classes this time). Anyway on the plus side, the original code seems to work fine, so we can still use that one.
