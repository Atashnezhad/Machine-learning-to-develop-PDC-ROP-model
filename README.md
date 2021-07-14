# Developing PDC ROP model using Artificial Intelligence

A PDC ROP model was developed using symbolic regression algorithm. 

* In this study, we use the Sandia National Lab and National Oil Varco full PDC bit data.
* The data was published in ARMA conference 55TH US ROCK MECHANICS / GEOMECHANICS SYMPOSIUM 18-25 June 2021 Online.
* Paper title is "ROP Model for PDC Bits in Geothermal Drilling". Please check out the Paper in the Paper folder.

### Symbolic Regression Algorithm




### Python library

The PySR library is used in this study. check out the PySR website [here](https://pysr.readthedocs.io/en/latest/docs/getting-started/).


### Repository structure

```
├───Archive
├───Data
├───Figures
├───Images
└───Paper
```

### Bits 


PDC bits manufactured by National Oil Varco - NOV (left) and Ulterra (right) are seen at the following image.
<p align="left">
  <img  width="450" src="Images/NOV_bits.PNG" >
  <img  width="450" src="Images/Ulterra_bits.PNG" >
</p>

### Data
The four-row of data used in this study are seen in the following table.

###### Table
```
|   year | name       |     WOB |   ROP data |   Db |   RPM |   UCS |   NOC |   BR |   SR |   Dc |   NOB |
|--------|------------|---------|------------|------|-------|-------|-------|------|------|------|-------|
|   2019 | SWG        | 2543.8  |    6.2     | 3.75 |    80 | 28000 |    11 |   25 |    1 | 0.51 |     4 |
|   2019 | SWG        | 3048.9  |   11.9     | 3.75 |    80 | 28000 |    11 |   25 |    1 | 0.51 |     4 |
|   2019 | SWG        | 3538.7  |   19.5     | 3.75 |    80 | 28000 |    11 |   25 |    1 | 0.51 |     4 |
|   2019 | SWG        | 4066.2  |   28.6     | 3.75 |    80 | 28000 |    11 |   25 |    1 | 0.51 |     4 |
```
###### Data Dimensions
```
WOB is in lbf
ROP data is in ft/hr
Db is in inch
RPM is in rpm
UCS is in psi
NOC is dimensionless
BR is dimensionless
Dc is in inch
NOB is dimensionless
```
### Results

The following equation was found using symbolic regression algorithm.
```
ROP = (pow((((((RPM + 98.457596) / Dc) * WOB) / (UCS - WOB)) - NOB) - NOC, 1.1348255) * 0.31298584)
```
The following figures compare the data versus above ROP model (found by AI).

<p align="left">
  <img  width="1400" src="Figures/Comparison between PDC ROP Model found by AI and ROP DATA.png" >
</p>

<p align="left">
  <img  width="450" src="Figures/ModelvsData.png" >
</p>



<p align="left">
  <img  width="450" src="Figures/Sensitivity_analysis_1.png" >
  <img  width="450" src="Figures/Sensitivity_analysis_2.png" >
</p>




### Suggestions

* The pysr clearly ignores the dimensionality of mathematical equation. The PySR guids the searching processes toward those equations which result in higher accuracy.
* It would be benefacial if the ML algorithm (symbolic regression package) comes with new feathers to consider the dimensionality in the process of evulution.
* One method that can be used for dimensionality consideration in PySR is by using customized loss function. In such case, it is suggested to develope a function that can measure the normalized beahavior of seperate input parameters into the dependant paramter. The influence of independant parameters on dependant paramters can be study seperatly using lab data or from liturature. For instance, there is almost an agreement that the WOB affects the ROP with power bigger than 1. Note that this is true before achieving the flunder point. Once the castomzied objective function was prepared, it is expected that the PySR incorporate more physic into developing equations.
* The sensitivity analysis package in this study was used. As it is seen in above gragh, the PySR found that the WOB, RPM,and UCS have bigger effect on ROP comare to Dc and NOC.
* The results can be affected by the availabe number of data points too.

