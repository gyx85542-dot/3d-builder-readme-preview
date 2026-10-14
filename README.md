<p align="center">
  <img src="assets/logo.png" alt="Topview 3D Builder" width="96">
</p>

<h1 align="center">Topview 3D Builder</h1>

<p align="center"><b>Block the scene in 3D. Let AI shoot the video.</b></p>

<p align="center">
  <a href="https://pypi.org/project/topview-3d-cli/"><img src="https://img.shields.io/pypi/v/topview-3d-cli.svg?style=flat" alt="PyPI version"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License: Apache 2.0"></a>
  <a href="https://www.python.org"><img src="https://img.shields.io/badge/python-%3E%3D3.11-3776AB" alt="Python 3.11+"></a>
  <a href="https://nodejs.org"><img src="https://img.shields.io/badge/node-%3E%3D20.6-brightgreen" alt="Node.js 20.6+"></a>
</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> ·
  <a href="#what-you-can-make">Examples</a> ·
  <a href="docs/topview-3d-cli.md">CLI Reference</a> ·
  <a href="https://www.topview.ai/3d-builder">Website</a>
</p>

<p align="center">
  <!--
    HERO — docs/assets/hero.mp4 (main) + docs/assets/hero.gif (fallback)
    What: one continuous take of the local Studio, no terminal.
      0–5s   build the set: drag a character and a table in, apply a seated pose
      5–10s  place the camera: add a camera, switch the viewport to it, nudge the framing
      10–16s direct the move: drop a "push in" move on the timeline, drag its length,
             the clips after it slide along; scrub the playhead
      16–22s render: reference frames / contact sheet appear, last second cuts to the final AI video
    Size: record at 1600×1000, show at 800 px wide. Dark theme, slowed cursor.
    Length: 18–25 s, seamless loop. MP4 (H.264) ≤ 10 MB; GIF ≤ 10 MB, 15 fps.
    GitHub strips relative <video> tags. Inline playback needs a user-attachments URL.
  -->
  <video src="https://github.com/user-attachments/assets/5b07a0d4-d3cc-48c0-aebf-31e2232d90de" width="800" autoplay loop muted playsinline controls></video>
</p>

Topview 3D Builder is a 3D director's stage that runs on your machine. You, or
your coding agent, place characters, poses, props and cameras, plan the camera
moves on a timeline, and render reference frames. A video model then shoots to
that plan, so framing and blocking come from you instead of from luck. Scenes
live in a project folder and stay editable. Building and rendering need no
account and upload nothing.

## Quick Start

**1. Add the plugin to your agent**

```bash
claude plugin marketplace add topviewai/topview-3d-builder
claude plugin install topview-3d-builder@topview-3d-builder
```

<details>
<summary>Codex / ChatGPT, Cursor, other agents</summary>

**Codex CLI and the ChatGPT desktop app** (they share `~/.codex`; restart the app afterwards)

```bash
codex plugin marketplace add https://github.com/topviewai/topview-3d-builder.git --ref main
codex plugin add topview-3d-builder@topview-3d-builder
```

**Cursor** (restart Cursor afterwards)

```bash
git clone https://github.com/topviewai/topview-3d-builder.git ~/.cursor/plugins/local/topview-3d-builder
```

**Any agent with skills support**

```bash
npx skills add topviewai/topview-3d-builder
```

Then pick `topview-3d-cli`.

</details>

You'll need Python 3.11+, Node.js 20.6+, and either uv or pipx.

**2. Ask for a shot**

Start a new session and try:

> Build a small café. Two people sit across a table from each other. Put the camera outside the window and slowly push in over four seconds. Render the first, middle and last frame.

**3. Open it in Studio and keep going**

```bash
topview-3d-cli studio open my-scene
```

This prints a local URL (port 3002 by default). Open it to move things around,
retime the camera, and render again.

## What you can make

<!--
  EXAMPLES — four pairs, each: docs/assets/examples/<name>-scene.png + <name>-video.gif
  Left: the 3D blocking in Studio (1200×675 PNG). Right: the AI video made from it (600 px GIF, 3–5 s, ≤ 4 MB).
  Same camera angle on both sides so the match is obvious.
-->
<table>
  <tr>
    <td width="50%" align="center"><img src="docs/assets/examples/dialogue-scene.png" alt="Two-person dialogue, 3D blocking" width="100%"><br><b>Dialogue</b> · over-the-shoulder coverage</td>
    <td width="50%" align="center"><img src="docs/assets/examples/dialogue-video.gif" alt="Two-person dialogue, generated video" width="100%"><br>The generated shot</td>
  </tr>
  <tr>
    <td width="50%" align="center"><img src="docs/assets/examples/product-scene.png" alt="Product on a table, 3D blocking" width="100%"><br><b>Product</b> · orbit around an object</td>
    <td width="50%" align="center"><img src="docs/assets/examples/product-video.gif" alt="Product orbit, generated video" width="100%"><br>The generated shot</td>
  </tr>
  <tr>
    <td width="50%" align="center"><img src="docs/assets/examples/action-scene.png" alt="Running figure, 3D blocking" width="100%"><br><b>Movement</b> · tracking a character</td>
    <td width="50%" align="center"><img src="docs/assets/examples/action-video.gif" alt="Tracking shot, generated video" width="100%"><br>The generated shot</td>
  </tr>
  <tr>
    <td width="50%" align="center"><img src="docs/assets/examples/establishing-scene.png" alt="Wide room, 3D blocking" width="100%"><br><b>Establishing</b> · slow zoom out</td>
    <td width="50%" align="center"><img src="docs/assets/examples/establishing-video.gif" alt="Zoom out, generated video" width="100%"><br>The generated shot</td>
  </tr>
</table>

More prompts to start from:

> A woman stands in a white studio holding a pose from the "walking" set. Three cameras: front, three-quarter, and a low angle. Render all three.

> Put a car in the middle of an empty street. Orbit the camera 90 degrees around it over five seconds.

> Take my current scene, add a second camera behind the main character, and cut to it halfway through.

## How it works

<!--
  DIAGRAM — docs/assets/how-it-works.svg (optional; the text list below works without it)
  Five boxes left to right: Your prompt → Agent + skill → Scene folder (.topview-3d/) → Studio / Renderer → Video model.
  1600×400, SVG or PNG, light and dark versions if possible.
-->

1. **You describe the shot.** Your agent reads the bundled skill and turns the request into scene edits.
2. **The scene is built locally.** `topview-3d-cli` writes it to `.topview-3d/` in your project folder, using built-in characters, poses and props.
3. **It checks its own work.** Framing and coverage are measured per camera before anything is rendered.
4. **Frames are rendered on your machine.** A headless browser renders each camera into PNG frames and a contact sheet.
5. **You refine in Studio.** Drag, retime, re-render. The agent picks up your edits on the next turn.

## Why a 3D stage first

- **Direct, don't gamble.** Composition, eyelines and camera paths are decided before the video model runs.
- **Edit, don't regenerate.** The scene is a file, not a prompt. Move one prop and render again.
- **Local by default.** No account, no upload, until you choose to send a render out.
- **Agent-native.** Works in Claude Code, Codex, the ChatGPT desktop app and Cursor.

## Topview Canvas

3D Builder makes the plan. [Topview Canvas](https://www.topview.ai) <!-- TODO: confirm the public Canvas URL --> turns it into video.
From Studio you can send a finished render to a Canvas, where the frames guide
generation. This is the only step that asks you to sign in to Topview.
Everything before it works offline.

## Documentation

- [CLI reference and project format](docs/topview-3d-cli.md)
- [Contributing, development setup and releases](CONTRIBUTING.md)
- Questions and bugs: [GitHub Issues](https://github.com/topviewai/topview-3d-builder/issues)

## License

Code, schemas and docs are [Apache 2.0](LICENSE). The built-in characters, poses
and primitives in `builtin-assets/` are [CC BY 4.0](builtin-assets/LICENSE) —
credit them as "Scene3D built-in assets © Topview, CC BY 4.0"
(see [NOTICE](builtin-assets/NOTICE)).
