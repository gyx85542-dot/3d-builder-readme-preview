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

<!--
  HERO — docs/assets/hero.mp4 (main) + docs/assets/hero.gif (fallback)
  GitHub only plays a user-attachments URL when that URL is its own paragraph.
-->

https://github.com/user-attachments/assets/5b07a0d4-d3cc-48c0-aebf-31e2232d90de

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
  EXAMPLES — left is the 3D blocking, right is the generated shot.
  GitHub only plays a user-attachments URL, so these cells use those URLs.
-->
<table>
  <tr>
    <td width="50%" align="center"><video src="https://github.com/user-attachments/assets/5a12c45a-a5d0-4fe8-a5d9-40689fd62988" width="100%" controls muted playsinline></video><br>prompt：Build a café counter. One person stands behind it and pours from a pitcher into a cup. Put the camera across the counter, close on the pour, and hold for eight seconds.</td>
    <td width="50%" align="center"><video src="https://github.com/user-attachments/assets/d20f2c9a-8fc2-45c7-b7cc-249a4a6b1e8c" width="100%" controls muted playsinline></video><br>The generated shot</td>
  </tr>
  <tr>
    <td width="50%" align="center"><video src="https://github.com/user-attachments/assets/a49d606b-b480-4846-a60c-59044c93c1f7" width="100%" controls muted playsinline></video><br>prompt：Put a basketball hoop at the end of a court. A player jumps and reaches the ball up toward the rim. Place the camera low and to the side so the player and the hoop both stay in frame, and hold for eight seconds.</td>
    <td width="50%" align="center"><video src="https://github.com/user-attachments/assets/6a3afbde-32f2-4274-8f25-c7f8b93bcca5" width="100%" controls muted playsinline></video><br>The generated shot</td>
  </tr>
  <tr>
    <td width="50%" align="center"><video src="https://github.com/user-attachments/assets/3616a492-1961-4760-ab3e-259c603b292c" width="100%" controls muted playsinline></video><br>prompt：A person rides a bicycle down a city street, with buildings and trees on either side. Place the camera level with the rider and track alongside them for eight seconds.</td>
    <td width="50%" align="center"><video src="https://github.com/user-attachments/assets/8db00ea9-9b6b-414e-a76b-9b92761504f6" width="100%" controls muted playsinline></video><br>The generated shot</td>
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
