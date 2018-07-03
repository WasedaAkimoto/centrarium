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

## <b><font face="segoe script" color="blue" size="2">1.Conditional Grid Extension</font></b>

<div class="divcss5">
<p>In [1], the number of effective grids during un-coarsening is usually limited, which results in the insufficient number of edges for coarsened graph.</p>
<p>[2] proposed an unconditional grid extension that is very time consuming results from iteration in which r is a constant in all levels.</p>
</div>

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
 

 


   

## <b><font face="segoe script" color="blue" size="2">2.HVH Channel Routing</font></b>

<div class="divcss5">
<p>In [2] and [3], the detail of interlayer connection was ignored.
</p>
</div>

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


## <b><font face="segoe script" color="blue" size="2">3.Revision of Pin Locations </font></b>

<div class="divcss5">  
<p>It used to assign pins and TSVs as well as calculating the wirelength based on the assumption that pins are located at the center of the grid. Error is accumulated.</p>
</div>

* I revise the location coordinates by adding the offset distance to pins.
 
    d<sub>off</sub>=|node<sub>(1<sub>x</sub>)</sub>-node<sub>(2<sub>x</sub>)</sub> |+|node<sub>(1<sub>y</sub>)</sub>−node<sub>(2<sub>y</sub>)</sub> |


* Merits of my work
<div class="divcss5">  
<p>Error of wirelength is eliminated.</p>
</div>



## <b><font face="segoe script" color="blue" size="2">4.Thermal Resistive Model</font></b>
## <b><font face="segoe script" color="blue" size="2">5.Multi-pins in a Net</font></b>
<a href="#Index">Click here to return to the Index</a>
-------

<h2 id="The original link of the thesis">The original link of the thesis:</h2>

## <b><font face="segoe script" color="blue" size="2">International conference PATMOS thesis</font></b>

<a href="http://pba9e7hoh.bkt.clouddn.com/conference_071817.pdf"><font size="4"><b>"TSV Assignment of Thermal and Wirelength Optimization for 3D-IC"</b></font></a>

## <b><font face="segoe script" color="blue" size="2">Graduation dissertation</font></b>

<a href="http://pba9e7hoh.bkt.clouddn.com/Thesis_44161555-9ZhaoYi.pdf"><font size="4"><b>"TSV Assignment of Thermal and Wirelength Optimization for 3D-IC"</b></font></a>

<a href="#Index">Click here to return to the Index</a>




<div class="cm-article" data-key="AkimotoYuduki.id"></div>

<link rel="stylesheet" href="//comment.moe/dest/static/css/plus.css">

<script src="//comment.moe/dest/static/js/build.js" charset="UTF-8"></script>


