# GOD Mic Chain

A single-page microphone processing chain you can test in Safari. Record a take, then flip between **A (dry)** and **B (processed)** while it loops. The switch is instant and playback never stops.

The first module is a **personal EQ** with 8 bands: high-pass, low shelf, four bells, high shelf and low-pass. Every band can be set to any type.

## Run it

Safari only lets a page use the microphone over `https://` or `http://localhost`, so serve the folder locally:

```sh
cd VST
python3 -m http.server 8000
```

Then open <http://localhost:8000> in Safari and allow the microphone.

To use it on an iPhone or iPad, turn on GitHub Pages (repo Settings → Pages → Deploy from branch → `main` / root) and open the `https://…github.io/VST/` URL.

## Test loop

1. **Arm record** asks for the mic and arms recording.
2. **Play** starts recording.
3. **Pause** ends the take.
4. **Disarm** turns recording off.
5. **Play** loops the take. Click **A** or **B** (or press `A`/`B`, `←`/`→`, `X`) to switch with no gap.

**B** is processed live, so EQ changes are heard right away while the take loops. **Match loudness** sets the output trim so B has the same RMS level as A, so a louder side doesn't win by default. **Save A / Save B** export 24-bit WAVs.

The mic is captured raw: echo cancellation, noise suppression and auto gain are turned off.

## EQ controls

- Drag a numbered point to set frequency and gain. Hold `Shift` while dragging for fine moves.
- Use the scroll wheel over a point to change Q.
- Double-click a point to turn its band on or off. `⌥`-click resets its gain to 0 dB.
- Click the graph, then use the arrow keys to nudge the selected band. Keys `1`–`8` select a band.
- Settings are saved automatically in the browser. Presets can be saved by name, or copied and pasted as JSON.

## Adding modules

`buildChain()` in `index.html` builds the chain from modules. New modules (compressor, de-esser, saturation…) go there, and they run in both the live chain and the offline render used for export and loudness matching.
