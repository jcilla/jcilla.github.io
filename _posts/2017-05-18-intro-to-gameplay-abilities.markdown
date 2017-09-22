---
layout: post
title:  "Intro to Gameplay Abilities"
date:   2017-05-18 19:33:00 -0800
categories: UE4
---
<script src='https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML'></script>

Unreal Engine has a module called Gameplay Abilities, which are exactly what they sound like. Apparently it is in use for Paragon, and they are slowly trickling the full functionality into UE4. There's a ton of functionality available here. You can:
* Apply effects to targeted areas or Actors. Set things on fire, slow them, poison them, the works.
* Cast an ability that grants another ability. Combo attacks can be written this way.
* Conditionally cast abilities or apply effects. Shatter enemies that have been frozen. Only set tarred enemies on fire.
* Apply modifiers to attributes. Keep track of doubling attack, with a weakness debuff, etc, with different periods and durations all at the same time.
* Spawn other Actors. Shoot bullets, raise the dead!
* And much more...

Everything is modular. An AbilitySystemComponent (ASC) keeps track of all a character's ability needs. It activates a GameplayAbility, which might apply a GameplayEffect to something, or have some custom logic like playing animations or dealing damage. GameplayCues are meant to be client side effects, like particles or sounds. So on and so forth. Anything you can think of, this system can probably do it.

The whole system goes hand in hand with another system called GameplayTags, which is basically a big heirarchical tree of tags. An example of a list could be
* Damage
  * Elemental
    * Fire
    * Ice
  * Physical
    * Piercing
    * Bludgeoning
* Status
  * Buff
    * Haste
  * Debuff
    * Frozen

Generally tags are given and taken from ASCs through GameplayEffects. You can query for things like "target's tags include elemental damage" or "target is buffed but not frozen", etc. GameplayAbilities also have a big list of default uses.

![Abilities default tags](/res/blog/tags-on-abilities.png)
{:
	title="Abilities default tags"
}

One major issue I have so far is that cooldowns are tracked as GameplayEffects. While it makes sense, it also means that each new ability needs a new GameplayEffect for cooldown. I guess it makes sense, if you want to be able to do different things to different cooldowns, but as a programmer it seems clunky and cumbersome. Likely, I will try to setup a timer to handle cooldown in my subclass at some point in the future.