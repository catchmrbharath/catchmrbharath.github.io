---
layout: post
title: "GSoC last week"
description: ""
category: gsoc
comments: true
tags: [gsoc]
---

This happens to be the last week of GSoC. The major things that I accomplished this
week are

* Got pylab to work interactively.
* Made more changes to the documentation of plotting module. 

I have a pull request for the restructured plotting module at [here](https://github.com/sympy/sympy/pull/1468).
There has been lots of discussions on how the new plot API should look like in the pull request.
The API as of now has 5 functions:

* ``plot_line`` which plots 2D line plots, which I think I will change to ``plot``.
* ``plot_parametric`` which plots 2D parametric plots.
* ``plot3D`` which plots 3D plots.
* ``plot3D_parametric`` which plots 3D parametric line plots. I think I will have to 
change it into ``plot_parametric3D``.
* ``plot3D_surface`` which plots 3D parametric surfaces.

The names are slightly confusing, but the alternative to these names are big. If you
have any good names for 3D plots, please leave it in the comments.

I will have another post describing the things I learnt over this GSoC period.
