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
 ![model] (https://www.dropbox.com/s/sznv7nm5mt9lbu5/transformsnew2.svg?dl=1)
 
 basically we have Np (pathogen population, fixed), and Nh (host population, fixed). In Np we are considering Nte, the # of TE, and Neff, the # of effector genes. what we want is a simple model that shows how the genome length of this kind of pathogen is getting longer in the evolution (the model in theory should be fine for animals too, the thing is that in this last case things are more complicated, here we have that plants can;t move, so the pathigen has to do it, and doing this it should be able to change host species quite often, that could drive a faster evolution and a larger genome size). the size of the genome is calculate d Neff+Nte, considering their length (infact each gene or TE has its own list of characteristics like length, score for fitness).
we can have a series of events (shown in figure), each w/ its own probability (given in the model after read some paper on real data set). note that we are not considering, at the moment, events of TE mutations, because we're supposing they basically just get disrupted after a mutation, cause they just have transposase activity. Plus we are considering the event a TE is inserted in an effector gene, and here we could or not consider the effector in the count (this issue is being considered right now).
there will be a more complex model that for instance will consider pathogen effectors and their target, so we don't just get a fitness number (that by the way changes each jump), but it's a matching model. Moreover it will be considered the possibility that a mutation or an effector gene after a jump is not just worst than before, but it can harm the pathogen, causing its extinction.
* running mprocstest.py to get the data, looking at the code:

 _notes for myself to remember: floor (in math lib) return the biggest int number <= of its argument_

 _rng in pygsl it's the random number generator, and it needs a seed to be set. if u give the same seed multiple times u'll end up w/ the same results again and again_

 _m1 to m8 are the different probability for each event considered in the model, just look at the comment lines to get which one_

 _uniform(low, high, size) returns a sample from a uniform distribution_

 _the line **Lth=floor((RXCLRPTS[0]+CRKPTS[0]+TES[0])*(1.0/3.0)*(av1+av2+av3))** is calculating a treshold value, the last part is an average of avrages then multiplied for the total number of genes, see at the drawing in the exercise book to get what this treshold is_

#####5/10/2015

* read the paper

> Biological applications of the theory of birth-and-death processes.

* installed atom as an editor

* learned to mount this computer as a volume in the cluster (in the bar, connect to server, after logging in)

* I need a bash script to launch program in the cluster.

* stopped the script launche don Fri, changed the script so that there are no jumps (ie the new score is just the same as the old one, while before there was a modification + or - their initial score), moreover removed the orinting of plots from the code, this way the program is running much faster.

* after looking at the plot created in the notebbok and seen everything is fine changed the seed (cause in one of the run i had extinction so the folder was empty) and run the simulation again in 50 runs. now i'm waiting for it tpo finish: even without creating all the graphs i think it will take some days. after that the plan is to do it again and again each time slightly modifying the c (for the evolution in jumps i think)

_NB i get a mail from the cluster when a process is killed, gives an error and die and when it finishes_

#####6/10/2015

* discussed w/ c about the models. the simpler one is just as i've alredy take notes as. I'm running the code (this time c=Qi in code IS changing, meaning that we have jump events w/ changes of score for a number of effector genes.
 
 I'm doing 20 RUNS for each of this:
  * DT=5000, JUMPS=40
  * DT=10000, JUMPS=20
  * DT=15000, JUMPS=13 (the integer that most resemble the real number for the condition below)
  * DT=20000, JUMPS=10

 All these parameters are chosen so that DT is an arbitrarial interval of time (expressed in evolutionary events) between two jumps from/to different host.
 Moreover we want to consider always the same interval of time, so the number are chosen so that DT*JUMPS always give the same results. (again i commented the code to create figures in here to make it faster and each time i used a diifferent seed)
 other general notes: in the more sophisticated model we are considering connection between effectors gene and their target, so we need to consider not just the pathogen population, but the host population too. for the cases of interested we are considering a host population Nh, where Nh is constant in time: this is because we are considering something like a small area, so the host is going to become exctincetd, but in this case the pathogen will be exctincetd to and we don't care, or the Nh has to be >> Np.
  each effector will be characterized not just by [s,l] as before (score/expression, length), but by a list of attributes in the following form:
  eff=[s,l,[list of targets], where s is actually going to be another list because we will have different scores for different targets.

  when there is a jump, as before, we will randomly change this score (and so the fitness, that more or less is calculated as a sum of the score for the links eff-target that are present for the pair pathogen-host that we are considering), this can also modify the list of targets recognized by the effector. But each jump we are also going to create a random new host as a subset of length L of the set of all the known target. this way we are going to see a lot of excinction.

 the fact is we are introducing sometimes new strains, so we don't just have a population of pathogens, but a number of different strains. Each time an evolutionary events occurs we are going to extimate the fitness of the new organism, if it's worst than the previous one we are not considering this case cause this is not going to be fixed, but if the fitness score is >= than the previous we create a new strain, that from now on will evolve indipendently form the other one.

 In this new model we consider time as realistic, in fact each mutation event will be considered as seasonal (this pathogens are), so we are going to have a jump, let's say, once in 5000 years, for exaple. every time there is an evolutionary event we consider each organism per se and each one of its gene and we use the probabilities in the model to decide if there will be a duplication/deletion/silensing/mutation. (the formula in the model suppose that the duplication rate is lower if the pathogen is alredy well fitted to the host, moreover it's considering a max capacity for the number of gene that can be present in a genome, and an ideal max number of nucleotides that can be present because of polymer extention capacity [i actually want to check if this kind of organism could take in additional chrs cause in this case we should set this treshold very high).  

* reading a lot of stuff on working in parallel w/ python (multiprocessing and pp)

#####7/10/2015

* the code running 50x for c=0 finished with exctinctions in 2 runs (18 and 49), now waiting for carlos to find a way to check the results without using the notebook, given that i can't upload all this stuff on this computer. (I'll probably just try to do it by myself later)

* i probably found a way to display the model image above: i hosted it in my dropbox, got the link to it. what you have to do then is to change the end of the link from _?dl=0_ to _?dl=1_ -just like when i coded the games-

* talked to martin about getting involved in one of the projects he's working on

* tried to modify the CLUSTERV notebook script to run in the cluster but i get an error when the code tries to save images (_RuntimeError: Could not allocate memory for image_).
  Correction: it works (I don't know what happened before), but I had to comment the saving of jpg images cause i kept having the error they are not supported. I don't think there is something of particoular interest/strange in this images, but we need them to copare them with the situation of evolutionary jumps from one host to another.

  here's the images:
  
  ![first graph, length over evolutionary time](https://www.dropbox.com/s/8jmp98f2op9z58a/typrunlength.png?dl=1)

  ![second graph. number of genes over evolutionary time](https://www.dropbox.com/s/wc0wk4io4st6sg5/typrunnumbers.png?dl=1)

  ![3rd graph, ratio Transposable Element/Effector Genes](https://www.dropbox.com/s/s367fjxe156jre3/randomwalk.png?dl=1)

  ![4th graph, average of the 1st](https://www.dropbox.com/s/wh8jgouikhjpias/averagesl.png?dl=1)

  ![5th graph, average of the 2nd](https://www.dropbox.com/s/t0s90hxqik0bgvi/averagesn.png?dl=1)

#####8/10/2015

* meeting w/ dan about models and what to do in the next months:
  * first: create a make file (see to do list below, so i'm reading about it, at the moment i don' really get why i should use make if i don't have to compile stuff)
  * during spare time i need to read about the main algorithms that are already used in libraries
  * create a database w/ c's model results w/ m?
  * use methods and programs to check/test my code

* going trough make documentation, the advantage is that it will create the output if and just if the prerequisites have changed after its last creation

#####9/10/2015

* finished make tutorial:

 > Automated build tools such as Make can help us in a number of ways. They help us to automate repetitive commands and, so, save us time and reduce the risk of us making errors we might make if running these commands manually.
 They can also save time by ensuring that automatically-generated artefacts (such as data files or plots) are only recreated when the files that were used to create these have changed in some way.
 Through their notion of targets, dependencies and actions they serve as a form of documentation, recording dependencies between code, scripts, tools, configurations, raw data, derived data, plots and papers.

 if i need it the link is: **http://swcarpentry.github.io/make-novice/**

* m explained me the very basics of schemas, so i basically got two (or more of course) tables, each line is an entry, and each line has got its own ID. the other table is constructed the same way (but w/ lines and colums w/ diferent meaning, but again each line has its own ID (this time the ID don't have to be unique, because it's linking that entry to the one in the other table. so m's example is fb: we got a table w/ all the people signed up, each w/ its very own ID. we can have another table w/ each line correspondiong to a post, in each line we have also the id of the person who posted it, in tjhis way we can link each post to the person and if we want we can extract a list of all the posts of a person. so this is how a basic database is constructed, will be a little bit more complicated w/ c's files cause we don't have an input that changes but all the parameters are just inside the code.

#####12/10/2015

* trying to fix issues w/ Makefile (especially I don't get why the path has to change, and why it is working if i call the previous existing launch.sh files, but not if i copy and paste their content into the Makefile itself?):
  * the bash script, that as more than one line as to be put in just one line, separeted w/ semicolons and eventually i can put \+return to write it in two lines, this because each command is run by make in a different shell
  * looks like the path in python script had to be changed cause the relative path is referred to the folder i'm running make into and not the folder where the py script is, so i changed ../../ w/ ../ and ../ w/ ./
  * i kept getting an error because the second script (clusterV.py) i wanted to run began running before the first script finished (even if i added output_data as his dependency) and couln't find the files. So now i changed the order in the make script, all is depending on plot and output_data (and not the opposite, i don't know if this is relevant, but btw). then i changed in the makefile the order of the target: the first one is now plot, that depends on output_data, so now it should start and wait until the other script finishes (i hope at least). If it will work, here below the congif.mk and Makefile:
    * config.mk (here the variables are defined, when want to use a variable, remember $() around it):
      ```makefile
      IM_SRC=./LNKMODEL/mprostest.py
      
      #SIM_EXE=bash ./LNKMODEL/launch.sh
      SIM_EXE=export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/tsl/software/testing/gsl/1.16/x86_64/bin/lib; \
      bsub -q TSL-Prod128 -We 1 "source python-2.7.4; python $(SIM_SRC)"
      
      PLOT_SRC=./clusterV.py
      
      #PLOT_EXE=bash launch_clusterV.sh
      PLOT_EXE=export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/tsl/software/testing/gsl/1.16/x86_64/bin/lib; \
      bsub -q TSL-Prod128 -We 1 "source python-2.7.4; python $(PLOT_SRC)"
      ```
    * Makefile (the bash part above are from C's launch scripts):
      ```makefile
      include config.mk
      
      DATA_FILES=$(wildcard ../*.dat)
      
      all : plot output_data
      
      .PHONY : plot
      plot : output_data $(PLOT_SRC)
              $(PLOT_EXE)
      #$(PLOT_EXE2)
      
      .PHONY : output_data
      output_data : $(SIM_SRC) $(DATA_FILES)
              $(SIM_EXE)
      #$(SIM_EXE2)
      
      .PHONY : clean
      clean :
              rm -f output_data
              rm -f plot
      ```

* update: the clean part doesn't work neither, in this case i supose it is because i have no filename as output_data or plot, btw need a new solution

#####13/10/2015

* SQL notes: SQL is not case sensitive; semicolon ate the end of each statement (this depends from the database system btw)

  > SELECT - extracts data from a database  
  > UPDATE - updates data in a database  
  > DELETE - deletes data from a database  
  > INSERT INTO - inserts new data into a database  
  > CREATE DATABASE - creates a new database  
  > ALTER DATABASE - modifies a database  
  > CREATE TABLE - creates a new table  
  > ALTER TABLE - modifies a table  
  > DROP TABLE - deletes a table  
  > CREATE INDEX - creates an index (search key)  
  > DROP INDEX - deletes an index  

  beware when using database on the internet cause the user input are transformed in sql commands potentially creating security issues!! especially one could write 'or 1=1' or, more strangely, 'or ""="' and for some reasons these always evaluate to True (this way one couldd see a whole database!). moreover, one could write a semicolon (that divides instructions) and then drop table, this would cause the table to be deleted from the database... very bad again.
  Here is an example to avoid it:

  > txtUserId = getRequestString("UserId");  
  > txtSQL = "SELECT * FROM Users WHERE UserId = @0";  
  > db.Execute(txtSQL,txtUserId);

  > Note that parameters are represented in the SQL statement by a @ marker. The SQL engine checks each parameter to ensure that it is correct for its column and are treated literally, and not as part of the SQL to be executed.

  about **BETWEEN**, its inclusive or exclusive behaviour depends on the database, so it must be checked before using it.
  most important syntax part i need to remember:

  > SELECT column_name(s)  
  > FROM table1  
  > JOIN table2  
  > ON table1.column_name=table2.column_name;

  NB. **JOIN** and **INNER JOIN** are just the same
  
  PS if for any reason i need to get back again to this, this is a very good tutorial: http://www.w3schools.com/sql/default.asp
  
  **NOT NULL** constraint: note that this works if i add rows like this: insert into table (name_column1, name_column2 etc.) values (value1, value2 etc), and i don't give any input for a given notnull column, if i give an empty string it just accept it!

* discussed w/ c again the new model, that needs to be parallelized. no new notes about it except for the fact that c is going to implement the part i talked about, ie the fact that too much connection between an effector gene and target could be deleterious because of immune system of the plant or even because it could damge the plant too much preventing a proper infeciton. this is going to be implmented as a treshold, over which the score (transcription) will increase, bu the fitness score will decrease.

#####14/10/2015

* I launched the make again (it didn't create figures), i did it the same way cause i want to check if it didn't because of some changes (yesterday i gave c acces to these files and they are now in a different color in the terminal)

* going on w/ the sql tutorial, registered into oracle mysql

* the c's code i launched on 6th it is stuck, doing **bpeek job_id** gave me the following for each time frequency:
  ```bash
  Traceback (most recent call last):
  File "/tsl/software/testing/python/2.7.4/x86_64/lib/python2.7/multiprocessing/process.py", line 258, in _bootstrap
    self.run()
  File "/tsl/software/testing/python/2.7.4/x86_64/lib/python2.7/multiprocessing/process.py", line 114, in run
    self._target(*self._args, **self._kwargs)
  File "/usr/users/TSL_20/minottoa/change_DT/DT15000/LNKMODEL/mprostest.py", line 91, in evolx
    trs=Lffit.trates(gen,MU)
  File "/usr/users/TSL_20/minottoa/change_DT/DT15000/LNKMODEL/Lffit.py", line 76, in trates
    Ws=1.0-((Wn/neff)/((Wn/neff)+(Wo)))
  ZeroDivisionError: float division by zero
  ```
  I'm trying to run again the DT5000 making it print out the Genome, cause it looks like we had all extinctions here? (have to ask carlos why the program didn't stop by itself it these are exctintions indeed)
  UPDATE: mailed c, they are extinctions indeed, on Fri we'll run another version that should have the right flag to avoid the code gets stuck during the simulations.

* about the fixation time for a new mutation in a population of size N, the most important paper is probably http://www.ncbi.nlm.nih.gov/pmc/articles/PMC1212239/pdf/763.pdf
  here Kimura gets to the cocnclusion that the fixation time is 4N generations, where N is the size population, BUT he's supposing NEUTRAL mutation and a DYPLOID population. I asked c and for our sample the assumption t~N should work fine. So the probability of a neutral mutation n to become fixed in a population on size N (fixed) is just 1/N.
  I wrote a simple script:
  ```python
  #simulation for fixation time of an allele in a population of fixed size N

import sys
import random
MOD=int(sys.argv[1])
if MOD==1 or MOD==0:
    pass
else:
    print 'write 0 to perform a simulation with each individual witha different allele'
    print 'write 1 to add a new mutation in a population with a fixed allele'
    exit()

def initialize_variable():
    global INIT_ALL
    if MOD==0:
        INIT_ALL=N #number of initial different alleles in the population
        d={}
        for j in range(N):
            d[j]=j
    else:
        INIT_ALL=2
        d={}
        for j in range(N):
            if j==0:
                d[j]=0
            else:
                d[j]=1
    T=0 #number of generations
    return T, d

N=500 #population size
TRIALS=10000 #number of trials
nt=0 #number of trials performed
average=0.0 #average fixation time of an allele
somma=0 #sum to calculate average number of generation
T=0 #number of generations
INIT_ALL=0 #number of alleles in pop, to be initialized
correction=0 #dont want to count trials where the allele dont get fixated in pop when calculating average

for x in range(TRIALS):
    iv=initialize_variable()
    T=iv[0]
    d=iv[1]
    #print str(d)+'*****'
    #print T
    print
    print "TRIAL # "+str(x)
    while True:
        print d
        dnew={} #this will be the new population
        for x in range(N):
            allele=d[random.choice(d.keys())]
            dnew[x]=allele
        del d
        d=dnew
        T+=1
        test=d[0]
        if all(alls==test for alls in d.values()):
            print d
            print
            if MOD==0:
                somma+=T
                print 'fixation time of allele '+str(test)+': '+str(T)
            else:
                if test==0:
                    somma+=T
                    print 'fixation time of allele: '+str(T)
                else:
                    correction-=1
                    print 'new allele no more present in the sample population'
            break

if TRIALS+correction==0:
    print 'the allele was never fixated in pop in these trials'
else:
    average=float(somma)/(TRIALS+correction)
    print
    print 'average number of generation for fixation of the allele: '+str(average)
print 'size of population '+str(N)
print 'initial number of alleles in population '+str(INIT_ALL)
if MOD==1:
    print 'fixation rate: '+str(float(TRIALS+correction)/TRIALS)
  ```
  to perform a simulation both of a population of fied size N with N different alleles and an omogeneous population of size N with a single new allele to have a fixation, respectively, for any allele or for the new allele. in the second case i calculate the rate of fixation and it looks like the previous formula it's a good approximation (rate of mutation/size of population). the formula was made with the hypotesis of fixed size N and non overlapping generations (this should be a good approximation of overlapping generations too, ad should work well w/ our seasonal pathogens). Moreover i'm calculating the average time of fixation and here i'm getting some results that are not great with the previous assumption of N~t. In this case it looks more like t~2N, and I found a couple of website/slides with this result for haploid organisms, but i can't find the original mathematical demonstration.
  This code was inspired by http://www.biology.arizona.edu/evolution/act/drift/frame.html, as it has the same logic.

#####15/10/2015

* killed the previous running codes, running the code again for the jumps in different time intervals, id DT5000, DT10000, DT15000 and DT20000, changing the seed to avoi extintions. c has the correct code and we'll run it tomorrow anyway.

* look trhough various evolution model for rates and time of fixation: the main models are the moran's for overlapping generations, and the wright-fisher model for non overlapping situation (my previous code). moran's is more accurate but more difficoult end expensive in a computer environment. w-f calculate the ratio as $P=(@N k)p^kq^(2N-k)$ where k is the number of copies of the allele p, for 1 copy as above. the two model are just the same for the ratio, but bcause of the different relative importance of stochastic fluctuation
  > In practice the Moran model and Wrigth-Fisher model give qualitatively similar results, but genetic drifts runs twice as fast in the Moran model.
  said this, T~2N, but for non overlapping population (talking haploid) T~N.

* meeting time: have to design a propr database for c's data, modify c's code so that i can have a file with all the input it's using (create a branch in github) -->this repository will be private because the code is not mine, create a repository w/ all my scripts (including the makefile).
  for now i'm considering two possible structures, they're basically the same just that one table could be a table with a very large number of columns, OR i could make 3/4 different tables (each for a kind of parameters, i.e. data files, mutation-hgt-duplication-deletion probabilities, size of genome and eff and tes, number of jumps-tie interval-seed). I would prefer the second option but i'd like a second opinion.
  these tables (or this table) will have a primary key, the ID, created with auto_increment. the ID would then be the foreign key for another table, with columns: ID, RUN#, n# (n changing when Qi is changing). in this case the primary key would be the union of the three columns.
  at this moment we are not changing any of the fors parameters except jumps,tn and seed, but if it has to be a database, one could decide to change the other parameters too. moreover there are kn, beta1, beta2 and i need to ask c what these are to decide if they should go in the database too.

* created new repository for my scripts and code, added wright and fisher model simulation. to remeber:
  * git init <name_of_directory>
  * git add <file_name>
  * git commit -m 'description of commit'
  * git push

#####16/10/2015

* deleted all previous results for DT changes cause i had the wrong code, more than getting stuck at extinctions it wasn't saving all the data we need. running the right c's code now, w/ the parameters above for DT an number of jumps. going trough the script to see if it's giving as an output everything i need to create a database. so pickle() is serializing the data when you do pickle.dump(), meaning you need to invert the process before getting the data (i'll check exactly what it is stored in the file btw). so now i'm going trouh c's clusterV.py code to see if is possible to simply add the data I want in the previously existing funcion (btw i'd like to talk to martin about this, cause it's possible there's a more functional way to store the data if i want to create a database from those). i would need Neff, NTE, Np, JUMPS, tn [id est DT], plus it would probably be fine to have the run # and the n# here and not just in the folders' architecture).
    * in pdt.py savedata() when pickle.dump() add at the end of the list everything i want (i will need to add these when i call the function from mprostest as well of course), this shouldn't create any problem with the plot code cause there are no for loops or len(A) anywhere. I'll do it after these 20 runs finish.
  launched the programs again because the version was wrong, i realized it wasn't doing the jumps, so i changed PAR=9, Qi+=1 and in the evolvx line 84 and 88 (if the pathogen is getting worst we don't consider it anymore)

* fixed the makefile (probably a problem with a tab?)

* to use programs in the cluster i need to source them, meaning **source name_and_version** (each time i log in the cluster), and then i can use it as usual. this way i cloned my git scripts repository and i should be able to put and pull stuff from there (and from other folders too)

#####19/10/2015

* read stuff about **pickle** and tried it. i should be able to get the data i want unpickling the output list. A[7] will be the list of probabiities (mutation, hgt, deletion, duplication), and A[8] will be the SEED. i will need to add the DT, number of jumps, run and n. i changed the code  of mprosest.py and pdt.py (here is the function to save the data), so that ~~A[11],A1[12] and A[13]~~ A[12], A[13] and A[14] are the DT the number of total jumps in the simulation and a list with [run_number, n_number,jump_number]. for this last list i justh use the already existing variable pth (string wi/ this format: '../RUN#/n#'), doing **stringa.strip(./).split(/)**; there are other options, the main would be re.split(r'\b\d+\b','stringa') to have a list of the numbers in the string, but in that case i should import the re library, so in this case my solution should be more simple. I tried to retrieve the data i need for a new run and it looks like it's working.

* **pysqlite3** is a library used to build a DB from Python (so I can directly access the data pickled in the output files); this library 
  > provides a disk-based db that allows accessing database using a nonstandard variant if SQL query language.
  another option would be the MySQLdb library, but it's not installed on this computer nor in the cluster yet, so sqlite3 should be easier 

* mysql is already in the cluster, but not on this computer. i'm downloading and installing it from the website to follow a tutorial to create a db from the very beginning. Installed mysql on this computer from dmg file. by default it is not running, so need to go in system preference, look up for mysql and start it.

#####20/10/2015

* modified c's clusterV code to have just one copy of the script in the main directory (need to change just the launch file when using it), added parser to give options from the command line, plus pickle an additional file CDATAV_par.p that saves the parameters given from the command line (including tha path to the directory). The line i modified are marked with **###***.
  btw still need to make it handle extinctions automathically

* used sqlite3 in python to create a tutorial database

* c's code for DT was running with Qi=1 (mutation rate), instead of 0.1. so I created a new folder named **changeDT_Qi** where Qi is correct and I'm running everything again. In the meanwhile i'll use the other duta to fix ClusterV.py

#####21/10/2015

* the modified code for clusterV.py worked and was hable to handle extinctions authomatically [i imported os library and added a step to verify if the folder architecture is empty **os.listdir()==[]**, in this case ignore it]. I created a Makefile and a config file (as below and as in script folder) to authomate the process over all the folders i need to plot.

```makefile
SRC=./clusterV.py

SRC_EXE_5000=export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/tsl/software/testing/gsl/1.16/x86_64/bin/lib; \
bsub -q TSL-Prod128 -We 1 "source python-2.7.4; python /usr/users/TSL_20/minottoa/change_DT_Qi/clusterV.py /usr/users/TSL_20/minottoa/change_DT_Qi/DT5000/ 20 40"

SRC_EXE_10000=export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/tsl/software/testing/gsl/1.16/x86_64/bin/lib; \
bsub -q TSL-Prod128 -We 1 "source python-2.7.4; python /usr/users/TSL_20/minottoa/change_DT_Qi/clusterV.py /usr/users/TSL_20/minottoa/change_DT_Qi/DT10000/ 20 20"

SRC_EXE_15000=export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/tsl/software/testing/gsl/1.16/x86_64/bin/lib; \
bsub -q TSL-Prod128 -We 1 "source python-2.7.4; python /usr/users/TSL_20/minottoa/change_DT_Qi/clusterV.py /usr/users/TSL_20/minottoa/change_DT_Qi/DT15000/ 20 13"

SRC_EXE_20000=export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/tsl/software/testing/gsl/1.16/x86_64/bin/lib; \
bsub -q TSL-Prod128 -We 1 "source python-2.7.4; python /usr/users/TSL_20/minottoa/change_DT_Qi/clusterV.py /usr/users/TSL_20/minottoa/change_DT_Qi/DT20000/ 20 10"

DATA_5000=./DT5000

DATA_10000=./DT10000

DATA_15000=./DT15000

DATA_20000=./DT20000
```

```makefile
include config.mk

all : o5000 o10000 o15000 o20000

.PHONY : o5000 o10000 o15000 o20000 clean

o5000 : $(SRC) $(DATA_5000)
        $(SRC_EXE_5000)

o10000 : $(SRC) $(DATA_10000)
        $(SRC_EXE_10000)

o15000 : $(SRC) $(DATA_15000)
        $(SRC_EXE_15000)

o20000 : $(SRC) $(DATA_20000)
        $(SRC_EXE_20000)

clean :
        rm ./DT5000/*.png
        rm ./DT5000/*.eps
        rm ./DT10000/*.png
        rm ./DT10000/*.eps
        rm ./DT15000/*.png
        rm ./DT15000/*.eps
        rm ./DT20000/*.png
        rm ./DT20000/*.eps
```

* fixed typo in last lines of clusterV.py that caused the code not to save CDATAVcomp and par.

* note i will need about sqlite3:
  > The AUTOINCREMENT keyword imposes extra CPU, memory, disk space, and disk I/O overhead and should be avoided if not strictly needed. It is usually not needed.
  >
  > In SQLite, a column with type INTEGER PRIMARY KEY is an alias for the ROWID (except in WITHOUT ROWID tables) which is always a 64-bit signed integer.
  >
  > On an INSERT, if the ROWID or INTEGER PRIMARY KEY column is not explicitly given a value, then it will be filled automatically with an unused integer, usually one more than the largest ROWID currently in use. This is true regardless of whether or not the AUTOINCREMENT keyword is used.
  > 
  > If the AUTOINCREMENT keyword appears after INTEGER PRIMARY KEY, that changes the automatic ROWID assignment algorithm to prevent the reuse of ROWIDs over the lifetime of the database. In other words, the purpose of AUTOINCREMENT is to prevent the reuse of ROWIDs from previously deleted rows.
 
  at this very moment iput autoincrement (mainly because i was using plain mysql syntax, btw i need to think better about this. at first sight it still looks to me like it would be a better idea to use it, giving i will have other tables linked via id, to prevent wrong connections).

####_work in progress/to do list_

* install pygsl locally (it's giving problems and i don't get way, it can't find numpy, but that's actually installed)
* parallel python, what's the main difference between multiprocessing and pp?
* see first point on 16/10/2015
* create database for c's data
* create a new repository w/ c's code and modify it in a branch to get all the inputs in an output file to be put in the database.
