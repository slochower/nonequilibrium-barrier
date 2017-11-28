---
author-meta:
- David R. Slochower
date-meta: '2017-11-28'
keywords:
- work-in-progress
- markdown
- manuscript
- publishing
title: 'Nonequilibrium molecular motors: optimization and torque'
...

<small><em>
This manuscript was automatically generated
from [slochower/nonequilibrium-barrier@9244179](https://github.com/slochower/nonequilibrium-barrier/tree/9244179633f35b61bd0c69cfddcc0698ce17ed12)
on November 28, 2017.
</em></small>



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
I could look into this further, but I haven't.
It may have to do with the interpolation.

![In my hands, the Nelder-Mead optimization is not completely deterministic.](https://cdn.rawgit.com/slochower/nonequilibrium-master/d346ae563e1c9b584b87695cc431defd14530f5a/notebooks/surface-optimization/nelder-mead-evaluations.svg){#fig:nelder-mead width=10cm}

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


### Optimization of both surfaces for maximal flux
COBYLA in particular handles the bounds and produces highly optimized surfaces after just a few iterations.

## Optimization of a surface for maximum force


## The force on a barrier

It is interesting that in most places $F = 0$.


## Outline

1. Surface with and without a barrier

2. Family of curves showing force on the barrier as a function of height and
position of the barrier.

3. Optimization of a surface for flux and force with and without a barrier.

### Ideas

1. MD and umbrella sampling of a Feringa-type motor.

2. pH change can be modeled as a change in substrate concentration, for our purposes.

3. Can the experimental groups synthesize motors based on an energy surface?

4. CD can be a platform -- a scaffold -- for building, but it will be hard to figure out the appropriate assays.
