---
author:
- David R. Slochower
keywords:
- work-in-progress
- markdown
- manuscript
- publishing
title: 'Manubot Rootstock: nonequilibrium-barrier'
...


<small><em>
This manuscript was automatically generated from [slochower/nonequilibrium-barrier@27c541e](https://github.com/slochower/nonequilibrium-barrier/tree/27c541eaa543c3491b3cbe0cfa9078d670126796).
</em></small>


# Manubot Rootstock: Molecular motors with barriers

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
[@SdO7fVnR]

### Ideas

1. MD and umbrella sampling of a Feringa-type motor.

2. pH change can be modeled as a change in substrate concentration, for our purposes.

3. Can the experimental groups synthesize motors based on an energy surface?

4. CD can be a platform -- a scaffold -- for building, but it will be hard to figure out the appropriate assays.

## Optimization of a surface for maximum probability flux

It would be nice to be able to design -- or suggest -- how to design a molecular motor for specific properties (speed, force, torque, gearing, ability to work against a load, resistance to being forced backwards, or something else).

### Two surfaces, starting with

Starting with a fixed bound surface
![](https://github.com/slochower/nonequilibrium-master/blob/bcac92c96f496a888dc02249e40d049032225205/notebooks/surface-optimization/fixed-bound-surfaces.svg){#fig:fixed-bound-surfaces}

There is something I still don't understand about this. The resutls do not seem to be completely reproducable even with setting `np.random.seed(42)`. I have consistently gotten between 1300 and 1400 iterations, but not always the same number.

### Two surfaces, both optimized (?)

## Optimization of a surface for maximum force
