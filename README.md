# Evolutionary Prisoner's Dilemma

## Introduction

This is a project by Tristan Miller ([@tristanlmiller](https://github.com/tristanlmiller/)) from 2014.  I created a evolutionary simulation of the Iterated Prisoner's Dilemma.  I used Igor Pro, which was the language I was using in my work at the time.  The movies were generated later, for the purpose of this readme.

The **Prisoner's Dilemma** is an important concept in game theory, which captures the problem of altruism.  Each of the two players chooses to either cooperate or defect.  Cooperating incurs a personal cost, but benefits the other player.  If both players cooperate, then they are better off than if they had both defected.  In a single Prisoner's Dilemma, it seems that it's best to defect.  However, if there are multiple games played in succession, it's possible for players to punish defectors in subsequent games.  When multiple games are played in succession, it is called the **Iterated Prisoner's Dilemma** (IPD).

The best approach to the IPD is highly nontrivial.  In 2012, William Press and Freeman Dyson proved that there is <a href="http://www.pnas.org/content/109/26/10409.full">a class of "zero-determinant" strategies</a> that seem dominant, and which would lead to mostly defection.  However, Christoph Adami and Arend Hintze showed that the zero-determinant strategies are not dominant <a href="https://www.nature.com/articles/ncomms3193">in the context of evolution</a>.  Understanding this issue could elucidate why humans and other creatures appear to be altruistic.

## How the simulation works

1. We have a population of 40 individuals.  Each individual has 4 parameters that govern how they play IPD.
2. Each individual plays IPD against 2 other individuals in the population, and their fitness is calculated from their average score.
3. One individual dies, and another reproduces.  The probability of reproduction increases with fitness, and the probability of death decreases with fitness.
4. All the parameters of the individuals are mutated by small amounts.
5. Steps 2-4 are repeated a million times.  Each repetition is called a "generation".

## How the Iterated Prisoner's Dilemma Works

The Prisoner's Dilemma has the following payoff matrix:

<div align="center"><img src="/Images/Game-Theory-prisoners-dilemma.png" alt="Prisoner's Dilemma payoff matrix"><br>
<a href="http://blankonthemap.blogspot.com/2012/09/optimal-strategies-in-iterated.html">Image credit: Blank On The Map</a><br></div>

A simple strategy is to have a certain flat probability of cooperating.  However, in the Iterated Prisoner's Dilemma, this probability could depend on the results of all the earlier games.  The simplest case is when the probability depends *only* on the result of the previous game.  Since there are 4 possible results of each game, that means we need 4 probabilities, each between 0 and 1.  Thus, each individual has 4 parameters:
- Parameter 1 is the probability of cooperating if the last game was CC (all cooperated)
- Parameter 2 is the probability if the last game was CD (I cooperated, other player defected).
- Parameter 3 is the probability if the last game was DC (I defected, other player cooperated).
- Parameter 4 is the probability if the last game was DD (all defected).

The other question is, how many iterations do we play?  In fact, it is possible to calculate the average outcome over an *infinite* number of iterations, using Markov chains.  The method is described by Press & Dyson, and it is what I use in this simulation.  The catch is that none of the parameters can be exactly 0 or exactly 1, lest the method fail.

## Results

The evolutionary trajectory of the population is shown in the video linked below:

[![Evolutionary Prisoner's Dilemma](https://img.youtube.com/vi/q_vd2_Ww6rs/0.jpg)](http://www.youtube.com/watch?v=q_vd2_Ww6rs)

Each individual is represented by a colored pixel.  The location of the pixel represents the value of parameters 1 and 3.  Some pixels may represent multiple individuals at the same location.  The color of the pixel represents parameters 2 and 4, according to the color scale below:

<div align="center"><img src="/Images/colorscale.png" width=300></div>

As we can see from the movie, the population is highly unstable, and continues to change even after a million generations.  Below I identify several strategies that are similar to ones with common names.  There are also many strategies in the video that don't have any names that I know of.

<div align="center"><img src="/Images/Named strategies.png" width=500></div>


## Other games

I was worried that the simulation might be unstable simply because the mutation rate is set too high.  So I tried the simulation again, adjusting the payoff matrices so that it would use a different game.

First we have **Battle of the Sexes**.  In Battle of the sexes, a married couple is deciding what to do for the night.  One prefers to go to the football game, but his husband prefers to go to the opera.  However, whatever they choose to do, they both strongly prefer to stay together.  In this game, "cooperation" is going with the other player's preference, and "defection" is going with one's own preference.

Here are videos of two simulations of the Iterated Battle of the Sexes:

[![Evolutionary Battle of the Sexes](https://img.youtube.com/vi/AJMjYO4lw5c/0.jpg)](http://www.youtube.com/watch?v=AJMjYO4lw5c)

[![Evolutionary Battle of the Sexes, second sim](https://img.youtube.com/vi/zRdhymcQ2bI/0.jpg)](http://www.youtube.com/watch?v=zRdhymcQ2bI)

Each simulation appears to settle on a relatively stable equilibrium, but interestingly different simulations show different equilibria.  The first simulation shows a population that likes to take turns, while the second simulation shows a population that likes to hold on to dominance as long as possible.

Second we have **Stag Hunt**.  Two individuals go on a hunt.  Each can choose to go after a stag (cooperate) or after a hare (defect).  Going after the stag offers the biggest payoff, but only if both players choose to hunt the stag.  If only one player hunts a stag, then they fail to catch anything, while the other player catches a hare.

Here is the evolutionary trajectory of a population that plays Iterated Stag Hunt:

[![Evolutionary Stag Hunt](https://img.youtube.com/vi/YbkLpjByJO8/0.jpg)](http://www.youtube.com/watch?v=YbkLpjByJO8)

It seems that the population settles on hare hunting.  However, on repeated simulations, sometimes they settle on stag hunting.

All these movies are contained in the <a href="/Movies">movies folder</a>.  You may also see these results presented in a more traditional graph form in the <a href="/Images">images folder</a>.

## Conclusion

The Iterated Prisoner's Dilemma appears to lead to an evolutionary trajectory marked by instability.  This instability is particular to the Prisoner's Dilemma; similar simulations of Stag Hunt and Battle of the Sexes lead to more stable populations.

Of course, it's plausible that with different simulation settings and procedures, the population could eventually settle in a stable state.  This has been shown in <a href="http://dx.doi.org/10.1126/science.289.5485.1773">some of the literature</a>.  Creating this simulation gave me an appreciation for how difficult this problem is, and why it is the subject of an entire field of research.