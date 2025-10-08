<!-- 1) TITLE -->
<table width="720" align="center" cellspacing="0" cellpadding="6" border="0">
<tr>
<td align="center" width="720">
  <b style="font-size:20px;">Oxygen-evolving complex</b>
</td>
</tr>
</table>

<!-- 2) TOP ROW: OEC image (left) | Areas & States (right) -->
<table width="720" align="center" cellspacing="0" cellpadding="6" border="0">
<tr>
<!-- Left cell -->
<td width="240" valign="top">
  <b>Oxygen-evolving complex (OEC)</b>
  <div align="center" style="margin-top:6px;">
    <img
      src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
      alt="Oxygen-evolving complex (OEC)"
      height="180"
    />
  </div>
</td>

<!-- Right cell -->
<td width="480" valign="top">
  <b>Areas &amp; States</b>
  <div align="center" style="margin-top:6px;">
    <img
      src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_Documentation_Tree.png"
      alt="OEC — Areas &amp; States"
      height="180"
    />
    <div><small>Note: Pulling_area is not visible here as it is a large circle that does not fit the image here</small></div>
  </div>
</td>
</tr>
</table>

<!-- 3) DESCRIPTION -->
<table width="720" align="center" cellspacing="0" cellpadding="6" border="0">
<tr><td><b>Description</b></td></tr>
<tr>
<td>
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

<!-- 4) BEHAVIOR -->
<table width="720" align="center" cellspacing="0" cellpadding="6" border="0">
<tr><td><b>Behavior in Simulation</b></td></tr>
<tr>
<td>

  <p><b>Regions &amp; signals:</b> The OEC exposes two <code>Area2D</code> regions:
  <code>Pulling_area</code> (outer) and <code>Center</code> (inner). Signals
  <code>body_entered</code>/<code>body_exited</code> are wired to
  <code>body_entered_Water_pulling_area</code>, <code>body_entered_OEC_center</code>, etc.</p>

  <p><b>Water attraction (outer area):</b> When an H<sub>2</sub>O enters
  <code>Pulling_area</code>, it is added to
  <code>bodies_that_entered_Water_pulling_area</code> for 3&nbsp;s.
  Every frame, <code>pulling_of_water_to_OEC_center()</code> gently steers those
  water bodies toward the OEC using a LERP of ~0.05 toward the area’s center.</p>

  <p><b>Electron attraction:</b> Electrons in
  <code>electrons_that_are_pulled_to_OEC_center</code> are steered toward the OEC
  (LERP ~0.55 with slight horizontal jitter) by
  <code>pulling_of_electrons_to_OEC()</code>.
  On crossing <code>Center</code>, they move to
  <code>electrons_inside_OEC_center</code> and set <code>OEC_is_electronised = true</code>.</p>

  <p><b>Locking two waters at the center:</b> When an H<sub>2</sub>O reaches
  <code>Center</code>, it locks into the first free slot (then the second):
  physics paused, <code>CollisionShape2D</code> disabled, a collision “copy” is added,
  and the body lerps onto its anchor sprite.</p>

  <p><b>Electron handoff to Tyrosine gate:</b>
  If at least one electron is inside the OEC and the Tyrosine queue is free
  (<code>electrons_that_are_pulled_to_tyrosine_center.size() &lt; 1</code>),
  an electron is moved to that queue, then <code>delectronation_of_water()</code> runs.</p>

  <p><b>Stepwise water de-electronation (H<sub>2</sub>O → OH → O):</b>
  Each step spawns one electron and one proton near the position sprite, toggling
  sprites from H<sub>2</sub>O → OH → O. Across both waters this yields four e⁻ and four H⁺ in total.</p>

  <p><b>Releasing the O atoms (forming O<sub>2</sub>):</b>
  Once both show <code>O_SimpleSprite</code>, monitoring pauses, physics/collisions are restored,
  groups switch from <code>"H2O"</code> to <code>"O"</code>, and the copies are freed.
  A background routine then gently attracts O atoms so they meet (visual O<sub>2</sub>).</p>

  <p><b>Continuous positioning:</b> While locked,
  <code>_lerping_of_locked_particles_to_OEC()</code> lerps each water toward its anchor
  using <code>LOCKING_LERP</code> each frame.</p>

</td>
</tr>
</table>

<!-- 5) SCRIPT LINK -->
<table width="720" align="center" cellspacing="0" cellpadding="6" border="0">
<tr><td><b>Script</b></td></tr>
<tr>
<td>
  <a href="../Project/Scripts/OEC.gd" target="_blank" rel="noopener noreferrer">View the OEC.gd script →</a>
</td>
</tr>
</table>
