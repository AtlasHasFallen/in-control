---
title: "The Fleet"
date: 2026-04-21
draft: false
tags: ["3d-printing", "intro"]
description: "Six 3D printers. One unfinished. A process engineer asks the obvious question a little too late."
ShowToc: false
math: false
---

It started with one printer. It always starts with one printer.

What nobody tells you when you buy your first 3D printer is how many settings it has. Temperature, speed, layer height, retraction distance, cooling, infill density, infill pattern — each one a dial you're expected to tune by feel, guided by forum posts from strangers who may or may not have the same filament, the same room temperature, or the same definition of "good enough."

I am a process engineer. I build statistical models for manufacturing processes. I did not notice the irony of this for several years.

## The Fleet

**Prusa MK-series** — built from a kit, which taught me a great deal about how these machines actually work. It has a temperature issue with the extruder I haven't resolved. Something in the process is drifting. I know this because the prints tell me. I have not gone further than that.

**Elegoo Mars** — resin. A completely different process: photopolymer cured layer by layer by UV light in a vat of something you probably shouldn't breathe. Fewer tunable parameters than FDM, but the ones that matter — exposure time, lift speed, layer thickness — matter a lot. I found the right settings eventually. I couldn't tell you exactly why they're right.

**Ender 3** — the Prusa build went well enough that I thought: sure, another one. The Ender 3 now lives in my workshop in a state I'll generously describe as "in progress." The workshop is very patient.

**Elegoo Saturn** — larger resin printer. Same process as the Mars, bigger build volume, more things to calibrate. More prints I'm happy with. Still no formal understanding of why.

**Bambu X1C** — fast, enclosed, multi-material capable, and packed with sensors. It logs temperatures, flow rates, vibration signatures. It has a mechanical extruder issue I haven't diagnosed. Somewhere in that data is probably the answer. I have not looked.

**Bambu P1S** — the current workhorse. Enclosed, reliable, consistent. Every print generates a record of its parameters. I have never seriously analyzed one.

---

Six printers. Hundreds of prints. Thousands of data points I've collected by accident and ignored on purpose.

Here's the question I should have asked years ago: what would it look like to treat this like a process? Not forum-post engineering — actual designed experiments, actual models, actual predictions. Can I build something that tells me, from process parameters alone, whether a print will succeed before it fails?

The P1S is the testbed. That's what this blog is for. We'll find out.
