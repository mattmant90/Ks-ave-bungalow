```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PO Light Troubleshooting — Full Chain</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Space+Grotesk:wght@600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#12151a; --panel:#1a1f26; --line:#2c333d; --text:#e6eaee; --muted:#8b96a3;
    --amber:#e8a33d; --coral:#e8654f; --teal:#46b8a6; --gray:#3a4250; --purple:#a888e0;
  }
  *{box-sizing:border-box;}
  body{margin:0;background:var(--bg);color:var(--text);font-family:'JetBrains Mono',monospace;display:flex;flex-direction:column;align-items:center;padding:24px 12px 60px;}
  h1{font-family:'Space Grotesk',sans-serif;font-size:18px;margin:0 0 6px;text-align:center;}
  h2{font-family:'Space Grotesk',sans-serif;font-size:14.5px;margin:34px 0 12px;text-align:left;width:100%;max-width:640px;color:var(--purple);}
  p{color:var(--muted);font-size:12px;text-align:center;max-width:560px;margin:0 0 10px;line-height:1.6;}
  svg{width:100%;max-width:680px;height:auto;}

  .method{width:100%;max-width:640px;background:var(--panel);border:1px solid var(--line);border-radius:8px;padding:16px 18px;margin-top:8px;}
  .method ul{margin:0;padding-left:18px;font-size:12px;line-height:1.9;color:var(--text);}
  .method li b{color:var(--amber);}
  .warn{width:100%;max-width:640px;margin:12px 0 4px;padding:10px 14px;background:#241a17;border:1px solid #4a2e24;border-radius:6px;color:#e8a08f;font-size:11.5px;line-height:1.6;}

  table{width:100%;max-width:640px;border-collapse:collapse;font-size:11.5px;margin-top:6px;}
  th,td{border:1px solid var(--line);padding:8px 10px;text-align:left;vertical-align:top;}
  th{background:var(--panel);color:var(--muted);font-weight:600;font-size:11px;text-transform:uppercase;letter-spacing:.03em;}
  td.name{color:var(--amber);font-weight:600;white-space:nowrap;}
  tr.cut td{color:#e8a08f;}
  .badge{display:inline-block;font-size:9.5px;padding:1px 6px;border-radius:10px;background:#4a2e24;color:#e8a08f;margin-left:6px;letter-spacing:.02em;}

  .box{stroke-width:1;}
  .box.gray{fill:#20262e;stroke:var(--gray);}
  .box.amber{fill:#2a2115;stroke:var(--amber);}
  .box.coral{fill:#241a17;stroke:var(--coral);}
  .box.teal{fill:#152622;stroke:var(--teal);}
  .box.purple{fill:#221c33;stroke:var(--purple);}
  .th{font-family:'Space Grotesk',sans-serif;font-weight:600;font-size:13px;fill:var(--text);}
  .ts{font-family:'JetBrains Mono',monospace;font-size:11px;fill:var(--muted);}
  .tag{font-family:'JetBrains Mono',monospace;font-size:10.5px;fill:var(--muted);}
  .arr{stroke:var(--muted);stroke-width:1.3;fill:none;}
</style>
</head>
<body>
<h1>PO light troubleshooting — full chain</h1>
<p>XPR relaxed (closed contact) = AC good. 1-POR and 2-POR are two relays in series, not fuses — both must pick. Continuity checks and the lamp resistor/strap block are included below.</p>

<div class="warn"><b>Before continuity testing:</b> isolate or de-energize the circuit first. Checking continuity on a live circuit gives false readings and can damage your meter. Set the meter to con[...]

<div class="method">
<ul>
<li><b>Wire / strap / jumper:</b> should read near-zero Ω end to end. Anything above a few ohms means a loose crimp, corrosion, or a broken strand.</li>
<li><b>Resistor (RG3T, RG6T/B, RF3T, RF6T/B blocks):</b> should read a stable, non-zero resistance across its two terminals. <b>0 Ω = shorted/burned</b>. <b>OL / infinite = open, likely burnt out</b>[...]
<li><b>Relay contact (1-POR, 2-POR, XPR):</b> with the relay picked, its front contact should read near-zero Ω. With it relaxed, its back contact should read near-zero Ω. Infinite in the state that [...]
<li><b>Relay coil:</b> should read a fixed, non-zero resistance matching the relay's rating. 0 Ω or OL both indicate a bad coil.</li>
<li><b>WAGO terminals:</b> probe the test port on top of the connector body, not the orange release lever — see earlier note on backprobing at the screw terminal instead if the WAGO port is hard to [...]
</ul>
</div>

<h2>1 — Main chain: XPR → POR relays → POK → WAGO 20+</h2>
<svg viewBox="0 0 680 970" role="img">
<title>PO light troubleshooting flowchart, main chain</title>
<desc>Decision tree tracing AC power presence from the XPR relay contact through the 1-POR and 2-POR relays in series to the POK wire and WAGO 20 plus terminal feeding the PO lamp.</desc>
<defs><marker id="arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse"><path d="M2 1L8 5L2 9" fill="none" stroke="currentColor" stroke-width="1.5" [...]

<rect class="box gray" x="310" y="20" width="240" height="50" rx="10"/>
<text class="th" x="430" y="40" text-anchor="middle" dominant-baseline="central">PO light dark</text>
<text class="ts" x="430" y="58" text-anchor="middle" dominant-baseline="central">AC present at bungalow</text>
<line x1="430" y1="70" x2="430" y2="103" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>

<polygon class="box amber" points="430,105 570,140 430,175 290,140"/>
<text class="th" x="430" y="134" text-anchor="middle" dominant-baseline="central">XPR contact</text>
<text class="th" x="430" y="150" text-anchor="middle" dominant-baseline="central">closed?</text>
<line x1="290" y1="140" x2="272" y2="140" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="277" y="130" text-anchor="middle">No</text>
<rect class="box coral" x="40" y="110" width="230" height="60" rx="8"/>
<text class="th" x="155" y="132" text-anchor="middle" dominant-baseline="central">Upstream fault</text>
<text class="ts" x="155" y="150" text-anchor="middle" dominant-baseline="central">continuity-check XPR coil circuit</text>
<line x1="430" y1="175" x2="430" y2="213" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="450" y="197" text-anchor="middle">Yes</text>

<polygon class="box amber" points="430,215 570,250 430,285 290,250"/>
<text class="th" x="430" y="244" text-anchor="middle" dominant-baseline="central">Continuity to</text>
<text class="th" x="430" y="260" text-anchor="middle" dominant-baseline="central">terminal 11?</text>
<line x1="290" y1="250" x2="272" y2="250" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="277" y="240" text-anchor="middle">No</text>
<rect class="box coral" x="40" y="220" width="230" height="60" rx="8"/>
<text class="th" x="155" y="242" text-anchor="middle" dominant-baseline="central">Wiring fault</text>
<text class="ts" x="155" y="260" text-anchor="middle" dominant-baseline="central">repair XPR 21 → terminal 11</text>
<line x1="430" y1="285" x2="430" y2="323" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="450" y="307" text-anchor="middle">Yes</text>

<polygon class="box amber" points="430,325 570,360 430,395 290,360"/>
<text class="th" x="430" y="354" text-anchor="middle" dominant-baseline="central">1-POR coil</text>
<text class="th" x="430" y="370" text-anchor="middle" dominant-baseline="central">reads OK &amp; picked?</text>
<line x1="290" y1="360" x2="272" y2="360" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="277" y="350" text-anchor="middle">No</text>
<rect class="box coral" x="40" y="330" width="230" height="60" rx="8"/>
<text class="th" x="155" y="352" text-anchor="middle" dominant-baseline="central">Relay fault</text>
<text class="ts" x="155" y="370" text-anchor="middle" dominant-baseline="central">service/replace 1-POR relay</text>
<line x1="430" y1="395" x2="430" y2="433" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="450" y="417" text-anchor="middle">Yes</text>

<polygon class="box amber" points="430,435 570,470 430,505 290,470"/>
<text class="th" x="430" y="464" text-anchor="middle" dominant-baseline="central">2-POR coil</text>
<text class="th" x="430" y="480" text-anchor="middle" dominant-baseline="central">reads OK &amp; picked?</text>
<line x1="290" y1="470" x2="272" y2="470" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="277" y="460" text-anchor="middle">No</text>
<rect class="box coral" x="40" y="440" width="230" height="60" rx="8"/>
<text class="th" x="155" y="462" text-anchor="middle" dominant-baseline="central">Relay fault</text>
<text class="ts" x="155" y="480" text-anchor="middle" dominant-baseline="central">service/replace 2-POR relay</text>
<line x1="430" y1="505" x2="430" y2="543" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="450" y="527" text-anchor="middle">Yes</text>

<polygon class="box amber" points="430,545 570,580 430,615 290,580"/>
<text class="th" x="430" y="574" text-anchor="middle" dominant-baseline="central">1-POR term 5</text>
<text class="th" x="430" y="590" text-anchor="middle" dominant-baseline="central">contact continuity?</text>
<line x1="290" y1="580" x2="272" y2="580" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="277" y="570" text-anchor="middle">No</text>
<rect class="box coral" x="40" y="550" width="230" height="60" rx="8"/>
<text class="th" x="155" y="572" text-anchor="middle" dominant-baseline="central">Contact fault</text>
<text class="ts" x="155" y="590" text-anchor="middle" dominant-baseline="central">inspect/replace 1-POR relay</text>
<line x1="430" y1="615" x2="430" y2="653" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="450" y="637" text-anchor="middle">Yes</text>

<polygon class="box amber" points="430,655 570,690 430,725 290,690"/>
<text class="th" x="430" y="684" text-anchor="middle" dominant-baseline="central">2-POR term 5</text>
<text class="th" x="430" y="700" text-anchor="middle" dominant-baseline="central">contact continuity?</text>
<line x1="290" y1="690" x2="272" y2="690" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="277" y="680" text-anchor="middle">No</text>
<rect class="box coral" x="40" y="660" width="230" height="60" rx="8"/>
<text class="th" x="155" y="682" text-anchor="middle" dominant-baseline="central">Contact fault</text>
<text class="ts" x="155" y="700" text-anchor="middle" dominant-baseline="central">inspect/replace 2-POR relay</text>
<line x1="430" y1="725" x2="430" y2="763" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="450" y="747" text-anchor="middle">Yes</text>

<polygon class="box amber" points="430,765 570,800 430,835 290,800"/>
<text class="th" x="430" y="794" text-anchor="middle" dominant-baseline="central">Continuity POK</text>
<text class="th" x="430" y="810" text-anchor="middle" dominant-baseline="central">wire → WAGO 20+?</text>
<line x1="290" y1="800" x2="272" y2="800" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="277" y="790" text-anchor="middle">No</text>
<rect class="box coral" x="40" y="770" width="230" height="60" rx="8"/>
<text class="th" x="155" y="792" text-anchor="middle" dominant-baseline="central">Wiring fault</text>
<text class="ts" x="155" y="810" text-anchor="middle" dominant-baseline="central">repair POK wire to WAGO 20+</text>
<line x1="430" y1="835" x2="430" y2="873" class="arr" marker-end="url(#arrow)" color="var(--muted)"/>
<text class="tag" x="450" y="857" text-anchor="middle">Yes</text>

<rect class="box purple" x="290" y="875" width="280" height="80" rx="10"/>
<text class="th" x="430" y="898" text-anchor="middle" dominant-baseline="central">Still dark at WAGO 20+</text>
<text class="ts" x="430" y="916" text-anchor="middle" dominant-baseline="central">continue to lamp resistor &amp;</text>
<text class="ts" x="430" y="932" text-anchor="middle" dominant-baseline="central">strap checks in section 2 below</text>
</svg>

<h2>2 — Lamp resistor block &amp; straps (from your photo)</h2>
<p>These are the wire-wound resistors feeding the RG and RF mast lamps. Check each resistor's terminal-to-terminal resistance, and each strap's continuity, in this order.</p>

<table>
<tr><th>Element</th><th>Terminals</th><th>Check</th><th>Expect</th></tr>
<tr>
<td class="name">RG3T resistor</td>
<td>Top: RG3T POK-R / POK-L<br>Bottom: RG3B / 1-POR 8</td>
<td>Resistance top-to-bottom</td>
<td>Stable non-zero Ω — not 0, not OL</td>
</tr>
<tr>
<td class="name">RG6T/B resistor</td>
<td>Top: RG6B XN / LD45T<br>Bottom: RG6T POK-L XN / POK-R XN</td>
<td>Resistance top-to-bottom</td>
<td>Stable non-zero Ω</td>
</tr>
<tr>
<td class="name">RF6T/B resistor</td>
<td>Top: RF6B XN / LD45T<br>Bottom: RF6T XN POK</td>
<td>Resistance top-to-bottom</td>
<td>Stable non-zero Ω</td>
</tr>
<tr>
<td class="name">RF3T resistor</td>
<td>Top: RF3T POK-S<br>Bottom: RF3B / 2-POR 3</td>
<td>Resistance top-to-bottom</td>
<td>Stable non-zero Ω</td>
</tr>
<tr>
<td class="name">Strap 1</td>
<td>RG6T POK-L XN ↔ RG6T POK-R XN</td>
<td>Continuity across the two tagged leads at that shared terminal</td>
<td>Near-zero Ω</td>
</tr>
<tr>
<td class="name">Strap 2</td>
<td>RG6B XN / LD45T ↔ RF6B XN / LD45T</td>
<td>Continuity across the jumper tying the two upper-left/lower-left resistor tops together</td>
<td>Near-zero Ω</td>
</tr>
<tr class="cut">
<td class="name">Strap 3 <span class="badge">should be open</span></td>
<td>RF6B XN / LD45T ↔ RF6T XN POK</td>
<td>Continuity across this jumper</td>
<td>Should read OPEN — this strap was documented as intentionally open. If it reads continuous, that's unexpected and worth flagging, not assuming it's fine.</td>
</tr>
</table>

</body>
</html>
```
