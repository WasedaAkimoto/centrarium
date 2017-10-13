---
layout: post
title:  <font face="德彪钢笔行书字库" size="6">An Efficient Multi-Level Algorithm for 3D-IC TSV Assignment</font>
date:   2017-09-30 10:38:03
author: Cong HAO, Member and Takeshi YOSHIMURA, Fellow
categories: Academia
tags:	3D-IC Floorplan
cover:  "/assets/AAEAAQAAAAAAAAhdAAAAJDljZDFlNDc5LWZjNWQtNDgyNC1hM2ViLTA2M2QzYTQzMWJiNQ.png"
---

<style>
.divcss5{text-indent:35px}
</style>


# <font face="segoe script"><font color="blue"><b>Index</b></font></font>
* Background Introduction
* Problem formulation
* Previous Work
* Contributions
* Terminologies and Theories
* Experimental Results
* Conclusions

------

# <b><font face="segoe script"><font color="blue">Background Introduction</font></font></b>
## <b><font face="segoe script" color="blue" size="2">3D-IC</font></b>
* Advantage:

    Higher density, reduced power, smaller footprint, improved performance, lower cost.
* TSV(Through Silicon Via):

    TSVs are essential component. It passes the silicon layer functioning inter-dies communication.

    TSV could increase inter-die communication bandwidth, reduce form factor, lower power consumption of stacked multi-die systems

![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%871.jpg)
<div class="divcss5">
<p><font size="1">The structure of 3D-IC with TSVs.It shows the connections inner-dies and inter-dies.</font></p>
</div>
-------

# <b><font face="segoe script"><font color="blue">Problem Formulation</font></font></b>

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

-------

# <b><font face="segoe script"><font color="blue">Previos Work</font></font></b>

## <b><font face="segoe script" color="blue" size="2"> Existed Problems</font></b>
* High complexity of a complete IMCMC network.
    The algorithm is not able to handle more grids for a testbench, which degrades the accuracy of TSV assignment.
* NP-completeness of the integer multi-commodity problem.
    Once a flow is assigned for a commodity, it is fixed and cannot be updated.
* Lack of efficiency of optimization.
    Runtime is very time consuming.
--------

# <b><font face="segoe script"><font color="blue">Contribution in the Thesis</font></font></b>

* We group adjacent vertices together level by level to build smaller networks, and send rough flows between the coarsened vertices.
![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%873.png)
<div class="divcss5">
<p><font size="1">Flows are sent roughly on grouped vertices.</font></p>
</div>

* The edges on which rough flows are sent are regarded as promising, and are generated when the coarsened vertices are un-coarsened.
![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%874.png)
<div class="divcss5">
<p><font size="1">Only promising edges are generated.</font></p>
</div>
------

# <b><font face="segoe script"><font color="blue">Algorithms</font></font></b>

## <b><font face="segoe script" color="blue" size="2">Multi-Level TSV Assignment</font></b>
![](http://oxpem0aij.bkt.clouddn.com/1.JPG)

     1. Build coarsened grids of multiple levels

     2. Run the rough flow assignment and un-coarsening, which are executed by turns on each level of graphs composed of coarsened grids.


* 1. Grid Coarsening and Source Grouping
![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%875.png)

    The grid coarsening is performed level by level, the source pins are grouped

![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%876.png)
<div class="divcss5">
<p><font size="1">Chips and dies are divided into grids.Coarsened grid of level ε(ε>0).</font></p>
</div>
 
<div class="divcss5">
<p>[grp]  (source pins)
<p>[grd]  (grids)
<p>The source pins that locate in a same coarsened grid are regarded as one group of level ϵ.</font></p>
</div>


* 2.Rough Flow Assignment
 
![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%877.png)
<div class="divcss5">
<p><font size="1">The coarsened graph of level ε with rough flow assignment.</font></p>
</div>

<div class="divcss5">
<p>The grids with non-zero capacities are called effective grids; both effective and ineffective grids are included in the coarsened graph, but edges are only generated for effective grids.</p>
</div>

* 3.Graph Un-Coarsening
 
![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%878.png)
<div class="divcss5">
<p><font size="1">Coarsened graph of level ε-1 with generated edges. 
</font></p>
</div>

<div class="divcss5">
<p>Similar to last step, un-coarsen for one level and generate edges for effective grids. </p>
</div>










     











<div class="cm-article" data-key="AkimotoYuduki.id"></div>

<link rel="stylesheet" href="//comment.moe/dest/static/css/plus.css">

<script src="//comment.moe/dest/static/js/build.js" charset="UTF-8"></script>


