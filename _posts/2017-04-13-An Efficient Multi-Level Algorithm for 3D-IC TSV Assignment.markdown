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


<h2 id="Index"><font face="segoe script"><font color="blue"><b>Index</b></font></font></h>

* <a href="#Background Introduction">Background Introduction</a>
* <a href="#Problem formulation">Problem formulation</a>
* <a href="#Previous Work">Previous Work</a>
* <a href="#Contributions">Contributions</a>
* <a href="#Terminologies and Theories">Terminologies and Theories</a>
* <a href="#Experimental Results">Experimental Results</a>
* <a href="#Conclusions">Conclusions</a>
* <a href="#The original link of the thesis">The original link of the thesis</a>

------

<h2 id="Background Introduction"><b><font face="segoe script"><font color="blue">Background Introduction</font></font></b></h>
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

<a href="#Index">Click here to return to the Index</a>
-------

<h2 id="Problem Formulation"><font face="segoe script"><font color="blue">Problem Formulation</font></font></b></h>

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

<a href="#Index">Click here to return to the Index</a>
-------

<h2 id="Previous Work"><b><font face="segoe script"><font color="blue">Previous Work</font></font></b></h>

## <b><font face="segoe script" color="blue" size="2"> Existed Problems</font></b>
* High complexity of a complete IMCMC network.
    The algorithm is not able to handle more grids for a testbench, which degrades the accuracy of TSV assignment.
* NP-completeness of the integer multi-commodity problem.
    Once a flow is assigned for a commodity, it is fixed and cannot be updated.
* Lack of efficiency of optimization.
    Runtime is very time consuming.

<a href="#Index">Click here to return to the Index</a>
--------

<h2 id="Contribution"><b><font face="segoe script"><font color="blue">Contribution in the Thesis</font></font></b></h>

* We group adjacent vertices together level by level to build smaller networks, and send rough flows between the coarsened vertices.
* 
![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%873.png)
<div class="divcss5">
<p><font size="1">Flows are sent roughly on grouped vertices.</font></p>
</div>

* The edges on which rough flows are sent are regarded as promising, and are generated when the coarsened vertices are un-coarsened.
 
![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%874.png)
<div class="divcss5">
<p><font size="1">Only promising edges are generated.</font></p>
</div>

<a href="#Index">Click here to return to the Index</a>

------

<h2 id="Terminologies and Theories"><b><font face="segoe script"><font color="blue">Terminologies and Theories</font></font></b></h>

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
<p>[grp]  (source pins)</p>
<p>[grd]  (grids)</p>
<p>The source pins that locate in a same coarsened grid are regarded as one group of level ϵ.</p>
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

## <b><font face="segoe script" color="blue" size="2">Grid Extension</font></b> 

![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%879.png)
<div class="divcss5">
<p>When the generated edges are insufficient, we're to use this method. </p>
</div>

![](http://oxpem0aij.bkt.clouddn.com/GIF.gif)
<div class="divcss5">
<p><font size="1">The included grids with r = 1 and r = 2, and edges are also generated for these grids. 
</font></p>
</div>

## <b><font face="segoe script" color="blue" size="2">Mixed Single and Multi Commodity Flow</font></b>

![](http://oxpem0aij.bkt.clouddn.com/2.JPG)


    1. Build coarsened grids of multiple levels.
    2. Steps are executed by turns on each level of graphs composed of coarsened grids.

* 1. Mixed Flow on Source Group

![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%872.jpg)
<div class="divcss5">
<p><font size="1">Split edges from e1 to e6.</font></p>
</div>

    (a)Vertices are replaced by edges.
    (b)Assign the net through residual edges.
    (c)Update the flow.

<div class="divcss5">
<p>In order to avoid TSV congestions, we take grid capacities into consideration  so that we use flow networks module.</p>
<p>Grids are replaced by a pair of vertices with a directed edge, called split edge.</p>
<p>Flows from grp1 to t1 and t2 have been found. We find an augmenting path from s3 on the residual network of grp1.</p>
<p>In this step, flows are assigned net by net by successive shortest path. The purpose is to first ensure a feasible assignment for each net, and then minimize the total wire length.</p>
</div>



* 2.Single Commodity Min-Cost Flow

![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%8712.png)
<div class="divcss5">
<p><font size="1">Min-cost flow algorithm being applied on grid vertex g1.</font></p>
</div>

    (a) Initial flow assignment.
    (b) Shortest path from g1 to t2.
    (c) Augmenting path from g1 to t1 through residual path.
    (d)Update flow.

<div class="divcss5">
<p>We first get a shortest path from g1 to t2, and then try to find an augmenting path is found from g1 to t1 on the residual network.</p>
<p>Update the flow assignment, the net is optimally assigned.</p>
<p>In this stage, an optimization of already assigned flows is applied on grid vertices to minimize total wire length only.</p>
</div>

## <b><font face="segoe script" color="blue" size="2">Optimally Assigned Nets</font></b>

![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%8713.png)
<div class="divcss5">
<p><font size="1">Un-Optimally</font></p>
</div>

![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%8714.png)
<div class="divcss5">
<p><font size="1">Optimally</font></p>
</div>

<div class="divcss5">
<p>There’s a principle to judge whether nets are optimally assigned. The total wire length from s to t equals to the half parameter of the bounding box.</p>
</div>

<a href="#Index">Click here to return to the Index</a>

------

<h2 id="Experimental Results"><b><font face="segoe script"><font color="blue">Experimental Results</font></font></b>/h>

## <b><font face="segoe script" color="blue" size="2">Algorithm Efficiency and Solution Quality</font></b>

![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%8715.png)
<div class="divcss5">
<p><font size="1">The difference between the number of original and reduced edges.</font></p>
</div>

![](http://oxpem0aij.bkt.clouddn.com/%E5%9B%BE%E7%89%8716.png)
<div class="divcss5">
<p><font size="1">Results compared with the integer TSV assignment.</font></p>
<p>Pc: monotonically decreasing function of the capacity of edge</p>
<p>Pr: monotonically increasing function of the radius r</p>
</div>

    ML: Simple Multi-Level
    MF: Mixed Flow
    PF: Penalty Function
    FG: Min-Cost Flow

<a href="#Index">Click here to return to the Index</a>

--------

<h2 id="Conclusions"><b><font face="segoe script"><font color="blue">Conclusions</font></font></b></h2>

## <b><font face="segoe script" color="blue" size="2">Algorithms Contribution</font></b>

* An efficient multi-level algorithm for 3D-IC TSV assignment which greatly reduced the number of edges in the IMCMC network
* A mixed single and multi commodity method to improve the solution optimality.

## <b><font face="segoe script" color="blue" size="2">For Application</font></b>

* Achieving 37X speedup
* Reducing the total wire length by 7.0%.

<a href="#Index">Click here to return to the Index</a>



-------
<h2 id="The original link of the thesis">The original link of the thesis:</h>

<a href="http://ieeexplore.ieee.org/document/7604740/"><font size="4"><b>"An Efficient Multi-Level Algorithm for 3D-IC TSV Assignment"</b></font></a>

<a href="#Index">Click here to return to the Index</a>




<div class="cm-article" data-key="AkimotoYuduki.id"></div>

<link rel="stylesheet" href="//comment.moe/dest/static/css/plus.css">

<script src="//comment.moe/dest/static/js/build.js" charset="UTF-8"></script>


