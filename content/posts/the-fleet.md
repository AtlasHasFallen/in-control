---
title: "The Fleet"
date: 2026-04-21
draft: true
tags: ["3d-printing", "intro"]
description: "Six 3D printers. One unfinished. A process engineer asks the obvious question a little too late."
ShowToc: false
math: false
---

It started with one printer. It always starts with one printer.

What nobody tells you when you buy your first 3D printer is how many settings it has. Temperature, speed, layer height, retraction distance, cooling, infill — each one a dial you're expected to tune by feel, guided by forum posts from strangers who may or may not have the same filament, the same room temperature, or the same definition of "good enough."

![All those settings](/in-control/images/Slicer_overwhelm.svg)

I am a process engineer.I build statistical models for manufacturing processes. I did not notice the irony of this for several years.

By the time I noticed, I had accumulated a Prusa I built from a kit, two resin printers, a partially assembled Ender 3 that lives in the workshop graveyard, and two Bambu machines. Six printers. Hundreds of prints. Thousands of data points collected by accident and ignored on purpose.

The current workhorse is the Bambu P1S — enclosed, reliable, consistent. Every print generates a record of its parameters. I have never seriously analyzed one.

Here's the question I should have asked years ago: what would it look like to treat this like a process? Not forum-post engineering — actual designed experiments, actual models, actual predictions. Can I build something that tells me, from process parameters alone, whether a print will succeed before it fails?

That's what this blog is for. We'll find out.
