<!-- TITLE (centered) -->
<table width="720" align="center" cellspacing="0" cellpadding="6" border="0">
  <tr>
    <td align="center" width="720">
      <b style="font-size:50px;">Oxygen-evolving complex</b>
    </td>
  </tr>
</table>

<table width="720" align="center" cellspacing="0" cellpadding="6" border="0">

<!-- TOP ROW: Left = OEC image (240) | Right = Areas & States (480) -->
<tr>
<!-- Left: OEC image -->
<td width="240" valign="top">
<table width="240" cellspacing="0" cellpadding="6" border="0">
<tr>
<td width="240"><b>Oxygen-evolving complex (OEC)</b></td>
</tr>
<tr>
<td align="center" width="240">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="Oxygen-evolving complex (OEC)"
height="180"
/>
<div><small>&nbsp;</small></div>
</td>
</tr>
</table>
</td>

<!-- Right: Areas & States -->
<td width="480" valign="top" colspan="2">
<table width="480" cellspacing="0" cellpadding="6" border="0">
<tr>
<td width="480"><b>Areas &amp; States</b></td>
</tr>
<tr>
<td align="center" width="480">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_Documentation_Tree.png"
alt="OEC — Areas &amp; States"
height="180"
/>
<div>
<small>Note: Pulling_area is not visible here as it is a large circle that does not fit the image here</small>
</div>
</td>
</tr>
</table>
</td>
</tr>

<!-- DESCRIPTION (full width = 720) -->
<tr>
<td colspan="3" valign="top" width="720">
<table width="720" cellspacing="0" cellpadding="6" border="0">
<tr>
<td width="720"><b>Description</b></td>
</tr>
<tr>
<td width="720">
<p>
The Oxygen-evolving complex (OEC), also called the water-splitting complex,
is the catalytic Mn<sub>4</sub>CaO<sub>5</sub> cluster of Photosystem&nbsp;II (PSII).
It oxidizes water, releasing molecular oxygen, protons, and electrons that
feed the PSII electron transfer chain.
</p>
<p><b>Overall reaction:</b> <code>2 H₂O → O₂ + 4 H⁺ + 4 e⁻</code></p>
</td>
</tr>
</table>
</td>
</tr>

<!-- BEHAVIOR (full width = 720, expanded to match code; no bullets) -->
<tr>
<td colspan="3" valign="top" width="720">
<table width="720" cellspacing="0" cellpadding="6" border="0">
<tr>
<td width="720"><b>Behavior in Simulation</b></td>
</tr>
<tr>
<td width="720">

  <p><b>Regions &amp; signals:</b> The OEC exposes two <code>Area2D</code> regions:
  <code>Pulling_area</code> (outer) and <code>Center</code> (inner). Signals
  <code>body_entered</code>/<code>body_exited</code> are wired to
  <code>body_entered_Water_pulling_area</code>, <code>body_entered_OEC_center</code>, etc.</p>

  <p><b>Water attraction (outer area):</b> When an H<sub>2</sub>O enters
  <code>Pulling_area</code>, it is added to
  <code>bodies_that_entered_Water_pulling_area</code> for 3&nbsp;s.
  Every frame, <code>pulling_of_water_to_OEC_center()</code> gently steers those
  water bodies toward the OEC using a LERP of strength ~0.05 toward the area’s
  center (<code>body.direction = lerp(...)</code>).</p>

  <p><b>Electron attraction:</b> Electrons in
  <code>electrons_that_are_pulled_to_OEC_center</code> are steered toward the OEC
  (LERP ~0.55 with slight horizontal jitter) by
  <code>pulling_of_electrons_to_OEC()</code>.
  When such an electron crosses the <code>Center</code>, it is added to
  <code>electrons_inside_OEC_center</code> and <code>OEC_is_electronised</code> is set true.</p>

  <p><b>Locking two waters at the center:</b> When an H<sub>2</sub>O reaches
  <code>Center</code>, OEC locks it into the first free slot
  (<code>first_H2O</code> then <code>second_H2O</code>):
  physics is paused, the body’s <code>CollisionShape2D</code> is disabled, an
  internal collision shape “copy” is added, and an offset is tracked so the
  body is smoothly lerped onto its anchor sprites
  (<code>first_H2O_PositionSprite</code>, <code>second_H2O_PositionSprite</code>).
  Locking invokes <code>releasing_of_electrons_from_OEC()</code>.</p>


  <p><b>Electron handoff to Tyrosine gate:</b>
  If at least one electron sits inside the OEC and the Tyrosine queue is free
  (<code>electrons_that_are_pulled_to_tyrosine_center.size() &lt; 1</code>),
  the first electron is moved from the OEC lists to
  <code>electrons_that_are_pulled_to_tyrosine_center</code>. This prevents
  multiple electrons stacking at Tyrosine. The handoff then triggers
  <code>delectronation_of_water()</code>.</p>

  <p><b>Stepwise water de-electronation (H<sub>2</sub>O → OH → O):</b>
  For each bound water, <code>delectronation_of_water()</code> performs a
  two-step sequence. At each step it spawns one electron near the corresponding
  position sprite and appends it to <code>electrons_that_are_pulled_to_OEC_center</code>;
  spawns one proton near that position sprite and increments the UI proton counter;
  then toggles the water’s sprite state (first
  <code>H2O_SimpleSprite → OH_SimpleSprite</code>, then
  <code>OH_SimpleSprite → O_SimpleSprite</code>). Across both waters this yields
  two electrons and two protons per water (four of each total), matching the overall
  chemistry over four PSII events.</p>

  <p><b>Releasing the O atoms (forming O<sub>2</sub>):</b>
  When both locked bodies display <code>O_SimpleSprite</code>, the OEC temporarily
  disables <code>Center</code> and <code>Pulling_area</code> monitoring, re-enables
  physics and collisions on the two locked bodies, moves them from group
  <code>"H2O"</code> to <code>"O"</code>, and frees the internal collision shape copies.
  After 1&nbsp;s, monitoring is re-enabled. A background routine
  <code>_pulling_of_singlet_Os_to_each_other()</code> (LERP ~0.05) then attracts
  single O atoms to their nearest neighbors so they meet and visually represent O<sub>2</sub>.
  (If you maintain an O<sub>2</sub> counter, increment it when the pair criteria are met.)</p>

  <p><b>Continuous positioning:</b> While locked,
  <code>_lerping_of_locked_particles_to_OEC()</code> lerps each water toward its
  anchor using <code>LOCKING_LERP</code> each frame, keeping visuals tight.</p>

</td>
</tr>
</table>
</td>
</tr>


<!-- SCRIPT LINK (full width = 720) -->
<tr>
<td colspan="3" valign="top" width="720">
<table width="720" cellspacing="0" cellpadding="6" border="0">
<tr>
<td width="720"><b>Script</b></td>
</tr>
<tr>
<td width="720">
<a href="../Project/Scripts/OEC.gd" target="_blank" rel="noopener noreferrer">View the OEC.gd script →</a>
</td>
</tr>
</table>
</td>
</tr>

</table>
