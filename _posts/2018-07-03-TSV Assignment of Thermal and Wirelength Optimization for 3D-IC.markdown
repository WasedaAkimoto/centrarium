---
layout: post
title:  TSV Assignment of Thermal and Wirelength Optimization for 3D-IC
date:   2018-07-03 19:02:03
author: Yi ZHAO, Cong HAO, and Takeshi YOSHIMURA
categories: Academia
tags:	3D-IC Floorplan
cover:  "/assets/AAEAAQAAAAAAAAhdAAAAJDljZDFlNDc5LWZjNWQtNDgyNC1hM2ViLTA2M2QzYTQzMWJiNQ.png"
---

<style>
.divcss5{text-indent:35px}
</style>


<h2 id="Index"><font face="segoe script"><font color="blue"><b>Index</b></font></font></h2>

* <a href="#Background Introduction">Background Introduction</a>
* <a href="#Problem Formulation">Problem Formulation</a>
* <a href="#Terminologies and Theories">Terminologies and Theories</a>
<div class="divcss5">
<p>- <a href="#Conditional Grid Extension">Conditional Grid Extension</a></p>
<p>- <a href="#HVH Channel Routing">HVH Channel Routing</a></p>
<p>- <a href="#Grid Location Revision">Grid Location Revision</a></p>
<p>- <a href="#Thermal Resistive Model">Thermal Resistive Model</a></p>
<p>- <a href="#Multi-pins in a Net">Multi-pins in a Net</a></p>
</div>
* <a href="#Experimental Results">Experimental Results</a>
* <a href="#Conclusions">Conclusions</a>
* <a href="#The original link of the thesis">The original link of the thesis</a>

------

<h2 id="Background Introduction"><b><font face="segoe script"><font color="blue">Background Introduction</font></font></b></h2>
## <b><font face="segoe script" color="blue" size="2">3D-IC</font></b>
* Advantage:

    Higher density, reduced power, smaller footprint, improved performance, lower cost.
* TSV(Through Silicon Via):

    TSVs are essential component. It passes the silicon layer functioning inter-dies communication.

![](http://pba9e7hoh.bkt.clouddn.com/1-2.JPG)
<div class="divcss5">
<p><font size="1">TSVs, TSV landing pads, and connections to TSV landing pads.</font></p>
</div>

   Chips with different functions pile layer by layer in the vertical directions.TSV could increase inter-die communication bandwidth, reduce form factor, lower power consumption of stacked multi-die systems.
   
   ![](http://pba9e7hoh.bkt.clouddn.com/1-1.jpg)
<div class="divcss5">
<p><font size="1">The entire 3D-IC module</font></p>
</div>


<a href="#Index">Click here to return to the Index</a>
-------

<h2 id="Problem Formulation"><b><font face="segoe script"><font color="blue">Problem Formulation</font></font></b></h2>

## <b><font face="segoe script" color="blue" size="2"> What is TSV Assignement problem?</font></b>

*  The optimization of the number and locations of TSVs.
    
    Given a 3-D IC, we’ll decide which and how many TSVs are used to implement the nets spanning different chip dies. 

* Necessity
 
     1.The large area of TSVs.

     2.Crucial to the wire length and signal delays of 3-D circuits

## <b><font face="segoe script" color="blue" size="2"> IMCMC Network</font></b>

![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%872.png)
<div class="divcss5">
<p><font size="1">In the grapgh above, source pins, sink pins and grids belong to different layers.</font></p>
</div>

* IMCMC i.e. Integer Multi-Comodity Min-Cost.
    Two nets 1 = (s1; t1) and 2 = (s2; t2).

    3 TSVs exist between every two layers.

    Two nets are in yellow and blue respectively.
    
* The Goal

    To find a TSV assignment for each net &#951;_i=(s_i,t_i) to minimize the total wire length.

## <b><font face="segoe script" color="blue" size="2"> Coarsening and Un-coarsening Algorithm</font></b>

* We group adjacent vertices together level by level to build smaller networks, and send rough flows between the coarsened vertices.
* 
![](http://pba9e7hoh.bkt.clouddn.com/t1.JPG)
<div class="divcss5">
<p><font size="1">Flows are sent roughly on grouped vertices.</font></p>
</div>

* The edges on which rough flows are sent are regarded as promising, and are generated when the coarsened vertices are un-coarsened.
 
![](http://pba9e7hoh.bkt.clouddn.com/t2.JPG)
<div class="divcss5">
<p><font size="1">Only promising edges are generated.</font></p>
</div>

## <b><font face="segoe script" color="blue" size="2"> Multi-Level TSV Assignment</font></b>

![](http://oxpem0aij.bkt.clouddn.com/1.JPG)

     1. Build coarsened grids of multiple levels
     2. Run the rough flow assignment and un-coarsening, which are executed by turns on each level of graphs composed of coarsened grids.


* 1. Grid Coarsening and Source Grouping
 
![](http://pba9e7hoh.bkt.clouddn.com/t3.JPG)

    The grid coarsening is performed level by level, the source pins are grouped

![](http://pba9e7hoh.bkt.clouddn.com/t4.JPG)
<div class="divcss5">
<p><font size="1">Chips and dies are divided into grids.Coarsened grid of level ε(ε>0).</font></p>
</div>
 
<div class="divcss5">
<p>[grp]  (source pins)</p>
<p>[grd]  (grids)</p>
<p>The source pins that locate in a same coarsened grid are regarded as one group of level ϵ.</p>
</div>

* 2.Rough Flow Assignment
 
![](http://pba9e7hoh.bkt.clouddn.com/t5.JPG)
<div class="divcss5">
<p><font size="1">The coarsened graph of level ε with rough flow assignment.</font></p>
</div>

<div class="divcss5">
<p>The grids with non-zero capacities are called effective grids; both effective and ineffective grids are included in the coarsened graph, but edges are only generated for effective grids.</p>
</div>

* 3.Graph Un-Coarsening
 
![](http://pba9e7hoh.bkt.clouddn.com/t6.JPG)
<div class="divcss5">
<p><font size="1">Coarsened graph of level ε-1 with generated edges. 
</font></p>
</div>

<div class="divcss5">
<p>Similar to last step, un-coarsen for one level and generate edges for effective grids. </p>
</div>



<a href="#Index">Click here to return to the Index</a>
-------

<h2 id="Terminologies and Theories"><b><font face="segoe script"><font color="blue">Terminologies and Theories</font></font></b></h2>

In my research, the multi-level assignment will follow the following prosedure.
![](http://pba9e7hoh.bkt.clouddn.com/flowchart.JPG)
<div class="divcss5">
<p><font size="1">Algorithm flow of multilevel assignment 
</font></p>
</div>

## <a id="Conditional Grid Extension"><b><font face="segoe script" color="blue" size="2">1.Conditional Grid Extension</font></b></a>




In [[1]], the number of effective grids during un-coarsening is usually limited, which results in the insufficient number of edges for coarsened graph.

[[2]] proposed an unconditional grid extension that is very time consuming results from iteration in which r is a constant in all levels.


![](http://pba9e7hoh.bkt.clouddn.com/t9.JPG)

* Denoting the extending radius as r, the edges are generated for the effective grids in the region of radius r.
<div class="divcss5">
<p> Different coarsening level ε uses respective r.</p>

<p> The higher the level is, the less iteration is needed.</p>
</div>

![](http://oxpem0aij.bkt.clouddn.com/GIF.gif)
<div class="divcss5">
<p><font size="1">The included grids with r = 1 and r = 2, and edges are also generated for these grids. 
</font></p>
</div>

* Merits of my work
<div class="divcss5">
<p>I set different coefficient in each iteration to increase efficiency.</p>
<p>Conditional r could avoid the excessive iterative processes which could save much storage and time.</p>
</div>
 
<a href="#Index">Click here to return to the Index</a>
 


   

<a id="HVH Channel Routing"><b><font face="segoe script" color="blue" size="2">2.HVH Channel Routing</font></b></a>


In [[2]] and [[3]], the detail of interlayer connection was ignored.



* Merits of my work
<div class="divcss5">
<p>The wire width could be taken into consideration.</p>
<p>The capacitance exists between the wires generated from the electric connection.</p>
<p>It makes smaller congestion leading to less unnecessary routes and blocking of nets.</p></div>
   

![](http://pba9e7hoh.bkt.clouddn.com/4-1.PNG)
<div class="divcss5">
<p><font size="1">Metal wire orientation 
</font></p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/4-2.PNG)
<div class="divcss5">
<p><font size="1">Cross Wire Orientation
</font></p>
</div>

* Routing rule
<div class="divcss5">
<p>If the first layer is reserved for vertical components, the next layer is reserved for horizontal components, next is vertical, and so on.</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/4-7.jpg)
<div class="divcss5">
<p><font size="1">An instance of HVH channel routing
</font></p>
</div>

* Wirelength
<div class="divcss5">
<p>Wirelength could be calculated by Manhattan Distance in the bounding box composes of source and sink pin.</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t23.JPG)

<div class="divcss5">  
<p>Where l is the number of layer, l<sub>n</sub> is the number of layer the net passes totally, h is the height between adjacent layers and u, v are edges in the net.</p>
</div>

<a href="#Index">Click here to return to the Index</a>

<a id="Grid Location Revision"><b><font face="segoe script" color="blue" size="2">3.Revision of Pin Locations </font></b></a>


<div class="divcss5">  
<p>It used to assign pins and TSVs as well as calculating the wirelength based on the assumption that pins are located at the center of the grid. Error is accumulated.</p>
</div>

* I revise the location coordinates by adding the offset distance to pins.
 
<div class="divcss5">  

    d<sub>off</sub>=|node<sub>(1<sub>x</sub>)</sub>-node<sub>(2<sub>x</sub>)</sub>|+|node<sub>(1<sub>y</sub>)</sub>−node<sub>(2<sub>y</sub>)</sub>|
</div>

* Merits of my work
<div class="divcss5">  
<p>Error of wirelength is eliminated.</p>
</div>

<a href="#Index">Click here to return to the Index</a>

<a id="Thermal Resistive Model"><b><font face="segoe script" color="blue" size="2">4.Thermal Resistive Model</font></b></a>


 
[[4]] made use of thermal model in 3D-IC and proposed some compression storage method to calculations.


* Heat Dissipation Path
<div class="divcss5"> 
<p>our model properly takes the effect of layer assignment and thermal TSV into consideration according to the heat dissipation path.</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/3-1.JPG)
<div class="divcss5">
<p><font size="1">Heat dissipation path
</font></p>
</div>

* Thermal Resistance

    R=(T<sub>2</sub>-T<sub>1</sub>)/P

<div class="divcss5"> 
<p>Where T<sub>2</sub>−T<sub>1</sub> is the temperature difference between two edges of an object, P is the power consumption.
</p>
</div>

* Thermal Conductance

    g=1/R

* Merits of my work

<div class="divcss5"> 
<p>We could simulate temperature distribution of each layer and optimize the thermal condition of overheated regions. 
</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t23.JPG)

* Resistive network

<div class="divcss5"> 
1. Coefficients



<p>- <span style="text-decoration:overline;">V</span><sub>i</sub>: constant room temperature</p>

<p>- v<sub>i</sub>: temperature of node i that needs evaluating</p>

<p>- I<sub>i</sub>: heat generated at node i that changes according to the signal TSV number in the corresponding grid</p>

<p>- g<sub>i,j</sub>: thermal conductivity between node i and j.</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/1-4.JPG)
<div class="divcss5">
<p><font size="1">Resistive network of one chip die with 4 x 4 grid size
</font></p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/1-5new.JPG)
<div class="divcss5">
<p><font size="1">Incoming current for node i
</font></p>
</div>




<div class="divcss5"> 
2. For a chip consists of m x n grids, according to Current Conservation Theorem,
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t10.JPG)

<div class="divcss5"> 
3. Resistive network
<p>- Matrix equation of one chip die</p> 
    G*V=I+<span style="text-decoration:overline;">V</span>=<span style="text-decoration:overline;">I</span>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t12.JPG)

<div class="divcss5"> 
<p>Value of g<sub>i,j</sub>,</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t11.JPG)

<div class="divcss5"> 
<p>
- Matrix equation of 3D-IC</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t13.JPG)

<div class="divcss5"> 
4. Effect of thermal TSV
<p>- Overheated grids, v &ge; v<sub>th</sub>, where v<sub>th</sub> is the value of 10% highest temperature of grids.</p>
<p>- The number of thermal TSV on each grid</p>
    ttsv<sub>num</sub>=(grid area-total area of components)/(thermal TSV area)
<p>Thermal TSV brings parallel thermal conductance.</p>
    g<sub>ij</sub> &rarr; g<sub>ij</sub>+g<sub>TSV</sub>*ttsv<sub>num</sub>
<p>Get the new V={v<sub>1</sub>,v<sub>2</sub>...v<sub>n</sub>} by calculating the matrix equation.</p>
</div>

<a href="#Index">Click here to return to the Index</a>

<a id="Multi-pins in a Net"><b><font face="segoe script" color="blue" size="2">5.Multi-pins in a Net</font></b></a>



[[5]] and [[6]] discussed different TSV assignment model. But there are still only two pins in a net.


* Merits of my work

<div class="divcss5"> 
<p>Multi-pins in a net is discussed and I introduce algorithms to help build the tree.</p>
<p>I consider a more realistic model that a net contains multiple pins denoted as n=(s<sup>1</sup>,s<sup>2</sup>,s<sup>3</sup>...s<sup>m</sup>,t).</p>
1. Construction of 2D RST
<p>Project pins onto one plane and construct minimum rectilinear Steiner tree.</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/5-10.JPG)
<div class="divcss5">
<p><font size="1">2S RST
</font></p>
</div>


<div class="divcss5">
2. Fast Lookup Table Estimation(FLUTE)
<p>Put the pins into Hanan grid and RST is decomposed of a branch of Hanan edges. 1h<sub>1</sub>+2h<sub>2</sub>+1h<sub>3</sub>+1v<sub>1</sub>+1v<sub>2</sub>+2v<sub>3</sub>.</p>
</div>
[[7]]

![](http://pba9e7hoh.bkt.clouddn.com/5-12.JPG)
<div class="divcss5">
<p><font size="1">2D RST
</font></p>
</div>

<div class="divcss5">
<p>We could transfer to linear combination.
(1,2,1,1,1,2), (1,1,1,1,2,3), (1,2,1,1,1,1).</p>
<p>Simplicity of comparing wirelength.</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t28.JPG)

![](http://pba9e7hoh.bkt.clouddn.com/5-11.JPG)
<div class="divcss5">
<p><font size="1">3D RST
</font></p>
</div>

<div class="divcss5">
3. Construction of 3D RST
<p>3 occasions of TSV location relationship</p>
<p>- tTop is smaller than tBot, we use an edge to connect tTop-th layer with tBot-th;</p>
<p>- tTop equals to tBot, we could directly use planar wires to connect two TSVs;</p>
<p>- tTop is larger than tBot, there's overlap of layers so that we needn't add wires between layers, but use existed wires on whichever [tTop,tBot] layer.</p>
</div>
![](http://pba9e7hoh.bkt.clouddn.com/t27.JPG)

<div class="divcss5">
4. Wirelength Metrics
</div>

<div class="divcss5">
HPWL-2DBB
</div>
![](http://pba9e7hoh.bkt.clouddn.com/t25.JPG)
<div class="divcss5">
HPWL-3DBB
</div>
![](http://pba9e7hoh.bkt.clouddn.com/t26.JPG)

<div class="divcss5">
<p>HPWL is half perimeter wirelength for short.</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/5-4.JPG)
<div class="divcss5">
<p><font size="1">HPWL-2DBB
</font></p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/5-5.JPG)
<div class="divcss5">
<p><font size="1">HPWL-3DBB
</font></p>
</div>

<a href="#Index">Click here to return to the Index</a>
-------

<h2 id="Experimental Results"><b><font face="segoe script"><font color="blue">Experimental Results</font></font></b></h2>

<div class="divcss5">
1. Experimental Environment
</div>

<div class="divcss5">
<p>I test algorithms using C programming language on the 2.5GHz Intel(R) Core(M) workstation with 8-GB memory.</p>
<p>- grid size: Each layer is divided into g1xg2 grids.</p>
<p>- layer: The number of chip dies of 3D-IC.</p>
<p>- #net: The total number of nets in the netlists.</p>
<p>- #g_exist: The number of grids with capacity, which could contain TSVs.</p>
<p>- #max cap: The maximum capacity of grids.</p>
</div>
![](http://pba9e7hoh.bkt.clouddn.com/t16.JPG)

<div class="divcss5">
2. Evaluation of Conditional Grid Extension Algorithm
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t22.JPG)
<div class="divcss5">
<p>- Unconditional grid extension reduces the wirelength by 5.1% and conditional grid extension reduces by 8.2%.</p>
<p>- Conditional grid extension eliminates on average 32.7% overflows.</p>
<p>- Conditional grid extension could save the time cost by 30.2% on average.</p>
</div>

<div class="divcss5">
3. With/Without HVH Structure and Location Revision
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t21.JPG)
<div class="divcss5">
<p>- I use Mahattan Distance in HVH channel, wirelength is 13.2% to 20.5%, 18.2% on average more accurate.</p>
<p>- Location revision step makes the results more accurate by 8% on average.</p>
</div>

<div class="divcss5">
4. Evaluation of Temperature Distribution
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t17.JPG)

<div class="divcss5">
<p>The value of each physical variable is given in the table.</p>
</div>
[[8]]

<div class="divcss5">
<p>- Table shows the average temperature and number of inserted TSV in each layer.</p>
<p>- Generally the higher layer has the higher average temperature.</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t18.JPG)

<div class="divcss5">
<p>- The temperature is increasing as the color going to red from blue.</p>
<p>- The color of overheated regions of the circuits fades proving the heat dissipation path makes sense.</p>
</div>

![](http://pba9e7hoh.bkt.clouddn.com/6-1new.JPG)

<div class="divcss5">
5. Comparison of MST-based and RST-based floorplan
</div>

![](http://pba9e7hoh.bkt.clouddn.com/t20.JPG)

<div class="divcss5">
<p>- By using RST the HPWL-3D could be reduced 10% around and the number of TSVs is 18% less.</p>
<p>- With the number of dies goes up, the improvement by RST becomes more obvious.</p>
</div>

<a href="#Index">Click here to return to the Index</a>
------

<h2 id="Conclusions"><b><font face="segoe script"><font color="blue">Conclusions</font></font></b></h2>

* We apply conditional grid extension method to extend the effective grids, which reduces many overflows and saves much time.
* Our HVH channel and location revision considers more realistic occasions making results more accurate.
* We use thermal resistive model to estimate temperature distribution and thermal TSV to decrease temperature.
* We propose a viable procedure to make assignment in the occasion that multiple pins exist in a net.

<a href="#Index">Click here to return to the Index</a>
-------

<h2 id="The original link of the thesis"><b><font face="segoe script"><font color="blue">The original link of the thesis:</font></font></b></h2>

## <b><font face="segoe script" color="blue" size="2">2018 28th International Symposium on Power and Timing Modeling, Optimization and Simulation (PATMOS) thesis</font></b>

<a href="http://pba9e7hoh.bkt.clouddn.com/08464161.pdf"><font size="4"><b>"TSV Assignment of Thermal and Wirelength Optimization for 3D-IC"</b></font></a>

## <b><font face="segoe script" color="blue" size="2">IEEE Transactions on Electron Devices paper</font></b>

<a href="http://pba9e7hoh.bkt.clouddn.com/Transactions.pdf"><font size="4"><b>"Thermal and Wirelength Optimization with TSV Assignment for 3D-IC"</b></font></a>

## <b><font face="segoe script" color="blue" size="2">Graduation dissertation</font></b>

<a href="http://pba9e7hoh.bkt.clouddn.com/Thesis_44161555-9ZhaoYi.pdf"><font size="4"><b>"TSV Assignment of Thermal and Wirelength Optimization for 3D-IC"</b></font></a>

<a href="#Index">Click here to return to the Index</a>
------


[1]: https://ieeexplore.ieee.org/document/7604740/
[2]: https://search.ieice.org/bin/summary.php?id=e100-a_3_776
[3]: https://ieeexplore.ieee.org/document/1167513/
[4]: https://ieeexplore.ieee.org/document/8106948/
[5]: https://ieeexplore.ieee.org/document/6268361/
[6]: https://dl.acm.org/citation.cfm?id=1850914
[7]: https://ieeexplore.ieee.org/document/4358497/
[8]: https://ieeexplore.ieee.org/document/6706671/



<div class="cm-article" data-key="AkimotoYuduki.id"></div>

<link rel="stylesheet" href="//comment.moe/dest/static/css/plus.css">

<script src="//comment.moe/dest/static/js/build.js" charset="UTF-8"></script>


