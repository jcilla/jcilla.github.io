---
layout: post
title:  "Volleyballad: Hello World!"
date:   2016-02-09 1:41:00 -0800
categories: volleyballad
---
<script src='https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML'></script>

Greetings internet. I'm here to talk about a game that I've been developing slowly after work. And you're probably here to listen to all my failures. Great! Let's get into it.

Lots of sports have a game series - soccer has FIFA, basketball has NBA2K, even ice hockey has NHL2K. But what does volleyball have? Dead or Alive: Xtreme Beach Volleyball is the only well known volleyball game, which is like saying two pieces of bread with a pepperoni in the middle is a sandwich.

I'm trying to make a faithful simulation of indoor six-man volleyball, working title: <i><b>Volleyballad</b></i>. I want the player to be able to control one person on the team, while the rest are controlled by AI, with each AI having its own habits the player can pick up on.

The first important task was to figure out how to get a player to hit a ball toward a target in a parabolic arc.

The hiccup here was figuring out what I could solve for, and choosing which variables I could give as constants. Initially I tried solving for the angle of the trajectory using the maximum height, but that left too many variables unaccounted for. Eventually, I found I could pass the destination and the airtime, and solve for velocity. Beginning with the equation of projectile motion...

$$
r_{1} = \frac{at^2}{2} + vt + r_{0}
$$

Expanding this equation to three components...

$$
\begin{align}
	x_{1}& = v_{x}t + x_{0}
	\\
	y_{1}& = \frac{gt^2}{2} + v_{y}t + y_{0}
	\\
	z_{1}& = v_{z}t + z_{0}
\end{align}
$$

Solving for velocity...

$$
\begin{align}
	v_{z}& = \frac{(x_{1}-x_{0})}{t}
	\\
	v_{y}& = \frac{(y_{1}-y_{0})}{t} - \frac{gt}{2}
	\\
	v_{z}& = \frac{(z_{1}-z_{0})}{t}
\end{align}
$$

And so we end up with something like this.

``` csharp
// C#
Vector3 CalculateVelocityForTrajectory(Vector3 pos, Vector3 dst, float t) {
        Vector3 diff = dst - pos;
        Vector3 v = diff / t;
        v.y -= Physics.gravity.y * t / 2;
        return v;
}
```

As of now, if a player touches the ball, the ball's velocity is set to this value. Check it out in context below!

![SET THE D](/res/blog/trajectory.gif)
{:
	title="SET THE D"
}