# Muse AI Image Ecosystem

![Status](https://img.shields.io/badge/Status-v2.0.0-brightgreen?style=for-the-badge)
![Live](https://img.shields.io/badge/Live-GitHub_Pages-2ea44f?style=for-the-badge)

**A real working image generation workflow, built like a satellite station.**

**Live site:** https://git-fed.github.io/MuseAi-image-ecosystem/

**The working space:** Muse AI Image Ecosystem (Muse Space) — the pipeline there actually generates images. This repo is its GitHub Pages face: the same station, the same look, running in your browser.

---

## What it is

A 3D diorama: a tilted slab floating in a starfield viewport, six raised room blocks joined by conveyor streets to a red Deployment Bay pad at the centre. The default theme is Nebula (deep indigo, electric blue), with Emerald, Cyan, Amber, Violet and Rose in the THEME picker, recolours the whole scene, rooms included.

The agents hold still at rest: 12 named agents posted two per room, plus a two-person mini crew dormant at the benches in each room. Nothing moves until you press RUN PIPELINE. Then the Deployment Bay fires a flowing activation beam to each room in turn, each pair deploys through the bay, patrols its benches while working, then returns to post and the floor goes still again.

## The pipeline

| Room | What it does |
| --- | --- |
| Prompt Office | Takes your brief, subject, style, mood, format, detail level, keep-out list |
| Style Lab | Locks the look |
| Composition Bay | Builds the composition |
| Detail Forge | Refines the prompt, strips the flaws |
| Render Engine | Draws the image (the slow step, 15-45s) |
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

- **v2.0.0 — Nov 26, 2026:** Repo synced to the evolved 3D diorama build. Flat green map replaced by a tilted 3D slab in a starfield viewport with deeper raised rooms; default theme Nebula, picker with Nebula, Emerald, Cyan, Amber, Violet and Rose, recolours the whole scene. Every room holds its own two-person mini crew, dormant at rest, patrolling its benches while its stage works; the Deployment Bay fires a flowing activation beam to each room in turn. Room 4/6 fix carried over from the Space: stages renumbered to the true order (Detail Forge R04 before Render Engine R05), rooms read STAGED in cyan until their pair is genuinely working, Render row labelled the slow step. Also: ops stats bar from the session's run history, SURPRISE ME brief button, starrable vault images with full-screen lightbox, wider command-deck layout with bordered HUD panel, scan sweep while a run is live. Rest rule untouched: nothing moves until RUN PIPELINE is pressed.
- **v1.5.0 — Nov 26, 2026:** Agents do not move unless the pipeline is started. All 12 named agents hold still at their posts in their rooms while no job is running. The idle roaming tours are gone, the server issues no route to anyone outside a run, and IN MOTION reads 0/12 at rest. Street traffic, the conveyor belts, the gantry crane, and the idle bob on the crew dots are also held while idle. The page no longer runs a demo brief on its own. Movement only begins when you press RUN PIPELINE: each pair deploys through the bay, patrols its benches while working, then returns to its post and stops, and the floor goes still again until the next run. (Supersedes the idle-roam behaviour of v1.3.1-v1.4.3.)
- **v1.4.3 — Nov 26, 2026:** Fixed the invisible trails and the camouflaged crane at their causes. On a throttled phone the page rendered at only 9-20 frames per second, so the walk collapsed into choppy jumps; the breadcrumb trails were painted underneath the room boxes, so any trail dropped inside a room was invisible; and the gantry crane was the same dark green as the floor, so its travel could not be seen. The conveyor chevrons and background no longer repaint every frame, trails are now drawn on a single canvas above the rooms instead of churning DOM dots, and the crane got a brighter beam, a hazard-striped trolley, a drop cable with a lit hook and a pool of work light, on a faster loop. Frame rate rose to roughly 28-53fps under the same throttling, and a full run is a bit quicker, about 20 seconds.
- **v1.4.2 — Nov 26, 2026:** Fixed why the agents read as frozen on phones. The crew was animating through left/top layout updates, which collapse to a slideshow on phone GPUs, the first walk for some agents was delayed up to 4 seconds after load so fresh views caught them sitting in their room boxes, the breadcrumb trails switched off entirely on slow frames, and the gantry crane travelled hidden behind the room boxes. Now all 12 agents start walking within the first second, positions render on the GPU via transform, roam/patrol/travel speeds are up, trails stay visible (thinned, not disabled) on slow frames, the crane rides above the rooms with a lit trolley on a faster 26-second loop, the self-test run starts sooner and finishes quicker, and the status strip count now honestly reads CREW 12 and TRAFFIC n/18.
- **v1.4.1 — Nov 26, 2026:** Fixed the "sitting in one box" look at its cause. Every idle roam tour funneled through the single Deployment Bay centre point on near-identical timing, so the whole crew converged and lingered in the one bay box with overlapping labels, and heavy per-frame paint dropped a throttled phone viewport to about 17fps. Idle roam is now a perimeter tour of the conveyor streets with Dock B agents running it in reverse, a per-agent roam speed, and widely staggered start phases, so the crew stays spread around the whole floor. Deploys and returns now route through each agent's own bay slot instead of the one shared centre point. Breadcrumb-trail churn was cut so it cannot drag the frame rate down.
- **v1.4.0 — Nov 26, 2026:** Real continuous moving parts. Routes were issued one short hop at a time with 240-560ms pauses, which read as dots sitting still then jumping. Now the server issues each agent's whole tour as one chained route, at higher speeds, with near-zero pauses, so idle agents walk the full factory almost without stopping and a working pair patrols bench to bench for its whole stage. Walking is visible: agents bob at step pace, drop a fading dotted trail, and the status strip shows an IN MOTION counter for how many of the 12 are walking right now. The overhead gantry crane travels the floor, idle street traffic doubled, and if nobody starts a brief within 6 seconds the page runs one itself through the exact same pipeline, so the first thing you see is the factory working.
- **v1.3.2 — Nov 26, 2026:** Fixed the inverted agent behaviour. Stages used to advance on a fixed 2.1-second timer, but a deploy trip through the Deployment Bay takes up to 3.6 seconds, so every pair was recalled mid-journey and never reached its workstation, while idle agents roamed the whole factory. Now a stage never advances on a timer: it waits until its pair has actually arrived, then the pair spends a full 3 seconds visibly working, patrolling bench to bench across a wider loop at faster-than-roam speed, before the brief moves on. A 12-second watchdog means a run can never stall.
- **v1.3.1 — Nov 25, 2026:** Idle agents no longer sit in one box. Each pair now starts posted in its own home room, spread across all six rooms, and idle agents run a constant factory-wide tour: workstation, room corner, conveyor street, through the Deployment Bay, out to a far street, and back, at more than double the old roam speed. Starting a job no longer teleports everyone back into the bay; stages deploy via the bay, and finished pairs head back out on floor patrol. Status renamed AT POST.
- **v1.3.0 — Nov 25, 2026:** Factory upgrade. 3D raised room boxes, conveyor streets, hazard header, green industrial background. Agents rebuilt on server-owns-the-truth: the in-page server issues every agent's whole route (waypoints, departure, speed) for deploys, patrols, roam, and a matching return for every deploy. The map only renders, never moves an agent itself. Agents patrol while working, walk back when done, idle roam, and go OFFLINE grey with a last-seen time if their reports go stale. Live Ops and README say plainly the Page has no network server.
- **v1.2.0 — Nov 25, 2026:** Trees bug fixed. The painter only recognised 4 subjects and everything else fell through to pine trees. Now about 20 subject scenes (cat, dog, rocket, sailboat, car, train, castle, robot, dragon, bird, portrait, flowers, desert, snow, mountains, city, cottage, lighthouse, and more), trees only when the brief asks for a forest. New Photo Scout worker searches the Openverse archive for real openly licensed photos matching the brief, up to 4 per run, with credit and source link.
- **v1.1.0 — Nov 25, 2026:** Every agent is a someone. 12 named crew, 2 per room, each with a home dock, a callsign, a role, and a live task. Deployment Bay at the centre, crew stages in a spread 4x3 formation, tags readable on phone and desktop. Live Ops section: job, progress, heartbeat, timestamped deployment feed, Agent Inspector. 18 traffic dots labelled traffic only.
- **v1.0.0 — Nov 25, 2026:** First release. Satellite grid station, six pipeline rooms, agents that ramp from 4 slow dots at idle to 30 fast dots during a run, real end-to-end run on the page, Gallery Vault with PNG download.

---

Built by Muse3 for Git-FED. The old station lives at [Git-FED/MuseAi-ecosystem](https://github.com/Git-FED/MuseAi-ecosystem).
