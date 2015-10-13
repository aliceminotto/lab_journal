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
    txtSQL = "SELECT * FROM Users WHERE UserId = @0";
    db.Execute(txtSQL,txtUserId);

  > Note that parameters are represented in the SQL statement by a @ marker. The SQL engine checks each parameter to ensure that it is correct for its column and are treated literally, and not as part of the SQL to be executed.

  about **BETWEEN**, its inclusive or exclusive behaviour depends on the database, so it must be checked before using it.
  most important syntax part i need to remember:

  > SELECT column_name(s)
  > FROM table1
  > JOIN table2
  > ON table1.column_name=table2.column_name;

  NB. **JOIN** and **INNER JOIN** are just the same

* discussed w/ c again the new model, that needs to be parallelized. no new notes about it except for the fact that c is going to implement the part i talked about, ie the fact that too much connection between an effector gene and target could be deleterious because of immune system of the plant or even because it could damge the plant too much preventing a proper infeciton. this is going to be implmented as a treshold, over which the score (transcription) will increase, bu the fitness score will decrease.

####_work in progress/to do list_

* install pygsl locally (it's giving problems and i don't get way, it can't find numpy, but that's actually installed)
* parallel python, what's the main difference between multiprocessing and pp?
