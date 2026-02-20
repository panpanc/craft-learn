# Animation Player — Shared Template

A reusable animation player for step-by-step algorithm walkthroughs in Jupyter notebooks. Skills that reference this file should read it at generation time and adapt the templates below.

## 1. When to include

Include an animated walkthrough when **all** of these hold:
- The algorithm has a **step-by-step process** (pointer movement, partitioning, tree traversal, etc.)
- The process produces **3–50 distinct visual states** on the chosen input
- Each state differs meaningfully from the previous one (not just a counter incrementing)

**Skip** the animation when:
- The topic is conceptual with no iterative process (e.g., "what is Big-O notation")
- The step count exceeds 50 on the smallest reasonable input — prefer a sampled subset or skip entirely
- The visual would be identical to an existing static diagram in the notebook

## 2. Standard color scheme

Use these colors consistently across all animations:

| Role | Color | Hex |
|------|-------|-----|
| Current / active element | Red | `#ff6b6b` |
| Processed / done | Teal | `#4ecdc4` |
| Pointer / index marker | Blue | `#45b7d1` |
| Candidate / considering | Yellow | `#f9ca24` |
| Inactive / default | Gray | `#ddd` |

## 3. Defaults

- Figure size: `figsize=(10, 4)`, `dpi=100`
- Base speed (1×): 1 second per frame
- Maximum frames: 50 (sample key frames if the algorithm runs longer)
- CSS prefix: `ap-` (avoids collision with other notebook widgets)
- Unique ID: generate with `f"ap{random.randint(10000,99999)}"` so re-runs don't clash

## 4. Python frame rendering template

This is the generic pipeline. The skill fills in `render_frame` with problem-specific visualization code.

```python
import matplotlib.pyplot as plt
import io
import base64
import json as _json
import random
from IPython.display import display, HTML

# --- 1. Build snapshots ---
# snapshots is a list of dicts, each capturing the algorithm state at one step.
# Example for two-pointer: [{"arr": [...], "left": 0, "right": 5, "status": "searching"}, ...]
snapshots = []
# ... (problem-specific code to populate snapshots) ...

def render_frame(ax, snapshot, step_idx, total_steps):
    """Render one algorithm state onto a matplotlib Axes.

    Args:
        ax: matplotlib Axes (already cleared)
        snapshot: dict with algorithm state for this step
        step_idx: 0-based index of this frame
        total_steps: total number of frames
    """
    # --- Problem-specific drawing code goes here ---
    # Use the standard color scheme:
    #   #ff6b6b = current/active
    #   #4ecdc4 = processed/done
    #   #45b7d1 = pointer
    #   #f9ca24 = candidate
    #   #ddd    = inactive/default
    pass

# --- 2. Render snapshots to base64 PNGs ---
frames_b64 = []
for i, snap in enumerate(snapshots):
    fig, ax = plt.subplots(figsize=(10, 4))
    render_frame(ax, snap, i, len(snapshots))
    buf = io.BytesIO()
    fig.savefig(buf, format='png', bbox_inches='tight', dpi=100)
    plt.close(fig)
    buf.seek(0)
    frames_b64.append(base64.b64encode(buf.read()).decode('ascii'))

assert len(frames_b64) >= 3, f"Too few frames ({len(frames_b64)}); need at least 3"
assert len(frames_b64) <= 50, f"Too many frames ({len(frames_b64)}); max is 50"
print(f"Rendered {len(frames_b64)} frames.")
```

## 5. HTML/CSS/JS player template

Insert this after the frame-rendering code in the same cell. Replace `__UID__`, `__FIRST_FRAME__`, `__MAX__`, and `__FRAMES__` with the actual values.

```python
uid = f"ap{random.randint(10000, 99999)}"
n_frames = len(frames_b64)

html_tpl = """
<div id="__UID__" style="text-align:center; font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif; max-width:820px; margin:0 auto;">
  <style>
    #__UID__ .ap-frame {
      background:#fafafa; border:1px solid #e0e0e0;
      border-radius:10px; padding:12px; margin-bottom:8px;
    }
    #__UID__ .ap-frame img { max-width:100%; border-radius:6px; display:block; margin:0 auto; }
    #__UID__ .ap-controls { display:flex; justify-content:center; gap:8px; flex-wrap:wrap; }
    #__UID__ .ap-btn {
      padding:8px 16px; border:1px solid #ddd; border-radius:8px;
      background:white; font-size:14px; cursor:pointer; color:#333;
      transition:all 0.15s ease; user-select:none;
    }
    #__UID__ .ap-btn:hover:not(:disabled) { background:#f0f0f0; transform:scale(1.03); }
    #__UID__ .ap-btn:disabled { opacity:0.35; cursor:default; transform:none; }
    #__UID__ .ap-btn:active:not(:disabled) { transform:scale(0.97); }
    #__UID__ .ap-play {
      padding:8px 22px; border:none; border-radius:8px;
      background:#45b7d1; color:white; font-size:14px; font-weight:600;
      cursor:pointer; min-width:120px; transition:all 0.15s ease; user-select:none;
    }
    #__UID__ .ap-play:hover { filter:brightness(0.9); transform:scale(1.03); }
    #__UID__ .ap-play:active { transform:scale(0.97); }
    #__UID__ .ap-slider-row input[type=range] {
      width:80%; accent-color:#45b7d1; cursor:pointer; height:6px;
    }
    #__UID__ .ap-speed-row {
      display:flex; justify-content:center; align-items:center;
      gap:6px; margin-top:10px; flex-wrap:wrap;
    }
    #__UID__ .ap-speed-label {
      font-size:13px; color:#888; font-weight:500; margin-right:2px;
    }
    #__UID__ .ap-speed {
      padding:4px 12px; border:1px solid #ddd; border-radius:6px;
      background:white; font-size:13px; cursor:pointer; color:#555;
      transition:all 0.15s ease; user-select:none;
    }
    #__UID__ .ap-speed:hover { background:#f0f0f0; }
    #__UID__ .ap-speed.active {
      background:#45b7d1; color:white; border-color:#45b7d1; font-weight:600;
    }
  </style>
  <div class="ap-frame">
    <img id="__UID__-img" src="data:image/png;base64,__FIRST_FRAME__">
  </div>
  <div class="ap-slider-row" style="margin:10px 0 4px;">
    <input type="range" id="__UID__-slider" min="0" max="__MAX__" value="0">
  </div>
  <div id="__UID__-label" style="margin:2px 0 14px; font-size:15px; color:#555; font-weight:500;">
    Step 0 / __MAX__
  </div>
  <div class="ap-controls">
    <button class="ap-btn" id="__UID__-back" title="Go back one step">&#9664; Back</button>
    <button class="ap-play" id="__UID__-play" title="Play / Pause">&#9654;  Play</button>
    <button class="ap-btn" id="__UID__-fwd" title="Go forward one step">Next &#9654;</button>
    <button class="ap-btn" id="__UID__-replay" title="Start over from the beginning">&#8635; Replay</button>
  </div>
  <div class="ap-speed-row">
    <span class="ap-speed-label">Speed:</span>
    <button class="ap-speed" data-ms="2000">0.5x</button>
    <button class="ap-speed active" data-ms="1000">1x</button>
    <button class="ap-speed" data-ms="500">2x</button>
    <button class="ap-speed" data-ms="333">3x</button>
    <button class="ap-speed" data-ms="200">5x</button>
  </div>
</div>
"""

# Uses setTimeout chain (not setInterval) to prevent frame-skipping.
js_tpl = """
<script>
(function() {
  var frames = __FRAMES__;
  var cur = 0, playing = false, tmr = null, N = frames.length, MS = 1000;
  var el = function(s) { return document.getElementById('__UID__-' + s); };
  var img = el('img'), sld = el('slider'), lbl = el('label');
  var btnPlay = el('play'), btnBack = el('back'), btnFwd = el('fwd');
  var container = document.getElementById('__UID__');

  function show(i) {
    cur = Math.max(0, Math.min(N - 1, i));
    img.src = 'data:image/png;base64,' + frames[cur];
    sld.value = cur;
    lbl.textContent = 'Step ' + cur + ' / ' + (N - 1);
    btnBack.disabled = (cur === 0);
    btnFwd.disabled = (cur === N - 1);
  }

  function tick() {
    if (!playing || cur >= N - 1) { stopPlay(); return; }
    show(cur + 1);
    tmr = setTimeout(tick, MS);
  }

  function startPlay() {
    if (cur >= N - 1) show(0);
    playing = true;
    btnPlay.innerHTML = '&#9646;&#9646;  Pause';
    btnPlay.style.background = '#e74c3c';
    tmr = setTimeout(tick, MS);
  }

  function stopPlay() {
    playing = false;
    btnPlay.innerHTML = '&#9654;  Play';
    btnPlay.style.background = '#45b7d1';
    if (tmr) { clearTimeout(tmr); tmr = null; }
  }

  btnPlay.onclick = function() { playing ? stopPlay() : startPlay(); };
  btnBack.onclick = function() { stopPlay(); show(cur - 1); };
  btnFwd.onclick = function() { stopPlay(); show(cur + 1); };
  el('replay').onclick = function() { show(0); startPlay(); };
  sld.oninput = function() { stopPlay(); show(parseInt(this.value)); };

  var speedBtns = container.querySelectorAll('.ap-speed');
  for (var i = 0; i < speedBtns.length; i++) {
    speedBtns[i].onclick = (function(btn) {
      return function() {
        MS = parseInt(btn.getAttribute('data-ms'));
        for (var j = 0; j < speedBtns.length; j++)
          speedBtns[j].classList.remove('active');
        btn.classList.add('active');
        if (playing) {
          if (tmr) { clearTimeout(tmr); tmr = null; }
          tmr = setTimeout(tick, MS);
        }
      };
    })(speedBtns[i]);
  }

  show(0);
})();
</script>
"""

player_html = (html_tpl
    .replace('__UID__', uid)
    .replace('__FIRST_FRAME__', frames_b64[0])
    .replace('__MAX__', str(n_frames - 1)))

player_js = (js_tpl
    .replace('__FRAMES__', _json.dumps(frames_b64))
    .replace('__UID__', uid))

display(HTML(player_html + player_js))
```

## 6. Large frame count handling

If the algorithm produces more than 50 states on the chosen input:

1. **First choice:** Use a smaller input. Two Sum on a 6-element array is better than a 100-element array.
2. **Second choice:** Sample key frames — keep first, last, and every Nth frame to stay under 50. Add a "(sampled — showing key steps)" note in the step label.
3. **Last resort:** Skip the animation entirely and rely on the text walkthrough. Add a markdown note: "Animation omitted — too many steps for this input size."

## 7. Verification checklist

After generating the animation cell, verify:

- [ ] Frame count is between 3 and 50 (assert in code)
- [ ] No leaked matplotlib figures (`plt.close(fig)` after every render)
- [ ] Unique ID uses the `ap` prefix + random suffix
- [ ] `frames_b64` list is not empty and contains valid base64 strings
- [ ] The player HTML renders (contains `<div id="ap`)
- [ ] JSON encoding of frames list doesn't break the notebook JSON (no unescaped quotes)
- [ ] The animation cell is self-contained — runs after prior cells without extra imports
- [ ] **All visual content fits within the frame bounds.** When visualizations grow or shrink across frames (trees gaining nodes, arrays expanding, etc.), compute axis limits from the actual data positions in each frame — don't use static limits. Call `ax.set_xlim`/`ax.set_ylim` with margins derived from the min/max coordinates of all drawn elements in that frame. Test the largest frame specifically.

Common failure causes:
- **Empty snapshots list:** The algorithm loop didn't append states — check the snapshot-building code
- **Unclosed figures:** Missing `plt.close(fig)` causes memory warnings and blank frames
- **JSON encoding error:** `frames_b64` contains non-ASCII or the `_json.dumps()` call fails — ensure all frames are plain ASCII base64
- **Notebook JSON invalid:** Unescaped backslashes or quotes in the HTML template — use raw strings or proper escaping
- **Clipped content in frames:** Axes limits are too tight or static, causing nodes/labels to go off-screen as the visualization grows. Always compute limits from actual drawn positions per frame, with generous margins (at least 0.5-1.0 units). For tree/graph visualizations, compute layout positions first, then set `xlim`/`ylim` from the position extremes.
- **Deno `btoa` Unicode error:** `btoa()` in Deno only handles Latin1 (0-255). If SVG strings contain Unicode (arrows, em dashes, etc.), either use ASCII-only text in SVGs or encode via `TextEncoder` first: `const bytes = new TextEncoder().encode(svg); let bin = ""; for (const b of bytes) bin += String.fromCharCode(b); return btoa(bin);`

## 8. Concrete example — Two-pointer array animation

This shows the complete pattern for a Two Sum (sorted array) problem using two pointers.

```python
import matplotlib.pyplot as plt
import matplotlib.patches as patches
import io
import base64
import json as _json
import random
from IPython.display import display, HTML

# --- Problem-specific setup ---
arr = [1, 3, 5, 7, 9, 11]
target = 10

# --- Build snapshots ---
snapshots = []
left, right = 0, len(arr) - 1
while left < right:
    current_sum = arr[left] + arr[right]
    snapshots.append({
        "arr": arr[:], "left": left, "right": right,
        "sum": current_sum, "target": target,
        "status": "found" if current_sum == target else
                  "too_small" if current_sum < target else "too_large"
    })
    if current_sum == target:
        break
    elif current_sum < target:
        left += 1
    else:
        right -= 1

def render_frame(ax, snap, step_idx, total_steps):
    a = snap["arr"]
    n = len(a)
    for i, val in enumerate(a):
        if i == snap["left"] and i == snap["right"]:
            color = '#45b7d1'  # pointer (overlap)
        elif i == snap["left"] or i == snap["right"]:
            color = '#45b7d1'  # pointer
        elif snap["left"] < i < snap["right"]:
            color = '#f9ca24'  # candidate region
        else:
            color = '#ddd'     # inactive
        rect = patches.FancyBboxPatch((i - 0.4, 0), 0.8, 1,
            boxstyle="round,pad=0.05", facecolor=color, edgecolor='white', linewidth=2)
        ax.add_patch(rect)
        ax.text(i, 0.5, str(val), ha='center', va='center',
                fontsize=14, fontweight='bold', color='white' if color != '#ddd' else '#666')

    # Pointer labels
    ax.text(snap["left"], -0.3, "L", ha='center', fontsize=12, fontweight='bold', color='#45b7d1')
    ax.text(snap["right"], -0.3, "R", ha='center', fontsize=12, fontweight='bold', color='#45b7d1')

    # Status text
    status_color = '#4ecdc4' if snap["status"] == "found" else '#ff6b6b' if snap["status"] == "too_large" else '#f9ca24'
    status_text = f"arr[{snap['left']}] + arr[{snap['right']}] = {snap['sum']}  (target={snap['target']})  →  {snap['status'].replace('_', ' ')}"
    ax.text(n / 2 - 0.5, 1.4, status_text, ha='center', fontsize=11, color=status_color, fontweight='bold')

    ax.set_xlim(-0.8, n - 0.2)
    ax.set_ylim(-0.7, 1.8)
    ax.set_aspect('equal')
    ax.axis('off')
    ax.set_title(f"Two Pointers — Step {step_idx + 1}/{total_steps}", fontsize=12, fontweight='bold')

# --- Render frames ---
frames_b64 = []
for i, snap in enumerate(snapshots):
    fig, ax = plt.subplots(figsize=(10, 4))
    render_frame(ax, snap, i, len(snapshots))
    buf = io.BytesIO()
    fig.savefig(buf, format='png', bbox_inches='tight', dpi=100)
    plt.close(fig)
    buf.seek(0)
    frames_b64.append(base64.b64encode(buf.read()).decode('ascii'))

print(f"Rendered {len(frames_b64)} frames.")

# --- Player (use the HTML/JS template from section 5) ---
uid = f"ap{random.randint(10000, 99999)}"
n_frames = len(frames_b64)
# ... (insert html_tpl and js_tpl from section 5, then assemble and display) ...
```
