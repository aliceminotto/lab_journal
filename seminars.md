####_Mathematical modelling of life and death decision during cellular stress_
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
Moreover, we can have **positive feedback loop** or **double negative feedback loop**.
