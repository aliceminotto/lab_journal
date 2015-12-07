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
