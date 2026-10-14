<p align="center">
  <img src="logo.png" alt="Topview 3D Builder" width="120" />
</p>

<h1 align="center">Topview 3D Builder</h1>

<p align="center"><b>Block it in 3D. Let AI shoot it.</b></p>

<p align="center">
  From an idea, to a 3D scene, to a real animated video. Free, runs locally, no sign-up.
</p>

<p align="center">
  <a href="https://github.com/topviewai/topview-3d-builder/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License: Apache 2.0"></a>
  <a href="https://www.python.org"><img src="https://img.shields.io/badge/python-%3E%3D3.11-3776AB" alt="Python 3.11+"></a>
  <a href="https://nodejs.org"><img src="https://img.shields.io/badge/node-%3E%3D20.6-brightgreen" alt="Node.js 20.6+"></a>
  <img src="https://img.shields.io/badge/runs-100%25%20local-success" alt="Runs 100% local">
</p>

<p align="center">
  <a href="#quick-start">Quick Start</a> |
  <a href="#see-what-you-can-make">Examples</a> |
  <a href="https://www.topview.ai/academy/spatial-control#3-1-3d-builder-build-scenes-stage-action-and-move-the-camera">Tutorial</a> |
  <a href="https://www.topview.ai/3d-builder">3D Builder</a> |
  <a href="https://www.topview.ai">Topview.ai</a> |
  <a href="https://github.com/topviewai/topview-3d-builder/issues">Issues</a>
</p>

https://github.com/user-attachments/assets/5b07a0d4-d3cc-48c0-aebf-31e2232d90de

<p align="center"><sub>Build the scene, place the cameras, plan the camera move in Studio, then get the shot.</sub></p>

## Quick Start

Works with **ChatGPT / Codex**, **Cursor** and **Claude Code**. You need Python 3.11+, Node.js 20.6+, and either [uv](https://docs.astral.sh/uv/) or pipx.

**1. Send this to your agent**

```text
Install the Topview 3D Builder plugin from https://github.com/topviewai/topview-3d-builder for the agent I'm using (ChatGPT / Codex, Cursor or Claude Code). Follow the install steps in the README, then tell me when to restart.
```

<details>
<summary>What your agent will run</summary>

**ChatGPT / Codex** (the ChatGPT desktop app shares Codex's configuration; restart the app afterwards)

```bash
codex plugin marketplace add https://github.com/topviewai/topview-3d-builder.git --ref main
codex plugin add topview-3d-builder@topview-3d-builder
```

**Cursor** (restart Cursor afterwards)

```bash
git clone https://github.com/topviewai/topview-3d-builder.git ~/.cursor/plugins/local/topview-3d-builder
```

**Claude Code** (restart Claude Code afterwards)

```bash
claude plugin marketplace add https://github.com/topviewai/topview-3d-builder.git
claude plugin install topview-3d-builder@topview-3d-builder
```

**Any other agent with skills support**

```bash
npx skills add https://github.com/topviewai/topview-3d-builder.git
```

Then pick `topview-3d-cli`. The first render downloads a browser component once; after that it is cached. For updates, uninstalling and manual setup, see the [developer docs](DEVELOPER.md).

</details>

**2. Start a new session and describe the scene you want**

> Build a scene: a character sits next to a box. Render a front view.

**3. Review the scene and keep refining**

Keep talking to your agent, or open Studio and adjust by hand. When you're happy, turn the 3D scene into a real animated video.

## The problem

AI video is great until you try to direct it. With text alone, space is hard to describe:

- 😵 **Blocking is a guess.** "Two people facing each other across a table" comes back side by side, clipping, or without the table.
- 🎰 **Camera angles are a lottery.** Reverse shots, over-the-shoulder, top-down: you write a paragraph and get one random angle.
- 🔁 **One tweak, full redo.** Move a character half a step and everything changes on regenerate.
- 💸 **Retries burn credits.** A usable shot can take a dozen attempts.
- 🧩 **Shots don't match.** In one scene, character positions and space contradict each other from shot to shot.
- 📐 **Not everyone can storyboard.** No art skills means no way to show the staging in your head.

## The idea

> **Turn space you can't describe into a 3D scene you can see, then into a real video.**

Topview 3D Builder covers the whole path from **an idea, to a 3D scene, to a real video**:

1. **Idea → 3D scene.** Say the picture in your head. Your agent builds it: who stands where, who faces what, what they hold, and where the camera sits.
2. **3D scene → locked staging.** Blocking, scale and camera angles, the things AI gets wrong most often, are fixed before generation.
3. **3D scene → real video.** The scene guides generation into an animated video with real-world look and feel. Texture, lighting and performance come from the video model; the staging is yours.

```
An idea  →  Agent builds the 3D scene  →  Auto-check and refine  →  Multi-camera render  →  Real animated video
```

## What you get

- 🎬 **Direct, don't gamble.** You decide blocking, facing, poses, props and cameras. Render several cameras from one scene and the **characters and space stay consistent across every shot**.
- 🎥 **Design the camera move in advance.** Plan push-ins, pull-backs, rises, orbits and cuts on a timeline. Stretch or shorten a move and the clips after it shift automatically.
- 💬 **Just describe it.** No 3D software to learn. Ask in plain language, for example: *"Two people sit across a table, a woman is talking. Give me a front, an over-the-shoulder and a top-down shot."*
- ✅ **Checked before you generate.** Floating or clipping characters, spacing, framing and composition are measured automatically, so problems are caught before they cost you credits.
- ✏️ **Edit one thing, keep the rest.** Scenes are saved as projects. Move a character, change a pose or add a camera without starting over, or drag things around in the built-in Studio.
- 🔒 **Local by default.** Building and rendering run on your machine, with no account and no upload.

## See what you can make

Left is the 3D scene you build. Right is the video generated from it: **the way you stage it in 3D is the way it gets shot.**

<table>
  <tr>
    <th width="50%" align="center">3D scene</th>
    <th width="50%" align="center">Generated video</th>
  </tr>
  <tr>
    <td align="center"><video src="https://github.com/user-attachments/assets/f304c401-a009-470c-ba7b-1fba10ea3a14" width="100%" controls muted playsinline></video></td>
    <td align="center"><video src="https://github.com/user-attachments/assets/3365923a-a8b4-4c78-aeaa-2d32b6c22320" width="100%" controls muted playsinline></video></td>
  </tr>
  <tr>
    <td colspan="2"><b>🐉 Establishing shot, follow the flight:</b> A rider flies a dragon over a castle. The camera starts just behind and above them, looking forward over the wings at the towers. Over eight seconds it follows the flight as the dragon clears the castle and heads out over the hills.</td>
  </tr>
  <tr>
    <td align="center"><video src="https://github.com/user-attachments/assets/5a12c45a-a5d0-4fe8-a5d9-40689fd62988" width="100%" controls muted playsinline></video></td>
    <td align="center"><video src="https://github.com/user-attachments/assets/d20f2c9a-8fc2-45c7-b7cc-249a4a6b1e8c" width="100%" controls muted playsinline></video></td>
  </tr>
  <tr>
    <td colspan="2"><b>☕ Product shot, push in and rise:</b> One person pours from a pitcher into a cup on a café counter. The camera starts wide across the counter, then pushes in and rises to a top-down close-up of the pour over eight seconds.</td>
  </tr>
  <tr>
    <td align="center"><video src="https://github.com/user-attachments/assets/a49d606b-b480-4846-a60c-59044c93c1f7" width="100%" controls muted playsinline></video></td>
    <td align="center"><video src="https://github.com/user-attachments/assets/6a3afbde-32f2-4274-8f25-c7f8b93bcca5" width="100%" controls muted playsinline></video></td>
  </tr>
  <tr>
    <td colspan="2"><b>🏀 Sports, jump shot:</b> A player jumps and shoots at a hoop. The camera starts low beside them, then rises and pushes in toward the basket, finishing above the rim and looking down over eight seconds.</td>
  </tr>
</table>

<details>
<summary>More: street tracking shot</summary>

<table>
  <tr>
    <th width="50%" align="center">3D scene</th>
    <th width="50%" align="center">Generated video</th>
  </tr>
  <tr>
    <td align="center"><video src="https://github.com/user-attachments/assets/3616a492-1961-4760-ab3e-259c603b292c" width="100%" controls muted playsinline></video></td>
    <td align="center"><video src="https://github.com/user-attachments/assets/8db00ea9-9b6b-414e-a76b-9b92761504f6" width="100%" controls muted playsinline></video></td>
  </tr>
  <tr>
    <td colspan="2"><b>🚴 Street, tracking shot:</b> A person rides a bicycle along a city street. The camera starts level and tracks alongside, then rises and pulls back to a high angle looking down the street over eight seconds.</td>
  </tr>
</table>

</details>

### More prompts to try

> Build a small café. Two people sit across a table from each other. Put the camera outside the window and slowly push in over four seconds. Render the first, middle and last frame.

> A woman stands in a white studio holding a pose from the "walking" set. Three cameras: front, three-quarter, and a low angle. Render all three.

> Put a car in the middle of an empty street. Orbit the camera 90 degrees around it over five seconds.

> Take my current scene, add a second camera behind the main character, and cut to it halfway through.

## Built-in assets

Ready to use out of the box.

| Asset | Count | Notes |
| --- | --- | --- |
| 👤 Characters | 4 | Child, youth, woman, man |
| 🧍 Poses | 121 | Sitting, standing, walking, fighting, crawling, reaching and more |
| 📦 Props | Primitives | Boxes, cylinders and more, for quickly building tables, walls and objects |
| 🎥 Cameras | As many as you need | Story cameras plus a bird's-eye overview to see the whole staging at a glance |

Built-in assets are made by Topview and licensed under CC BY 4.0.

## Who it's for

- **AI short-drama and short-video creators.** Keep character positions consistent across shots and get more usable footage per generation.
- **Ad, brand and e-commerce content teams.** Agree on staging and camera work before you spend generation credits, and keep people and products in a stable relationship across shots.

Directors, storyboard artists and anyone previsualizing a scene can use it too.

## FAQ

**Do I need any 3D modeling skills?**
No. Describe what you want in plain language. Your agent builds, checks and renders the scene.

**Is it free? Do I need an account?**
Building, editing and rendering are free and need no account.

**Is my content uploaded?**
No. Every project stays in a `.topview-3d/` folder on your machine.

**Can it generate video?**
Yes. It covers the whole path from an idea, to a 3D scene, to a real animated video: you lock the staging first, then generate the video from that 3D scene.

## Learn more and join in

| | |
| --- | --- |
| 🌐 **Topview.ai** | [www.topview.ai](https://www.topview.ai) |
| 🎬 **3D Builder home** | [www.topview.ai/3d-builder](https://www.topview.ai/3d-builder) |
| 🎓 **3D Builder tutorial** | [Build scenes, stage action and move the camera](https://www.topview.ai/academy/spatial-control#3-1-3d-builder-build-scenes-stage-action-and-move-the-camera) |
| 🛠 **Developer docs** | [DEVELOPER.md](DEVELOPER.md) (CLI, project format, releases, contributing) |
| 🐞 **Feedback and bugs** | [GitHub Issues](https://github.com/topviewai/topview-3d-builder/issues) |

If Topview 3D Builder helps your work, **give the repo a ⭐** and share what you make. We'd love to see it.

## License

- Code, schemas and docs: [Apache License 2.0](https://github.com/topviewai/topview-3d-builder/blob/main/LICENSE)
- Built-in assets (characters, poses and more): [CC BY 4.0](https://github.com/topviewai/topview-3d-builder/blob/main/builtin-assets/LICENSE). Credit them as "Scene3D built-in assets © Topview, CC BY 4.0".
