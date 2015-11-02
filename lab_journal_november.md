##**Lab Journal**
####**_November_**
###**_Alice Minotto_**

#####2/11/2015
* going on reading matplotlib tutorials and documentations
  NOTES:
  * **import matplotlib.pyplot as plt**
  * if u provide a single array/list to plot plt will assume it's y values and generates x auto
  * the third parameter you can give indicates the type of line in the graph and its color (default **b-**, ie simple blue line). -- is a dotted line, o circles, s squares ^ triangles.
  * **plt.axis([xmin,xmax,ymin,ymax])**
  * you can plot multiples arrays of values w/ the following synthax **plt.plot(list1, list2,line, list3, list4, line2...)**
  * all current commands will aplly to the current axis/figure
  * to add a title to an ax (or a title to the plot) **t = plt.xlabel('my data', fontsize=14, color='red')**. u can also use math expressions surrounded by $. with an r in front of the expression tho avoid python interprete \ as escapes.
