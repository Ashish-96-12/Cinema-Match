# Cinema Match

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Ashish-96-12/Cinema-Match/blob/main/cinema_match_v2.ipynb)

An AI assistant for film directors. Upload a screenplay and work through it scene by scene: shot lists and camera angles, music for each scene, ideas for what should happen next, and script analysis. Built with LangGraph (7 agents), FAISS retrieval and a Gradio UI.

## Run it on Google Colab

1. Click **Open in Colab** above.
2. Optional, for real AI answers: click the 🔑 **Secrets** icon in Colab's left sidebar, add `ANTHROPIC_API_KEY`, and switch on **Notebook access**.
3. **Runtime > Run all.** The first run installs packages (1-2 minutes).
4. The last cell prints a public `https://....gradio.live` link. Open it, upload your script, and start asking.

Colab storage is temporary: uploaded scripts disappear when the runtime resets.

## Run it locally

```bash
pip install anthropic langgraph langchain-core sentence-transformers faiss-cpu gradio pypdf python-docx numpy pandas
export ANTHROPIC_API_KEY=sk-ant-...     # optional, see "Modes" below
jupyter notebook cinema_match_v2.ipynb  # run all cells; the app opens on http://localhost:7860
```

## Modes

- **Live** (when `ANTHROPIC_API_KEY` is set): every agent answers with Claude, using the full text of the scene you're asking about plus your recent chat.
- **Demo** (no key): rule-based answers built from your actual scenes (mood, lighting for the time of day, a shot list using the scene's characters and action, music picks from the library, next-step ideas). Good for trying the app; set a key for real answers.

## Working scene by scene

After uploading a script you can:

- Pick a scene from the **Current scene** dropdown or step through with **Previous / Next**.
- Ask in plain words: "camera angles for scene 4", "music for scenes 2 to 5", "now the next scene", "go back to the previous scene", "the last scene", "music for the harbor scene", "what should happen next?"
- Use the quick buttons: **Shot list for this scene**, **Music for this scene**, **What should happen next?**
- Click **Break down every scene** for a full scene-by-scene prep document (camera, music, next steps) you can download as Markdown.

Cinema Match remembers which scene you're on and which kind of help you last asked for, so follow-ups like "now do the next one" continue where you left off.

## Supported script formats

PDF, DOCX, TXT, Markdown and Fountain. Scene headings can be:

- Slug lines: `INT. HOUSE - NIGHT`, `EXT HOUSE - DAY` (no period), `INT./EXT. CAR - NIGHT`
- Numbered scenes from Final Draft / WriterDuet / Celtx: `12 INT. HOUSE - DAY 12`
- Scene-number style common in Indian and TV scripts: `SCENE 1 - EXT - TEMPLE - NIGHT`, `Sc. 9: Village road / Day`

Scanned PDFs (images of pages) need OCR before upload. If no headings are found, the whole script is treated as one scene and the app tells you.
