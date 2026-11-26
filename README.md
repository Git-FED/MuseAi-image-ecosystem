# Muse AI Image Ecosystem

![Status](https://img.shields.io/badge/Status-v1.3.2-brightgreen?style=for-the-badge)
![Live](https://img.shields.io/badge/Live-GitHub_Pages-2ea44f?style=for-the-badge)

**A real working image generation workflow, built like a satellite station.**

**Live site:** https://git-fed.github.io/MuseAi-image-ecosystem/

**The working space:** Muse AI Image Ecosystem (Muse Space) — the pipeline there actually generates images. This repo is its GitHub Pages face: the same station, the same look, running in your browser.

---

## What it is

Top-down satellite view on a dark green grid. Six room blocks joined by streets to a red relay hub. Little agent dots moving room to room like busy traffic.

The agents are quiet at rest: only 4 dots, drifting slow. When you set a pipeline, they wake up. More dots join, they move faster, stage by stage, as the brief travels through the rooms, then they settle back to idle when the run finishes.

## The pipeline

| Room | What it does |
| --- | --- |
| Prompt Office | Takes your brief, subject, style, mood, format, detail level, keep-out list |
| Style Lab | Locks the look |
| Composition Bay | Builds the composition |
| Render Engine | Draws the image |
| Detail Forge | Refines it |
| Gallery Vault | Keeps it, downloadable as a PNG, with the exact prompts it built |

Write a brief, hit Run Pipeline, watch the rooms light up in order, get an image at the end.

## How it works

- **In the Space:** the pipeline expands your brief into a full prompt, refines it, and generates a real image that lands in the Gallery Vault. Download it, view the exact prompts, remix the brief, retry a failed run, or delete it.
- **On this Page:** the same station and the same pipeline flow, with the Render Engine drawing the image live on a canvas in your browser. The full server generation lives in the Space.

## Files

- `index.html` — the whole station, one file
- `404.html` — the lost-room page
- `.nojekyll` — Pages serves the site as-is

## History

- **v1.3.2 — Nov 26, 2026:** Fixed the inverted agent behaviour. Stages used to advance on a fixed 2.1-second timer, but a deploy trip through the Deployment Bay takes up to 3.6 seconds, so every pair was recalled mid-journey and never reached its workstation, while idle agents roamed the whole factory. Now a stage never advances on a timer: it waits until its pair has actually arrived, then the pair spends a full 3 seconds visibly working, patrolling bench to bench across a wider loop at faster-than-roam speed, before the brief moves on. A 12-second watchdog means a run can never stall.
- **v1.3.1 — Nov 25, 2026:** Idle agents no longer sit in one box. Each pair now starts posted in its own home room, spread across all six rooms, and idle agents run a constant factory-wide tour: workstation, room corner, conveyor street, through the Deployment Bay, out to a far street, and back, at more than double the old roam speed. Starting a job no longer teleports everyone back into the bay; stages deploy via the bay, and finished pairs head back out on floor patrol. Status renamed AT POST.
- **v1.3.0 — Nov 25, 2026:** Factory upgrade. 3D raised room boxes, conveyor streets, hazard header, green industrial background. Agents rebuilt on server-owns-the-truth: the in-page server issues every agent's whole route (waypoints, departure, speed) for deploys, patrols, roam, and a matching return for every deploy. The map only renders, never moves an agent itself. Agents patrol while working, walk back when done, idle roam, and go OFFLINE grey with a last-seen time if their reports go stale. Live Ops and README say plainly the Page has no network server.
- **v1.2.0 — Nov 25, 2026:** Trees bug fixed. The painter only recognised 4 subjects and everything else fell through to pine trees. Now about 20 subject scenes (cat, dog, rocket, sailboat, car, train, castle, robot, dragon, bird, portrait, flowers, desert, snow, mountains, city, cottage, lighthouse, and more), trees only when the brief asks for a forest. New Photo Scout worker searches the Openverse archive for real openly licensed photos matching the brief, up to 4 per run, with credit and source link.
- **v1.1.0 — Nov 25, 2026:** Every agent is a someone. 12 named crew, 2 per room, each with a home dock, a callsign, a role, and a live task. Deployment Bay at the centre, crew stages in a spread 4x3 formation, tags readable on phone and desktop. Live Ops section: job, progress, heartbeat, timestamped deployment feed, Agent Inspector. 18 traffic dots labelled traffic only.
- **v1.0.0 — Nov 25, 2026:** First release. Satellite grid station, six pipeline rooms, agents that ramp from 4 slow dots at idle to 30 fast dots during a run, real end-to-end run on the page, Gallery Vault with PNG download.

---

Built by Muse3 for Git-FED. The old station lives at [Git-FED/MuseAi-ecosystem](https://github.com/Git-FED/MuseAi-ecosystem).
