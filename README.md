A small web tool that tells you whether your race goal is realistic, and what pace you need to run to hit it.

Live version: https://anugrahasn1.github.io/race-pace-planner/

## Why I made it

Most pace calculators just divide your goal time by the distance. That answers "what pace do I need?" but not the more useful question: can I actually run that pace right now?

I wanted something that starts from a race you've already run, predicts what you can do at the new distance, and then tells you honestly if your goal is a stretch.

## What it does

You enter a recent race (distance and time) and the race you're aiming for (distance and goal time). The tool then:

- predicts your finish time for the goal race
- compares your goal with that prediction and labels it realistic, ambitious or unlikely
- if the goal is unlikely, tells you what recent race time you'd need first
- gives you a pace band: the time you should see on your watch at every kilometre

The pace band has two options. Even pace is the same speed all the way. Negative split has you run the first half 1% slower and the second half 1% faster, which finishes in the same time but stops you from going out too fast.

## The maths

The prediction uses Riegel's formula, which is the standard way of converting a race time from one distance to another:

```
T2 = T1 × (D2 / D1) ^ 1.06
```

T1 and D1 are your recent race time and distance, D2 is the goal distance. The 1.06 exponent is there because you can't hold the same pace for longer.

I set the verdict thresholds like this:

| Goal vs prediction | Verdict |
|---|---|
| same or slower | realistic |
| up to 3% faster | ambitious |
| more than 3% faster | unlikely |

The 3% cut-off is my own judgement call, not a scientific rule. It felt like a fair line between "possible with a good day and good training" and "not yet".

## Example

25:00 for 5K, aiming for a 1:52:00 half marathon:

- predicted time: 1:55:00
- goal is 2.6% faster, so: ambitious
- negative split plan: around 5:22/km for the first half, then 5:15/km

## What it doesn't do

It assumes a flat course and normal weather. It doesn't know anything about your training, so a 5K time from someone who has never run longer than 10K will give an optimistic marathon prediction. The further apart the two distances are, the less you should trust the result.

## What I'd add next

- check how accurate the predictions really are, using public marathon results with split times
- adjust for hills and heat
- import past races from Strava instead of typing them in

## Running it locally

It's a single `index.html` file with plain HTML, CSS and JavaScript. Download it and open it in a browser. There's nothing to install.
 README (1).md…]()
