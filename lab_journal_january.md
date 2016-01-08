##**Lab Journal**
####**_January_**
###**_Alice Minotto_**

#####7/1/2016

* took a look at <code>functools</code>. nothing i can use at the moment.  
* read:
  > Subset selection of high-depth next generation sequencing reads for de novo genome assembly using MapReduce framework
  at http://www.ncbi.nlm.nih.gov/pmc/articles/PMC4682372/
  notes: not enough infor on the trimming alg and results (there's the name of the program used by the way), i think this could make a big change in the results of using a subset of data or not, especially cause i don't think i have ever kept in my trimming program read with such a low minimum quality score as described in the article. the other thing is that for large genomes they are using allpaths, and so not just paired end reads, but also mate pair. looks like they are just making the subset selection on the paired reads, so i'd like to know the effect using velvet, for example, and just pe.

* TO DO LIST:
  * comment the style for all the plots, to eliminate background colors.
  * ~~for the first plot in the **new** folder, fix the layout of the scale for both axis to make it consistent with other figures.~~
  * save all the plot with high definition adding these lines when saving:
    ```python
    fig.patch.set_alpha(0.5)
    plot.savefig(namefig,dpi=100,bbox_inches='tight')
    plot.savefig(namefig+'.svg',bbox_inches='tight')
    ```
  * for all the last plots with the comparisons between all the simulations do the same and set max values for the x axis as in carlos' mail
  * remove 'Eff' from title
  * for the TE plots decrease the bin number so that the figures are less messy
  * eliminate legend from 4.7 to 4.10

  * all done on <code>comparison_plot.py</code> and <code>comparison_plot_derivatives.py</code> and launched.

#####8/1/2016

* moved **CDATAV.p** from **old_images** to main **new** folder to get images again with yesterday changes.

* re launched last two because i forgot to change the launch files and i moved tthe scripts to **scripts** repository.
