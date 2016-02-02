####**_Mathematical modelling of life and death decision during cellular stress_**  
#####_Dr. Orsolya Kapuy_  
#####23/10/2015

Cell can underg both programmed and unprogrammed death (necrosis). There are two kind of programmed cell death: apoptosis and autophagy. This last one can actually be considered a way of surviaval, given that the cell eats the damaged components, and this behaviour can be able to save its life. Autophagy is especially seen during starvation.  
RE is very important in homeostasis, having a crucial role in protein synthesis and metabolic processes. If the cell is stressed and the RE is stresse, the Unfolded Protein Response (UPR) is activated. UPR has the role to choose between autophagy and apoptosis. The pathways involved in this choosing are multiples and complex, so they are trying to 'reduce the system' trough mathematical methods and molecular biology experiments. (they are working on different strains of human cell lines and they detect their viability).
They have to collect all the possible connections involved in the network for apoptosis and authophagy known by literature and experiment. Then they have to write down the dinamic of the system, meaning:
* a protein can be active or unactive
* synthesis and degradation of a protein
Both these processes are or can be mediated by other proteins.
Then they have to introduce **reaction kinetics equations**, where there will be constants multiplying each of the possible processes, positive numbers for activation and synthesis, and negative numbers for inactivation and degradation.
At this point you will have differential equations that can be solved in a computer simulation by imp-lementing time course (Protein/time). This will result in a qualitative study of the regulatory network.
OR you could do a (phase plain analysis?) by studying two crucial different equations (we'll see it later).
OR you could plot biforcation diagrams (protein/k).

There are different ways proteins can interact with each others: the most simple are simple activation (protein A activates protein B), or simple inactivation (protein A inactivate protein B).
Moreover, we can have **positive feedback loop** or **double negative feedback loop**. Let's think about a positive feedback loop: (Protein/signal) the signal (protein A) increases, at a certain point it will reach a treshold level and it will activate protein B, so there will be a sudden jump in the level of the protein cause now B is active and will speed up the process. On the reverse if signal decrease there will be a lower treshold of B where A itself will decrease. (will add an image here) From the graph we can see that there are two separated phases, so we have a **_molecular switch_**.
Last, we can have a negative loop where A activates B, B activates C and C inhibits A.

_When developing a model, keep in mind that the model has to be simple to be functional._

Two of the main know activators of apoptosis and autophagy are caspase3 and beclin1 respectively. Interestingly, both are inhibited by antibcl2, that we will call from now on a **crosstalk element**.

What it is seen in experiment (checking for caspase3 and beclin1 levels) is that just after a ER stress autophagy is activated, and after a while autophagy stops and apoptosis is activated (namely 10h). This could show a role of apoptosis in inactivating autophagy.
It is known that beclin1 can be cleaved by caspases. But the inactive form of beclin1 is able to help apoptosis. Here we have a positive feedback between the two processes.

One of utophagy inducer can inhibite apoptosis inducer. At the same time the apoptosis inducer inhibites the crosstalk element in a **double negative feedback**.
Making a graph (Apoptosis_inducer/Autophagy_inducer) (add image here), where we can say where eahc point will go, we can see that there are two stable points, one at autophagy and the other at apoptosis, plus an ustable steady state where the curves of the two inducers meet. (the reason for not considering the inactive form of the autophagy inducer is for model's semplicity's sake and because they are hypotesing that the two forms are already at equilibrium). The unstable state is like the max high point between two valleys: IRL it never really happens that the system stays here because there are always stimula towards the cell.

If we increase stress both the curves move to right, but the apoptosis curve moves much faster, so at a certain point we end up with the only stable state at apoptosis (basically the second valley disappear).
There'a double negative feedback between autophagy inducer and apoptosis inducer too.
The result of all these considerations is a deteministic model (add image here of the two curves for different stress level).
**BUT** in a population analysis of course we have to consider stochastic processes as well (because not all the cells perceive the same level of stress at the very same moment). So adding stochastic process on a single cell the graph will stay more or less the same (but the curve won't be that smooth, it will be zzzz). Instead, if we watch at the population level (add image here) at high stress level we can see that the apoptosis response doesn't look anymore like a swithc, but seems to increase gradually. And this is what actually can be seen in a wet lab experiment.

Another experiment was to wash out the stress factor after 30' or 60'. This way they were able to determine that at 30' the apoptotic response is reversible, while ti is no more at 60' (nad this makes biological sense if you think about it), so basically the second jumps in the curve doesn't exist (add image here).

***

####**seeing the future - a demo of light speed optical sequence alignment**
#####_5/11/2015_

the new technology is not yet available, but the idea (and the prototypes), is to use ligth to speed up very much the process of alignment (it can actually have many other applications, not crystal clear to the very developpers). The tech. uses crystal liquid to transmit informations and the pixel light is detected by a camera. This way you will be able ideally to permorm hexabytes of calculation on a desk (the device should be connected to a desk computer).
the program will be mainly open source but will require an effort from the community to dvelop them (problems here: how much time? will the results of these new 'alghorithms?' be comparable to the old ones?).
there are not yet precise information about the accuracy of the system (they expect to have the same accuracy as common blast), and the result are not discrete cause they are detecting ligth intensity, but continuous, this way enabling researchers to detect similarities between aa or bases too.
problems here: what about the ligth biases? don't they expect the same problems as Illumina? (but consider we are summing these problems to the previous ones, would they be avoidable running the same experiment multiple times?)

***

####**_G-Quadruplex: the DNA quadruplex helix_**
#####_Shankar Balasubramanian_
#####17/11/2015

The prof thinks that the double helix is the status of DNA when is "resting", not doing anything special. It was seen by difrraction analysis that there is this other possible structure, the G-tetra, that happens in G rich regions. In this case four G bases (on a ssDNA) are coordinated with other two Gs of the group and a central monovalent cation, that provides electron density to the structure (K^+ > NH_4 ^+ > Na^+ > Li^+). Potassium appears to be the best cation (more stable structure) because of its radius, notice it is also the most abundant in the cell environment.
A ssDNA that is G rich is tought to self assemble in particoular structures:
(put image here)
(it can actually be organized in other kind of structures too, as we'll say later).
It was suggested an interaction of this kind of structure with telomerase enzyme. 
An algorithm was implemented to detect PQS (Predicted Quadruplex Sequence) by the sequence, it appears to have almost 90% success rate. PQS are very very stable and, theoretically, they are found (>300000) in promoters, first introns (it looks like they are especially present in upstream elements), transcription end site, gene bodies, repetitive elements (so it looks like they distributin in the genome is not randomic).
A class of small molecules was synthetized that bind these $G structures stabilizing them and wiothout intercalating in the double helix.
Moreover an antibody against this structer has been designed so that it can be visialized in the cell. Using this antibody it was also possible to study the dynamics of these structures during the cell cycle: the cells were syncronized, at a pattern was seen about thi structures' detection, in particoular they are more visible during the S phase.
If the strustures are then stabilized with the molecules I talked about above (the main one being PDS) it can be seen that the visualization of G4 is possible in all the phases just like in the S phase.

A co-staining w/ the telomerase was tried but most of G4 do not colocalize with it, as already predicted with the algorithm.

Another essay was done using the antibody on naked DNA (not in cell and not organized as chromatin): the DNA was sonicated and the fragments are then immunoprecipitated. This way it is possible to find the DNA fragments that are enriched in quadruplex helix. The library was then sequenced.
This was very good cause the peaks identified with the pulldown essay well correlated with what was predicted by the algorithm.

PDS (=pyrodostatin) is the molecule that stabilize G4 they are more focusing on. there are some small evidence that this molecule caould be able to inhibit cell growth.
gammaH2AX is a classic staining for a phosforilation of the H2 histon involved in the damage response, it was seen a lot of its signal with PDS (BUT it requires translation or transcription). Their hipotesis is that the cell cycle blockage increases the probability of a dsbreak in the position the G4 are.

Thay also looked at the transcription levels of a lot of oncogenes and they found out that especially SRC is silenced by PDS.

Wound heling essay in SRC overexpressing cells (very metastatic ones): it was seen that the cellular motibility is strongly inhibited by PDS (more than with doxorubicin), because PDS inhibits SRC (here i'm supposing it was already found a linkage between cellular motility and SRC expression).

It looks like exists at least one helicasis to unwind the G4 structures (hPif1 in many cases colocalize with PDS).

**G4-seq** technique

they got Illumina reads that are sequenced w/ the usual quality control tool. Then they just keep the ssDNA (they throw away the new one generated by Illumina).
In a second time they to the same again, but with K<sup>+</sup> to see if they get quadruplex.
In this case, if you look at the Quality score plot (they had to change the pipeline so that the data were not thrown away as it would happen by default) you can see that there is a huge decreasing of the Q where there is a quadruplex, and the Q score never recovers from that.

**!!!!!!!!!!I think this is very very very very important/interesting given both the seq bias of Illumina, the thresholds used by Illumina itself and the quality trimming program used now!!!!!!!!!!!!!!!**

Using the ligand they were able to find even more quadruplex (and one of them is **_myc_**).
G4 seq revealed a lot of non canonical G4 structures (like long loops, bulges and multiple bulges), and these were not predicted by the algorithms because it would be very difficoult and prone to finding a lot of false positive probably.

They found that the highest density of quadruplex occurs in genes commonly amplified in cancer (again, one is myc). The high increase in the visibility of this strusture in cancer cells was also seen comparing same individual, same tissue, healty cells vs cancer cells.

Another essay: they used a primary cell line often used as a cancer model as the cells quickly become transformed _in vitro_ for chromatin immunoprecipitation (the previous essay was interesting, but as we know DNA is always bound in proteins so this is more significant biologically speaking). Thay fragmented DNA, bound it to the antibody for the G4 structurea and then sequence (**G4 chip**).
Combining this essay with ither techniques they were able to see that these structures (the peaks) are in open chromatin regions.
If the status of chromatin is changed, so changes the position of the peaks.
When the chromatin is open both in the normal cells and in the precancar cells the quadruplex is just (or mainly) present in the precancer cells (they can't explain these results today).

Synthetic Lethality: it looks like BRCA-/- cells are more sensitive to PDSI (the small molecule i was talking about). Moreover if DDR+ is somministrated (it inhibits the double strand break response) cells become more sensitive to PDSI.

(note: some link with A loop? they are going to have more research about it)

***

####**_The BioJS Workshop and Hackathon_**
#####3 and 4/12/2015

The use of nodejs allows to use javascript both on the web browser (usual use) AND on the server side like it was another programming language. Installed nmp to install components by command line and u need to have git.
Cloned an hand on repository on the desktop so we can make a mess with it.
d3 is used to create svg images.

***

####_Galaxy Training_
#####2/2/2016

used both by experimental biologist and bioinfromaticians.
it is possible to import datasets (there should't be a limit here), as well as tools. history (keep track of tools and dataset used) can also be shared with other users.
It is possible to create a workflow pretty easily, and galaxy is able to tell if an output is actually ok to be used as input for the next step.
