---
author-meta:
- David R. Slochower
date-meta: '2017-08-04'
keywords:
- work-in-progress
- markdown
- manuscript
- publishing
title: 'Manubot Rootstock: nonequilibrium-barrier'
...

<small><em>
This manuscript was automatically generated
from [slochower/nonequilibrium-barrier@2f5a20f](https://github.com/slochower/nonequilibrium-barrier/tree/2f5a20f069696b242f8633ec1d76aa47fd97987e)
on August  4, 2017.
</em></small>

## Authors


+ **David R. Slochower**<br>
    ![ORCID icon](images/orcid.svg){height="13px"}
    [0000-0003-3928-5050](https://orcid.org/0000-0003-3928-5050)
    · ![GitHub icon](images/github.svg){height="13px"}
    [slochower](https://github.com/slochower)
    · ![Twitter icon](images/twitter.svg){height="13px"}
    [drslochower](https://twitter.com/drslochower)<br>
  <small>
     Skaggs School of Pharmacy and Pharmaceutical Sciences, University of California, San Diego
  </small>


## Abstract

TBD

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

## Optimization of a surface for maximum probability flux

It would be nice to be able to design -- or suggest -- how to design a molecular motor for specific properties (speed, force, torque, gearing, ability to work against a load, resistance to being forced backwards, or something else). To that end, we set out to explore the relationship between the shape of the potential energy surfaces and these properties. [@mNNsAL8U]

### Optimization of a single surface

![The fixed bound potential energy surface during optimization.](https://cdn.rawgit.com/slochower/nonequilibrium-master/bcac92c96f496a888dc02249e40d049032225205/notebooks/surface-optimization/fixed-bound-surfaces.svg){#fig:bound width=10cm}


To start, let's begin with a fixed bound energy surface created by smoothing a sawtooth with six spline points @fig:bound.

This shows the results of [Nelder-Mead optimization](https://en.wikipedia.org/wiki/Nelder%E2%80%93Mead_method), also known as downhill simplex, which should be completely reproducible and deterministic.

There is something I still don't understand about this. The resutls do not seem to be completely reproducable even with setting `np.random.seed(42)`. I have consistently gotten between 1300 and 1400 iterations, but not always the same number.

### Two surfaces, both optimized (?)

## Optimization of a surface for maximum force
