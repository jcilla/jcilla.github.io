---
layout: post
title:  "Problems with Unity Physics"
date:   2016-03-07 20:21:00 -0800
categories: unity
---
<script src='https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML'></script>

I have a little thing in Unity that spawns a hundred blocks in a tight space, with many of them overlapping. Then I let the physics do its thing and spread them out somewhat randomly. The problem is that sometimes I find one block completely inside of another, and for some reason Unity decides nothing is wrong and no collisions or anything happen. It's just stuck in there.

The solution I found is to make the rigidbodies' collision mode "ContinuousDynamic" before letting them loose. This makes it much less likely for the blocks to be completely inside one another.
