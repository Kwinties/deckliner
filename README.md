<h3>🧭 How Deckliner Works</h3>
<p>
  Deckliner helps you finish a deck before a chosen <b>deadline</b>. It splits the work into a daily <b>quota</b>, shows your <b>pace</b> (🐇/🐢), and visualizes progress both in the deck browser and on the deck overview page.
</p>
<hr>

<h4>Core Concepts</h4>
<ul>
  <li><b>Deadline</b> — the date you want to be done.</li>
  <li><b>Start date</b> — when your study plan begins (used for historical pace when needed).</li>
  <li><b>Cut-off for new cards</b> — X days before the deadline; finish <b>new</b> cards by then so you can focus on <b>young</b> cards afterward.</li>
  <li><b>Young vs. Mature</b> — a card becomes <b>mature</b> when its interval ≥ 21 days; until then it’s <b>young</b>.</li>
</ul>
<hr>

<h4>What You See in the Deck Browser</h4>
<ul>
  <li><b>Deck</b> — clickable name; opens the deck overview.</li>
  <li><b>Deadline</b> — days remaining. <i>Hover</i> to see:
    <ul>
      <li>Before cut-off: when <b>new</b> cards must be finished.</li>
      <li>After cut-off: when <b>young</b> cards must be finished.</li>
    </ul>
  </li>
  <li><b>Pending</b> — cards still to learn (new + young).</li>
  <li><b>Today</b> — reviews done today for this deck (includes subdecks).</li>
  <li><b>Target</b> — cards/day needed to finish on time:
    <ul>
      <li>Before cut-off: <code>new / days_until_cutoff</code></li>
      <li>After cut-off: <code>young / days_left</code></li>
    </ul>
  </li>
  <li><b>Tempo</b> — your pace for <i>today</i>:
    <ul>
      <li>🐇 on track (daily quota met)</li>
      <li>🐢 behind (daily quota not yet met)</li>
      <li>⏳ not started (start date in the future)</li>
    </ul>
    <i>Hover</i> to see: <b>Quota • Done • Left • Today’s %</b> and the current phase (new→cutoff or young→deadline).
  </li>
  <li><b>Progress</b> — overall progress (bar + %, configurable):
    <ul>
      <li>0–67%: progress from <b>new → young</b></li>
      <li>67–100%: progress from <b>young → mature</b></li>
    </ul>
  </li>
</ul>
<hr>

<h4>Daily Message (per deck)</h4>
<p>
  Shows exactly what’s left <b>today</b> to stay on track tomorrow, e.g.:
</p>
<p style="margin-left: 16px;">
  <i>To be on track, learn <b>132</b> more today (quota 174, done 42) (~3h 25m).</i>
</p>
<ul>
  <li>Time estimate uses your measured avg. time per review (learning/review/relearn).</li>
  <li>Can be toggled on/off in settings.</li>
</ul>
<hr>

<h4>Streaks (optional)</h4>
<ul>
  <li>Counts how many consecutive days you reach the <b>daily quota</b>.</li>
  <li>❄️ at 0, 🔥 for 1+ (toggle in settings).</li>
</ul>
<hr>

<h4>Deck Overview: Daily Progress Card</h4>
<ul>
  <li>Appears between the top stats and your heatmap.</li>
  <li><b>Target today</b>: exact daily quota based on current phase (new→cutoff or young→deadline).</li>
  <li><b>Progress bar</b>: how much of today’s quota you’ve already completed.</li>
  <li><b>Done today</b> + percentage: quick confirmation.</li>
  <li>Can be turned on/off in settings.</li>
</ul>
<hr>

<h4>The Math (quick version)</h4>
<ol>
  <li><b>Which pile now?</b> If you still have <b>new</b> cards and today &lt; cut-off → finish <b>new</b>. Otherwise: <b>young</b>.</li>
  <li><b>Remaining days</b>:
    <ul>
      <li>Before cut-off: <code>days_until_cutoff = max((cutoff_date - today).days, 1)</code></li>
      <li>After cut-off: <code>days_left = max((deadline - today).days, 1)</code></li>
    </ul>
  </li>
  <li><b>Daily target (indicator)</b>: <code>target_per_day = remaining_cards / remaining_days</code></li>
  <li><b>Exact “today quota”</b>:
    <pre style="margin:8px 0; padding:8px; background:#111; color:#ddd; border-radius:6px;">quota_today = ceil(remaining_cards - target_per_day * (remaining_days - 1))</pre>
    This is what the <b>daily progress bar</b>, <b>tempo</b>, and <b>daily message</b> use.
  </li>
  <li><b>Done today</b>: today’s review count for this deck (incl. subdecks).</li>
  <li><b>Tempo</b>: 🐇 if <code>done_today &gt;= quota_today</code>, else 🐢.</li>
  <li><b>Time estimate</b>: remaining-today × avg time/review → shown as <i>~Hh Mm</i>.</li>
</ol>
<hr>

<h4>Settings</h4>
<ul>
  <li><b>Enable Deadline</b> — turn a plan on/off per deck.</li>
  <li><b>Customize</b>:
    <ul>
      <li><b>Name</b></li>
      <li><b>Deadline</b></li>
      <li><b>Start date</b></li>
      <li><b>Finish new cards</b> — cut-off offset (e.g., “-5 days before deadline”).</li>
    </ul>
  </li>
  <li><b>Show daily message below each deck</b></li>
  <li><b>Enable streaks</b></li>
  <li><b>Progress display</b> — bar + %, only bar, or only %.</li>
  <li><b>Show daily progress bar on deck overview</b></li>
</ul>
<p>Open via the gear icon next to a deck. Use <b>Clear</b> to remove deadlines (all or selected).</p>
<hr>

<h4>Good to Know</h4>
<ul>
  <li>A card becomes <b>mature</b> when its interval ≥ 21 days.</li>
  <li>To force work on young cards even if they’re not due today, create a <b>Filtered Deck</b>:
    <pre style="margin:8px 0; padding:8px; background:#111; color:#ddd; border-radius:6px;">deck:"your_deck" is:review prop:ivl&lt;21</pre>
  </li>
</ul>
<hr>

<h4>FAQ</h4>
<ul>
  <li><b>Why 🐢 if my overall progress is good?</b> Tempo is a <i>today</i> signal. If the bar &lt; 100%, you haven’t met today’s quota yet.</li>
  <li><b>What if my quota is 0?</b> You’ll see “No quota today.” The daily card is considered complete.</li>
  <li><b>Are subdecks included?</b> Yes — counts and “Done today” include subdecks.</li>
  <li><b>Do time estimates include relearn?</b> Yes — learning, review, and relearn are included in the average time per review.</li>
</ul>
<hr>

<h4>Troubleshooting</h4>
<ul>
  <li><b>Daily card missing</b> — make sure it’s enabled in settings. If you use other overview add-ons, Deckliner tries to insert before the heatmap; otherwise below the “Study” block.</li>
  <li><b>Numbers look off</b> — verify <b>deadline</b>, <b>start date</b>, and <b>cut-off</b> for the correct deck.</li>
  <li><b>I want averages back</b> — the UI now focuses on daily quota to avoid mixed signals, but you can reintroduce averages if you prefer.</li>
</ul>
