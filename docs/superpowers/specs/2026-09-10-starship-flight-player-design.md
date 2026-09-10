# Starship Flight Player - design spec

Date: 2026-09-10
Status: built autonomously; design decisions below were made without a
clarifying dialogue because the session ran unattended.

## Purpose

An interactive, single-page learning tool that shows how a SpaceX Starship
launch works from countdown to landing, and explains the technologies that
make it possible (Raptor engines, methalox, stainless steel, hot staging,
grid fins and the tower catch, the heat shield, flaps, header tanks, the
payload dispenser, orbital refilling).

Audience: one curious learner with a technical background but no rocketry
background. The page's single job: let them scrub through a flight and, at
every moment, see what the vehicle is doing and why.

## Approaches considered

1. Single self-contained HTML page, vanilla JS, inline SVG scene, keyframed
   trajectory data, published as an Artifact. Chosen: no build step, works
   inside the Artifact sandbox, easy to update, fully offline.
2. Three.js 3D scene from cdnjs. Rejected: no vehicle models available,
   heavy, and a schematic 2D side view explains phases better than an
   untextured 3D cylinder.
3. React app via CDN with a component per view. Rejected: framework weight
   with no benefit for a single-user learning page.

## Content basis

Vehicle: Starship V3 (Block 3), the current generation. Flown on Flight 12
(May 22, 2026) and Flight 13 (Jul 24, 2026). Flight 14 is expected NET
Sep 15, 2026.

Timeline: a composite "nominal" profile using the event times of Flights
11 and 13 (public SpaceX timelines). Altitude and speed curves are
approximations of webcast telemetry and are labelled as such. The booster
is shown ending in a tower catch, which was demonstrated on Flights 5, 7
and 8; V3 test flights so far ended with Gulf splashdowns, and the copy
says so.

## Views

- Flight: the player. Scene (SVG) showing the stack, then split cameras
  for booster and ship after staging. Phase panel with description,
  telemetry tiles, and the technologies active in that phase. Timeline
  scrubber with event markers, play/pause, speed, step to next/previous
  event. Altitude and speed small-multiple charts with a playhead.
- Vehicle: labelled side-view anatomy of the 124 m stack with a scale
  comparison, click a label to read about the part.
- Technology: cards for each key technology, including an FFSC cycle
  diagram for Raptor.
- Flight log: table of Flights 1 to 13 plus the planned Flight 14.

## Design plan

Colour: cool steel neutrals (dark ground #11161c, light ground #eef1f4),
Raptor-blue accent, ship series blue #2a78d6/#3987e5 and booster series
orange #eb6834/#d95926 (dataviz reference slots 1 and 2), plasma orange
reserved for reentry heat.
Type: Barlow Condensed for headings and the T+ clock, Barlow for body,
JetBrains Mono for telemetry digits.
Layout: app-style. Sticky header with view tabs; Flight view is a
two-column scene plus panel that stacks at phone width; timeline and
charts below the scene.

## Out of scope

Live telemetry, 3D rendering, user accounts, saved progress beyond the
last tab and playback speed (localStorage only).
