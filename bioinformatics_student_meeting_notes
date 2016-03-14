BASH:
awk '{if($4=="blabla")print$0}'
$0 is the whole line
$1, $2, $3... are the columns of the file
bioawk to process bam/sam file

for a website to be indexed by google you can register to google analytics and copy paste their code at the end of the html document.

***

```bash
#SBATCH requirement (-mem -t)

srun bablabla.sh
sacct --long
``` 
to check jobs in the SLURM

<code>sattach [jobid]</code>
instead of <code>bpeek</code>

***

ln -s [location of file]
create a link

***

###R

An useful tool to use R is RStudio (can be easily downloaed fron the internet).
Here there are 4 spaces t work, a terminal, the text editor for the script, a spece to upload data and a spece to visualize the plots that are generated.
to run automatically a command written in the text editor press ctrl+Enter.
to visualize the plot you have to write <code>plot</code> in the terminal command line.

To use a column in the dataset you can use <code>$<code> like this:
```R
data$name_of_column
```

```R
data[data$col_name == 0]$col_to_see
```
this last command will visualize the column <code>col_to_see</code> if the value stored in <code>col_name</code> is equal to <code>0</code>.

R can also be used to save data like:
```R
write.table(data,path)
```
or 
```R
write.csv(data,path)
```

Also to change the theme of a plot you don't need to actually regenerate the whole plot, but you can use:
```R
plot+theme_bw()
```
this example would get rid of the grey background. You can use this same synthax for everything.
```R
plot+labs(x=...,y=...)
```to change the axis labels.
```R
plot+xlim(...,...)
```
to set the x axis limits (or ylim for the y axis).
```R
palette <- brewer.pd(#,"name")
```
to save a colormap with # colors.

***
