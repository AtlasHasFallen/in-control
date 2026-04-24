---
title: "The Confounder"
date: 2026-04-22
draft: false
tags: ["3d-printing", "doe", "measurement"]
description: "Before you can model a process, you have to decide what you're measuring — and why it's harder than it sounds."
ShowToc: true
math: false
---

If I want to understand the printer, I need a test model — one I can print over and over, under different conditions, and actually measure. I could pick something off a model-sharing site. There are plenty of calibration prints out there. But let's make it hard on ourselves: I want to think about what I need to measure first, then design a model that captures exactly that. A test piece built around the data, not the other way around.

Also, the more I can *measure* the model, the better I can model the process. That part will make sense later.

## First Principles

What does a good print actually mean? Let's start there before touching any CAD software.

We want dimensional accuracy — the part should be the size we designed it to be. We want smooth surfaces and clean overhangs. We do not want stringing. We want it to stay on the bed. We want it to be strong.

That is not a complete list. It is a good-enough list to start, and starting is the point.

## What Are We Actually Measuring?

Here is where it gets interesting. A process engineer's instinct is to want numbers — clean, continuous measurements you can feed into a model without argument. Some of what we care about cooperates. Some of it does not.

### The Easy Ones

Dimensional accuracy is straightforward: print a known geometry, put calipers on it, record the deviation[^1]. Length, width, height. Hole diameters. Cylinder diameters. Wall thicknesses. Part mass. These are all continuous measurements with a well-defined ground truth and no interpretation required.

Mass deserves special mention. It is the cheapest measurement on the list — a kitchen scale — and it catches things calipers miss entirely. Under-extrusion produces a part with the right external shape but less material inside. The dimensions look fine. The mass is low. If your model only uses calipers, it never sees this failure mode.

### The hard ones

Stringing and overhang quality are a different problem. They are real, they matter, and they do not have a clean continuous measurement. A bridging test can be measured — how far did the span sag, in millimeters? That is a number. But stringing is fundamentally a visual assessment. How many strands? How thick? How bad?

The honest answer is: we use an ordinal scale. Rate it 1 to 5 against a reference set of photos. This is not as satisfying as a caliper measurement. It is also not optional — the alternative is pretending stringing does not exist because it is inconvenient to quantify.

The same logic applies to overhang quality. At some angle, overhangs start to droop. The exact angle depends on the material, the cooling, and a dozen other things. We can test multiple angles on the same print and rate the quality at each one. Ordinal, but structured.

Which brings us to a chicken-and-egg problem: the reference photos need to show a range from good to bad — but you do not know what your good and bad look like until you have printed some parts.

The solution is to not pretend otherwise. Print all the runs first, then rate them.[^2] Physically sort the prints by quality on each visual criterion — stringing pile, overhang pile — and assign ratings by rank. Bottom quintile gets a 1, top quintile gets a 5. The scale is anchored to the actual range your printer produced, not to a hypothetical reference set borrowed from someone else's machine, filament, and conditions.

The one rule: rate blind. Cover the run labels before scoring. You want to evaluate the print, not confirm your expectations about which settings should win. Rescaling after the fact is fine — as long as you do it before you open the model. Rescaling after seeing the residuals is a different thing entirely.

### The confound we are keeping

One more thing worth being upfront about: the cylinders on this model are the same height as the freestanding walls nearby. Stringing tends to occur between any two features at similar heights. That means stringing scores and cylinder diameter measurements are not fully independent — a setting that reduces stringing might also change how the cylinders print, and vice versa.

This is a known confound. We are keeping it because the goal is not to isolate every effect cleanly — that is what a controlled experiment with one feature at a time is for. The goal is to build a model that reflects how the printer actually behaves, where everything is happening at once. Acknowledging the confound is the first step to accounting for it.

### The full list

After working through all of this, the measurement plan looks like this:

| Feature | What we measure | Type |
|---|---|---|
| Reference cube | X, Y, Z external dimensions | Continuous (mm) |
| Top face hole | Diameter | Continuous (mm) |
| Side face hole | Diameter | Continuous (mm) |
| Cylinders (3 sizes) | Achieved diameter × 3 | Continuous (mm) |
| Wall fins (3 thicknesses) | Achieved thickness × 3 | Continuous (mm) |
| Bridge spans (3–4 lengths) | Sag at center × each span | Continuous (mm) |
| Arch overhangs (4 angles) | Quality rating at each angle | Ordinal 1–5 |
| Stringing | Overall severity | Ordinal 1–5 |
| Part mass | Grams | Continuous |

Eighteen responses. In most industrial DOE work, you'd have one or two. Here, the number is the point — more on that when we get to the modeling.

## The Model

This is The Confounder. Someone else could have looked at the same list of requirements and built something completely different — a different geometry, different feature sizes, different tradeoffs. This is one valid answer to the problem, not the only one.

{{< figure src="/in-control/images/the-confounder-annotated.png" alt="The Confounder test piece with numbered feature callouts" caption="The Confounder — annotated isometric view." >}}

| # | Feature | What it tests | Measurements |
|---|---|---|---|
| 1 | Reference cube | Overall dimensional accuracy | X, Y, Z external dims (mm) |
| 2 | Cylinders (4 / 6 / 8 mm) | Fine dimensional accuracy + stringing between features | Achieved diameter × 3 (mm) |
| 3 | Wall fins | Thin wall resolution | Achieved thickness × 3 (mm) |
| 4 | Bridge spans | Bridging performance at increasing lengths | Sag at span center × 3 (mm) |
| 5 | Arch | Overhang quality at 30°, 45°, 60°, 75° | Quality rating × 4 angles (1–5) |
| 6 | Top face hole | XY plane dimensional accuracy | Hole diameter (mm) |
| 7 | Side face hole | Z-axis dimensional accuracy | Hole diameter (mm) |
| — | Part (whole) | Material deposition — catches under-extrusion that calipers miss | Mass (g) |

[^1]: One can argue about the measurement method, but the many like calipers.
[^2]: Rating blind against your own ranked prints is how sensory evaluation panels handle this in food science and pharmaceuticals. It is more defensible than borrowing someone else's reference set, not less.