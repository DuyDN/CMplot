CMplot [![](https://img.shields.io/badge/Issues-50%2B-brightgreen.svg)](https://github.com/YinLiLin/R-CMplot/issues) [![](https://img.shields.io/badge/Release-v3.4.0-red.svg)](https://cran.r-project.org/web/packages/CMplot/)
=========

## A high-quality drawing tool designed for Manhattan plot of genomic analysis

### Installation

**CMplot** is available on CRAN, so it can be installed with the following R code:

```r
> install.packages("CMplot")
> library("CMplot")
#(optional)if you want to use the latest version:
#source("https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/R/CMplot.r")
```

---

There are two example datasets attached in **CMplot**, users can export and view the details by following R code:

```r
> data(pig60K)   #calculated p-values by MLM
> data(cattle50K)   #calculated SNP effects by rrblup
> head(pig60K)

          SNP Chromosome Position    trait1     trait2     trait3
1 ALGA0000009          1    52297 0.7738187 0.51194318 0.51194318
2 ALGA0000014          1    79763 0.7738187 0.51194318 0.51194318
3 ALGA0000021          1   209568 0.7583016 0.98405289 0.98405289
4 ALGA0000022          1   292758 0.7200305 0.48887140 0.48887140
5 ALGA0000046          1   747831 0.9736840 0.22096836 0.22096836
6 ALGA0000047          1   761957 0.9174565 0.05753712 0.05753712

> head(cattle50K)

   SNP chr    pos Somatic cell score  Milk yield Fat percentage
1 SNP1   1  59082        0.000244361 0.000484255    0.001379210
2 SNP2   1 118164        0.000532272 0.000039800    0.000598951
3 SNP3   1 177246        0.001633058 0.000311645    0.000279427
4 SNP4   1 236328        0.001412865 0.000909370    0.001040161
5 SNP5   1 295410        0.000090700 0.002202973    0.000351394
6 SNP6   1 354493        0.000110681 0.000342628    0.000105792

```
As the example datasets, the first three columns are names, chromosome, position of SNPs respectively, the res of columns are the pvalues of GWAS or effects of GS/GP for traits,  the number of traits is unlimited.
Note: if plotting SNP_Density, only the first three columns are needed.

Now **CMplot** could handle not only Genome-wide association study results, but also SNP effects, Fst, tajima's D and so on.

---

Total 40 parameters are available in **CMplot**, typing ```?CMplot``` can get the detail function of all parameters.

---
### Citation
**waiting for updating...**<br>

---
### SNP-density plot

```r
> CMplot(pig60K,plot.type="d",bin.size=1e6,col=c("darkgreen", "yellow", "red"),file="jpg",memo="",dpi=300,
    file.output=TRUE, verbose=TRUE)
# users can personally set the windowsize and the max of legend by:
# bin.size=1e6
# bin.max=N
# memo: add a character to the output file name.
```

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/illumilla_60K.jpg">
<img src="Figure/illumilla_60K.jpg" height="460px" width="680px">
</a>
</p>

---

### Circular-Manhattan plot

#### (1) Genome-wide association study(GWAS)

```r
> CMplot(pig60K,plot.type="c",chr.labels=paste("Chr",c(1:18,"X"),sep=""),r=0.4,cir.legend=TRUE,
        outward=FALSE,cir.legend.col="black",cir.chr.h=1.3,chr.den.col="black",file="jpg",
        memo="",dpi=300,file.output=TRUE,verbose=TRUE)
```

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/9.jpg">
<img src="Figure/9.jpg" height="400px" width="400px">
</a>
</p>

```r
> CMplot(pig60K,plot.type="c",r=0.4,col=c("grey30","grey60"),chr.labels=paste("Chr",c(1:18,"X"),sep=""),
      threshold=c(1e-6,1e-4),cir.chr.h=1.5,amplify=TRUE,threshold.lty=c(1,2),threshold.col=c("red",
      "blue"),signal.line=1,signal.col=c("red","green"),chr.den.col=c("darkgreen","yellow","red"),
      bin.size=1e6,outward=FALSE,file="jpg",memo="",dpi=300,file.output=TRUE,verbose=TRUE)

#Note:
1. if signal.line=NULL, the lines that crosse circles won't be added.
2. if the length of parameter 'chr.den.col' is not equal to 1, SNP density that counts 
   the number of SNP within given size('bin.size') will be plotted around the circle.
```

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/10.jpg">
<img src="Figure/10.jpg" height="400px" width="453px">
</a>
</p>


#### (2) Genomic Selection/Prediction(GS/GP)

```r
> CMplot(cattle50K,plot.type="c",LOG10=FALSE,outward=TRUE,col=matrix(c("#4DAF4A",NA,NA,"dodgerblue4",
         "deepskyblue",NA,"dodgerblue1", "olivedrab3", "darkgoldenrod1"), nrow=3, byrow=TRUE),
         chr.labels=paste("Chr",c(1:29),sep=""),threshold=NULL,r=1.2,cir.chr.h=1.5,cir.legend.cex=0.5,
         cir.band=1,file="jpg", memo="",dpi=300,chr.den.col="black",file.output=TRUE,verbose=TRUE)
        
#Note: 
Parameter 'col' can be either vector or matrix, if a matrix, each trait can be plotted in different colors.
```

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/11.jpg">
<img src="Figure/11.jpg" height="400px" width="400px">
</a>
</p>

---

### Single_track Rectangular-Manhattan plot

#### (1) Genome-wide association study(GWAS)

```r
> CMplot(pig60K,plot.type="m",LOG10=TRUE,threshold=NULL,chr.den.col=NULL,file="jpg",memo="",dpi=300,
    ,file.output=TRUE,verbose=TRUE)
```

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/1.jpg">
<img src="Figure/1.jpg" height="300px" width="900px">
</a>
</p>

```r
> CMplot(pig60K, plot.type="m", col=c("grey30","grey60"), LOG10=TRUE, ylim=c(2,12), threshold=c(1e-6,1e-4),
        threshold.lty=c(1,2), threshold.lwd=c(1,1), threshold.col=c("black","grey"), amplify=TRUE,
        chr.den.col=NULL, signal.col=c("red","green"), signal.cex=c(1,1),signal.pch=c(19,19),
        file="jpg",memo="",dpi=300,file.output=TRUE,verbose=TRUE)

#Note:
if the ylim is setted, then CMplot will only plot the ponits which among this interval.
```

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/2.jpg">
<img src="Figure/2.jpg" height="330px" width="900px">
</a>
</p>

```r
> CMplot(pig60K, plot.type="m", LOG10=TRUE, ylim=NULL, threshold=c(1e-6,1e-4),threshold.lty=c(1,2),
        threshold.lwd=c(1,1), threshold.col=c("black","grey"), amplify=TRUE,bin.size=1e6,
        chr.den.col=c("darkgreen", "yellow", "red"),signal.col=c("red","green"),signal.cex=c(1,1),
        signal.pch=c(19,19),file="jpg",memo="",dpi=300,file.output=TRUE,verbose=TRUE)
        
#Note:
if the length of parameter 'chr.den.col' is bigger than 1, SNP density that counts 
   the number of SNP within given size('bin.size') will be plotted.
```

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/2_2.jpg">
<img src="Figure/2_2.jpg" height="330px" width="900px">
</a>
</p>

#### (2) Genomic Selection/Prediction(GS/GP)

```r
> CMplot(cattle50K, plot.type="m", band=0.5, LOG10=FALSE, ylab="SNP effect",threshold=c(-0.015, 0.015),
        threshold.lty=2, threshold.lwd=1, threshold.col="red", amplify=FALSE,
        chr.den.col=NULL, file="jpg",memo="",dpi=300,file.output=TRUE,verbose=TRUE,cex=0.8)

#Note: 
if signal.col=NULL, the significant SNPs will be plotted with original colors.
```

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/3.jpg">
<img src="Figure/3.jpg" height="300px" width="900px">
</a>
</p>

```r
> cattle50K[,4:ncol(cattle50K)] <- apply(cattle50K[,4:ncol(cattle50K)], 2, 
         function(x) x*sample(c(1,-1), length(x), rep=TRUE))
> CMplot(cattle50K, plot.type="m", band=0, LOG10=FALSE, ylab="Abs(SNP effect)",threshold=0.015,
        threshold.lty=2, threshold.lwd=1, threshold.col="red", amplify=TRUE, signal.col=NULL,
        chr.den.col=NULL, file="jpg",memo="",dpi=300,file.output=TRUE,verbose=TRUE)

#Note: Positive and negative values are acceptable.
```

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/PN.jpg">
<img src="Figure/PN.jpg" height="300px" width="900px">
</a>
</p>

### Multi_tracks Rectangular-Manhattan plot

```r
> CMplot(pig60K, plot.type="m", multracks=TRUE, threshold=c(1e-6,1e-4),threshold.lty=c(1,2), 
        threshold.lwd=c(1,1), threshold.col=c("black","grey"), amplify=TRUE,bin.size=1e6,
        chr.den.col=c("darkgreen", "yellow", "red"), signal.col=c("red","green"),signal.cex=c(1,1),
        file="jpg",memo="",dpi=300,file.output=TRUE,verbose=TRUE)
```

#### a. all traits in a axes:

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/4.jpg">
<img src="Figure/5.jpg" height="330px" width="900px">
</a>
</p>

#### b. all traits in separated axes:

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/5.jpg">
<img src="Figure/4.jpg" height="900px" width="840px">
</a>
</p>

---

### Single_track Q-Q plot

```r
> CMplot(pig60K,plot.type="q",conf.int.col=NULL,box=TRUE,file="jpg",memo="",dpi=300,
    ,file.output=TRUE,verbose=TRUE)
```

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/6.jpg">
<img src="Figure/6.jpg" height="450px" width="450px">
</a>
</p>

### Multi_tracks Q-Q plot

```r
> CMplot(pig60K,plot.type="q",col=c("dodgerblue1", "olivedrab3", "darkgoldenrod1"),threshold=1e6,
        signal.pch=19,signal.cex=1.5,signal.col="red",conf.int.col="grey",box=FALSE,multracks=
        TRUE,file="jpg",memo="",dpi=300,file.output=TRUE,verbose=TRUE)
```

#### a. all traits in a axes:

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/8.jpg">
<img src="Figure/8.jpg" height="450px" width="450px">
</a>
</p>

#### b. all traits in separated axes:

<p align="center">
<a href="https://raw.githubusercontent.com/YinLiLin/R-CMplot/master/Figure/7.jpg">
<img src="Figure/7.jpg" height="450px" width="680px">
</a>
</p>

---

### Parameters of CMplot
```r
Pmap: a dataframe, at least four columns. The first column is the name of SNP, the second column is the chromosome of SNP, the third column is the position of SNP, and the remaining columns are the P-value of each trait(Note:each trait a column).

col: a vector or a matrix, if "col" equals to a vector, each circle use the same colors, it means that the same chromosome is drewed in the same color, the colors are not fixed, one, two, three or more colors can be used, if the length of the "col" is shorter than the length the chromosome, then colors will be applied circularly. 
  if "col" equals to a matrix, the row is the number of circles(traits), the columns are the colors that users want to use for different circles, so each circle can be plotted in different number of colors, the missing value can be replaced by NA. For example: 
  col=matrix(c("grey30","grey60",NA,"red","blue","green","orange",NA,NA),3,3,byrow=T).

bin.size: the size of bin for SNP_density plot.

bin.max: the max value of legend of SNP_density plot, the bin whose SNP number is bigger than 'bin.max' will be use the same color.

pch: a number, the type for the points, is the same with "pch" in <plot>.

band: a number, the space between chromosomes, the default is 1(if the band equals to 0, then there would be no space between chromosome).

cir.band: a number, the space between circles, the default is 1.

H: a number, the height for each circle, each circle represents a trait, the default is 1.

ylim: a vector, the range of Y-axis when plotting the two type of Manhattans, is the same with "ylim" in <plot>.

cex.axis: a number, controls the size of numbers of X-axis and the size of labels of circle plot.

plot.type: a character or vector, only "d", "c", "m", "q" or "b" can be used. if plot.type="d", SNP density will be plotted; if plot.type="c", only circle-Manhattan plot will be plotted; if plot.type="m",only Manhattan plot will be plotted; if plot.type="q",only Q-Q plot will be plotted;if plot.type="b", both circle-Manhattan, Manhattan and Q-Q plots will be plotted; if plot.type=c("m","q"), Both Manhattan and Q-Q plots will be plotted.

multracks: a logical,if multracks=FALSE, plotting multiple traits on multiple tracks, if it is TRUE, all Manhattan plots will be plotted in only one track.

cex: a number or a vector, the size for the points, is the same with "size" in <plot>, and if it is a vector, the first number controls the size of points in circle plot(the default is 0.5), the second number controls the size of points in Manhattan plot(the default is 1), the third number controls the size of points in Q-Q plot(the default is 1)

r: a number, the radius for the circle(the inside radius), the default is 1.

xlab: a character, the labels for x axis.

ylab: a character, the labels for y axis.

xaxs: a character, The style of axis interval calculation to be used for the x-axis. Possible values are "r", "i", "e", "s", "d". The styles are generally controlled by the range of data or xlim, if given.

yaxs: a character, The style of axis interval calculation to be used for the y-axis. See xaxs above..

outward: logical, if outward=TRUE,then all points will be plotted from inside to outside.

threshold: a number or vector, the significant threshold. For example, Bonfferoni adjustment method: threshold=0.01/nrow(Pmap). More than one significant line can be added on the plots, if threshold=0 or NULL, then the threshold line will not be added.

threshold.col: a character or vector, the colour for the line of threshold levels.

threshold.lwd: a number or vector, the width for the line of threshold levels.

threshold.lty: a number or vector, the type for the line of threshold levels.

amplify: logical, CMplot can amplify the significant points, if amplify=T, then the points greater than the minimal significant level will be highlighted, the default: amplify=TRUE.

chr.labels: a vector, the labels for the chromosomes of circle-Manhattan plot.

signal.cex: a number, if amplify=TRUE, users can set the size of significant points.

signal.pch: a number, if amplify=TRUE, users can set the shape of significant points.

signal.col: a character, if amplify=TRUE, users can set the colour of significant points, if signal.col=NULL, then the colors of significant points will not be changed.

signal.line: a number, the width of the lines cross the circle

cir.chr: logical, a boundary represents chromosome, the default is TRUE.

cir.chr.h: a number, the width for the boundary, if cir.chr=FALSE, then this parameter will be useless.

chr.den.col: a character or vector or NULL, the colour for the SNP density. If the length of parameter 'chr.den.col' is bigger than 1, SNP density that counts 
   the number of SNP within given size('bin.size') will be plotted around the circle. If chr.den.col=NULL, then the default colours are the same with the parameter "col" for circle.

cir.legend: logical, whether to add the legend of each circle.

cir.legend.cex: a number, the size of the number of legend.

cir.legend.col: a character, the color of the axis of legend.

LOG10: logical, whether to change the p-value into log10(p-value).

box: logical, this function draws a box around the current Manhattan plot.

conf.int.col: a character, the color of the confidence interval on QQ-plot.

file.output: a logical, users can choose whether to output the plot results.

file: a character, users can choose the different output formats of plot, so for, "jpg", "pdf", "tiff" can be selected by users.

dpi: a number, the picture element for .jpg and .tiff files. The default is 300.

memo: add a character to the output file name.

verbose: whether print the reminder.

```

---

### Contact
Questions, suggestions, and bug reports are welcome and appreciated.
- **Author:** Lilin Yin
- **Contact:** ylilin@163.com
- **QQ group:** 166305848
- **Institution:** [*Huazhong agricultural university*](http://www.hzau.edu.cn/2014/ch/)
