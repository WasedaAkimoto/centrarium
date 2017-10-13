---
layout: post
title:  <font face="德彪钢笔行书字库" size="3">An Efficient Multi-Level Algorithm for 3D-IC TSV Assignment</font>
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
## <b><font face="segoe script" color="blue" size="2">3D-IC</font></font></b>
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
*    IMCMC i.e. Integer Multi-Comodity Min-Cost.
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

     











<div class="cm-article" data-key="AkimotoYuduki.id"></div>

<link rel="stylesheet" href="//comment.moe/dest/static/css/plus.css">

<script src="//comment.moe/dest/static/js/build.js" charset="UTF-8"></script>


