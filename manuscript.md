---
author-meta:
- David R. Slochower
date-meta: '2018-05-08'
keywords:
- markdown
- publishing
- manubot
lang: en-US
title: 'Nonequilibrium molecular motors: optimization and torque'
...






<small><em>
This manuscript
([permalink](https://slochower.github.io/nonequilibrium-barrier/v/58c601e7df11cb27486dc7af8264d57acb491457/))
was automatically generated
from [slochower/nonequilibrium-barrier@58c601e](https://github.com/slochower/nonequilibrium-barrier/tree/58c601e7df11cb27486dc7af8264d57acb491457)
on May 8, 2018.
</em></small>

## Authors



+ **David R. Slochower**<br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [0000-0003-3928-5050](https://orcid.org/0000-0003-3928-5050)
    · ![GitHub icon](images/github.svg){height="13px" width="13px"}
    [slochower](https://github.com/slochower)
    · ![Twitter icon](images/twitter.svg){height="13px" width="13px"}
    [drslochower](https://twitter.com/drslochower)<br>
  <small>
     Skaggs School of Pharmacy and Pharmaceutical Sciences, University of California, San Diego
  </small>



## Abstract {.page_break_before}




## Optimization of the potential energy surfaces

It would be nice to be able to design -- or suggest how to design -- a molecular motor for specific properties: speed, force, torque, gearing, ability to work against a load, resistance to being forced backwards, or something else.
To that end, we set out to explore the relationship between the shape of the potential energy surfaces and these properties.

### Optimization of a single surface for maximal flux

![The fixed bound potential energy surface, based on a sawtooth wave. It is a little misleading, but this curve is actually only the seven points in red, drawn on a scale of 60, to show how the seven points map to the interpolated spline below. That is, the bound state is the curve consisting of the points `{(0, 3), (10, 4), (20, 5), (30, 0), (40, 1), (50, 2), (59, 3)}` interpolated to 60 bins using the spline.](https://cdn.rawgit.com/slochower/nonequilibrium-master/292d5ab98a15e4dfff6ef56d7dc4b7f13764ae11/notebooks/surface-optimization/bound-presmoothing-surface.svg){#fig:bound-presmooth width=10cm}

![The fixed bound potential energy surface after splining.](https://cdn.rawgit.com/slochower/nonequilibrium-master/bcac92c96f496a888dc02249e40d049032225205/notebooks/surface-optimization/fixed-bound-surfaces.svg){#fig:bound width=10cm}

To start, let's begin with a fixed bound energy surface created by smoothing a sawtooth with seven spline points (Figure @fig:bound).
I couldn't find a way to spline across the periodic boundary, so the curve looks a little wonkier than expected.
My first attempt was to use a downhill simplex method ([Nelder-Mead](https://en.wikipedia.org/wiki/Nelder%E2%80%93Mead_method)) to optimize the apo surface for maximal flux.
The algorithm begins with an initial guess of a flat apo surface.
The results are not completely deterministic, even with with setting `np.random.seed(42)`, and I don't understand that.
After 100 loops of the same optimization, using the same initial conditions and random seed, the number of function evaluations in each optimization bounces between around 1400 and around 500!
The non-repeatability of the optimization is repeatable itself, however!
Upon running a further 100 loops on a different day, I observed the same bouncing between 1400 and 500 iterations.
I could look into this further, but I haven't.
It may have to do with the interpolation.

![In my hands, the Nelder-Mead optimization is not completely deterministic.](https://cdn.rawgit.com/slochower/nonequilibrium-master/d346ae563e1c9b584b87695cc431defd14530f5a/notebooks/surface-optimization/nelder-mead-evaluations.svg){#fig:nelder-mead width=10cm}

![Predictably, non-deterministic.](https://cdn.rawgit.com/slochower/nonequilibrium-master/b5c42b4efcc295635d96989d00462ed18f253e89/notebooks/surface-optimization/nelder-mead-evaluations.svg){#fig:nelder-mead-2 width=10cm}

![The result of the optimized apo potential energy surface.](https://cdn.rawgit.com/slochower/nonequilibrium-master/292d5ab98a15e4dfff6ef56d7dc4b7f13764ae11/notebooks/surface-optimization/optimized-apo-surfaces.png){#fig:optimized width=10cm}

After 1403 iterations, Nelder-Mead optimization results in the surface shown in Figure @fig:optimized.
Each blue line is an iteration of the optimization.
Lighter colors correspond to earlier iterations.
The final surface is darker because many lines are overlaid.
I have not implemented bounds on the optimization because Nelder-Mead does not allow bounds, as far as I know.
I'll return to the idea of using bounds a little later.
The result of this optimization is that the flux starts near $0$ (although not exactly at zero, curiously) and drops to $-0.050 \,\text{cycle s}^{-1}$ quickly and stays there.

![The flux during optimization.](https://cdn.rawgit.com/slochower/nonequilibrium-master/292d5ab98a15e4dfff6ef56d7dc4b7f13764ae11/notebooks/surface-optimization/flux-iterations.png){#fig:optimized-flux width=10cm}

COBYLA and Powell's method result in better optimization than simplex downhill.
After 269 iterations, COBYLA approaches flux of more than $-250 \,\text{cycle s}^{-1}$, with the flux beginning to decrease after just a few iterations.
The iterations of COBYLA look like they are refining a single landscape, instead of jumping around.
Powell's method does well, too, although it occasionally jumps back to near zero flux after finding a high value.

Taken together, the fixed bound surface and the COBYLA-optimized apo surface are shown below.

![The COBYLA-optimized energy surfaces.](https://cdn.rawgit.com/slochower/nonequilibrium-master/01269a9f99c5d5858c1b903fb72b34c390c5f3b0/notebooks/surface-optimization/COBYLA-optimized-surfaces.png){#fig:cobyla-optimized-surfaces width=10cm}

![The COBYLA-optimized energy surfaces.](https://cdn.rawgit.com/slochower/nonequilibrium-master/01269a9f99c5d5858c1b903fb72b34c390c5f3b0/notebooks/surface-optimization/COBYLA-optimized-flux.png){#fig:cobyla-optimized-flux width=10cm}

Curiously, the flux is mostly zero across the

### Optimization of both surfaces for maximal flux
COBYLA in particular handles the bounds and produces highly optimized surfaces after just a few iterations.

## Optimization of a surface for maximum force


## The force on a barrier

It is interesting that in most places $F = 0$.


## Earlier outline (Sat Feb 17 17:14:00 2018 -0800 `#72608ff` in `motor-thoughts` 

Title: Phase-Dependent Stall Forces in Brownian Motors [Or maybe a catchier title based on analogies with 4-stroke engines and cyclists, see below]

Introduction 
Molecular motors are thought to work as Brownian ratchets, so Brownian ratchets are interesting. Key performance characteristics of motors are:
maximum speed (e.g., linear velocity for a walker, cycles per second for a rotary motor). For a probabilistic Brownian motor, we think of this is a probability flux
maximum force, or stall force. 
maximum power output to a load
One may expect maximum speed to be attained in the absence of any external load, so solving a model for this parameter would seem fairly straightforward. 
Stall force is typically obtained by imposing a linear energy gradient along the motor's coordinate of motion (e.g. x for a linear motor, phi for a rotary one). This corresponds to a constant force along the coordinate. One increases the force until the flux goes to zero, and then reads out the stall force. 
The force exerted by a macroscopic motor may depend on the phase of its working cycle. For example, the torque output of one cylinder of a 4-stroke engine varies enormously with rotation phase, and is in fact directed opposite to the direction of motion during most of the cycle (if I am reading this right: http://www.epi-eng.com/piston_engine_technology/torsional_excitation_from_piston_engines.htm).  Similarly, the torque a cyclist exerts on the crankset is high when the crank arm is horizontal, but zero when arm is vertical. Thus, the stall force of a macroscopic motor can, in general, depend on the phase of its operating cycle.  This has functional relevance: a four-cycle engine needs multiple cylinders to generating continuous forward torque (I think); and cyclists may stall when climbing a hill if their speed gets so low that they don't have enough momentum for the crank arm to go through the zero-torque vertical orientation. 
It is thus interesting to consider how the stall force exerted by a Brownian motor depends on the phase of its cycle. We examine this issue here, for a simple Brownian rotary motor model, by computing the torques exerted on high barriers which bring the flux to zero. We find that the stall torque depends strongly on phase. We also find that low barriers not large enough to bring the flux to zero can have complex effects on the motor's operating cycle, and may even cause the direction of the flux to reverse.  
Methods
    Theory of forces on barriers
    Motor model and solving the model

Results
I think we can look at just 1-3 different potential functions. Maybe even just a rounded sawtooth. I don't think we need to crank through loads of cases from our MD runs. 
Graphs of torque as a function of phase and barrier height (as you have already made). Observations of torque crossing through zero at some places (major energy minima, I think). Analogy with cylinder of 4-stroke engine.
Empirical relationship between conventional stall force results and barrier stall force results. (It would be nice if we could relate these, but there may not be a clean relationship to find.)

Discussion
We hypothesize, based on these results, that molecular motors also will have phase-dependent forces or torques. The pattern of these may also be informative regarding mechanisms (maybe we can flesh out ideas like this). May be challenging to measure, as probably need the motor's linkage to the force sensor to be quite rigid, in the sense of having fluctuations that are small in relation to the motor's cycle. Maybe comment that, just as a 4-stroke engine needs multiple cylinders out of phase on a camshaft to generate smooth motion (any net motion), due to phase dependence of torque, so perhaps the F1 ATPas has multiple equivalent active sites that together drive the shaft. 
Also may speculate that imposing low barriers on some motors could lead to reversal of direction. (However, I suspect that evolved motors, at least, are probably robust against this.)

===================

Questions/issues to examine

1) Relationship between conventional stall force results and barrier stall force results. (It would be nice if we could relate these, but there may not be a clean relationship to find.)

2) Should we test our "pressure" method of computing the force with a numerical example? I think the way to do this would be to set up a motor model with a very large number of bins (e.g. 1000), and 
3) Our motor models so far assume a catalytic rate constant that is uniform in phi. I wonder how the present results would change if we focused kcat>0 in some key part of the cycle. Could we get rid of the zero-torque locations? I don't think this would happen, but it may be worth considering for the paper, since I think biomolecular motors do have a phase-dependent kcat.

4) Due diligence again: can our results and ideas really be new? I've made another scan of literature on line, and haven't found them, but it seems unexpected that such a seemingly basic issue would not have been addressed.




## Tentative title: Force generation by Brownian Ratchets (or: molecular motors)

We are interested in optimizing the performance of molecular motors.


It would be nice to be able to design -- or suggest how to design -- a molecular motor for specific properties: speed, force, torque, gearing, ability to work against a load, resistance to being forced backwards, or something else.
To that end, we set out to explore the relationship between the shape of the potential energy surfaces and these properties.

We address these issues by showing how to determine the force exerted by a Brownian motor on a localized barrier. 
We then explore the consequences of this formulation by looking at how the barrier force varies as a function of the barrier height and of its location (or phase), and by using this approach to efficiently derive energy surfaces optimized for force generation.


## Outline

1. Surface with and without a barrier

2. Family of curves showing force on the barrier as a function of height and position of the barrier.

3. Optimization of a surface for flux and force with and without a barrier.

### Ideas



## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>