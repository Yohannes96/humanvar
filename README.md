---
Title: Human populations' variation in rs1426654 SNP tutorial 
Author: Yohannes
Date March 1,2021


## 1. Variation in rs1426654 SNP among human populations
1.1. Importing the Allele Frequency Data, [this file] (freq.df)
```r
freq <- read.table('freq.df', header=T)>
```

1.2 Histograms
-For a better presentation of the data.
```r
hist(freq$Allele_A)>
```
<center>
<image src="Histogram.png" width=777px></img>
</center>

1.3 Scatterplots
-For a better comparison of the relationships between latitude and the frequency of allele A 
```r
plot(freq$Allele_A, freq$lat, xlab="f(A) rs1426654", ylab="Latitude", 
        pch=16, cex=0.8, col=myColors[freq$superpop], xlim=c(0, 1))

legend('topleft', c('African', 'Admixed American', 'East Asia', 'European', 'South Asian'), 
        cex=0.8, col=c('red','blue','darkgreen','salmon','black'), pch=16, inset=0.02)

title(main="Latitudinal Variation in f(A) at rs1426654 among 26 Human Populations", cex.main=1)
```

<center>
<image src="Scatterplot.png" width=777px></img>
</center>


##2. Plotting Data on Geographical Maps
This will help us to present both  geographical coordinates and the frequency data together in one plot

2.1 Packages installation and Loading
-Before drawing the geographical maps, we need to install the following packages and load them.
```r
library(maps)

library(mapdata)

library(scales)

library(mapplots) 
```

2.2 World Map drawing

```r
map('worldHires', xlim=c(-120,142), ylim=c(-12,72), col='gray', fill=FALSE)

box()
```
<center>
<image src="World map.png" width=777px></img>
</center>
2.3 Plotting the 26 human populations on the world map

```r
map('worldHires', xlim=c(-120,142), ylim=c(-12,72), col='gray', fill=FALSE)

points(freq$long, freq$lat, pch=16, col="salmon")

box()
```
<center>
<image src="Plot of 26 human populations.png" width=777px></img>
</center>

2.4 Drawing a Pie Charts to Display Relative Allele Frequency
This will show the relative frequencies of both alleles at a given geographical position (i.e. population).
``r
map('worldHires', xlim=c(-120,142), ylim=c(-12,72), col='gray', fill=FALSE)

add.pie(z=c(0.104, 0.895), x=-59.5412, y=13.1776, radius=192/100, 
            col=c(alpha("orange", 0.6), alpha("blue", 0.6)), labels="")

box()
```
<center>
<image src="A Pie Chart showing Relative Allele Frequency.png" width=777px></img>
</center>

2.5 Ploting all Pie Charts Using for{} Loop
In order to plot all pie chart for the respective population of data, we will use for{} Loop

```r
map('worldHires', xlim=c(-120,142), ylim=c(-15,72), col='gray', fill=FALSE)


for (i in 1:26){add.pie(z=c(freq$Allele_A[i], freq$Allele_G[i]), x=freq$long[i], y=freq$lat[i], 
        radius=freq$N_CHR[i]/100, col=c(alpha("orange", 0.6), alpha("blue", 0.6)), labels="")
  i=i+1
}

box()
```

<center>
<image src="Plot for all Pie Charts.png" width=777px></img>
</center>

2.6 Labeling and legends for the final pie chart

```r
map('worldHires', xlim=c(-120,142), ylim=c(-15,72), col='gray', fill=FALSE)


for (i in 1:26){
  add.pie(z=c(freq$Allele_A[i], freq$Allele_G[i]), x=freq$long[i], y=freq$lat[i], 
        radius=freq$N_CHR[i]/100, col=c(alpha("orange", 0.6), alpha("blue", 0.6)), labels="")
  i=i+1
}

text(freq$long, freq$lat, labels=freq$superpop, cex=0.5, pos=1)

box()

legend('topright', bty='1', c("Freq. Allele A", "Freq. Allele G"), 
        pch=16, col=c(alpha("orange", 0.6), alpha("blue", 0.6)), pt.cex=1, cex=0.7)

title(main="Global Distribution of rs1426654 Alleles", font.main=1, cex.main=0.9)
```
<center>
<image src="Final pie chart with labels.png" width=777px></img>
</center>
