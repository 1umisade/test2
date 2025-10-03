<!-- OEC.md (pure HTML, images row + two full-width tables; images same height, NO OUTER BORDER) -->

<table width="720" align="center" cellspacing="0" cellpadding="6" border="0"
      role="presentation"
      style="border:0; outline:0; border-collapse:separate; border-spacing:0; box-shadow:none; background:transparent;">
<!-- TOP ROW: Left = OEC image (240) | Right = Combined Areas & States (480) -->
<tr style="border:0;">
  <!-- Left: OEC image -->
  <td width="240" valign="top" style="border:0; padding:6px;">
    <table width="240" cellspacing="0" cellpadding="6" border="1">
      <tr><th align="left">Oxygen-evolving complex (OEC)</th></tr>
      <tr>
        <td align="center">
          <img src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
                alt="Oxygen-evolving complex (OEC)" height="180" />
          <div><small></small></div>
        </td>
      </tr>
    </table>
  </td>

  <!-- Right: Areas & States (wider image) -->
  <td width="480" valign="top" colspan="2" style="border:0; padding:6px;">
    <table width="480" cellspacing="0" cellpadding="6" border="1">
      <tr><th align="left">Areas &amp; States</th></tr>
      <tr>
        <td align="center">
          <img src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_Documentation_Tree.png"
                alt="OEC — Areas &amp; States" height="180" />
          <div><small>Note: Pulling_area is not visible here as it is a large circle that does not fit the image here</small></div>
        </td>
      </tr>
    </table>
  </td>
</tr>

<!-- DESCRIPTION -->
<tr style="border:0;">
  <td colspan="3" valign="top" width="720" style="border:0; padding:6px;">
    <table width="720" cellspacing="0" cellpadding="6" border="1">
      <tr><th align="left" width="720">Description</th></tr>
      <tr>
        <td>
          <p>
            The Oxygen-evolving complex (OEC), also called the water-splitting complex,
            is the catalytic Mn<sub>4</sub>CaO<sub>5</sub> cluster of Photosystem&nbsp;II (PSII).
            It oxidizes water, releasing molecular oxygen, protons, and electrons that
            feed the PSII electron transfer chain.
          </p>
          <p><b>Overall reaction:</b> <code>2 H₂O → O₂ + 4 H⁺ + 4 e⁻</code></p>
          <p>
            The OEC advances through the Kok S-state cycle
            (S<sub>0</sub>→S<sub>1</sub>→S<sub>2</sub>→S<sub>3</sub>→S<sub>4</sub>→S<sub>0</sub>),
            driven by four successive PSII charge-separation events (photons). Electrons
            are transferred via the redox-active tyrosine (Y<sub>Z</sub>) to P680<sup>+</sup>.
          </p>
        </td>
      </tr>
    </table>
  </td>
</tr>

<!-- BEHAVIOR -->
<tr style="border:0;">
  <td colspan="3" valign="top" width="720" style="border:0; padding:6px;">
    <table width="720" cellspacing="0" cellpadding="6" border="1">
      <tr><th align="left" width="720">Behavior in Simulation</th></tr>
      <tr>
        <td width="720">
          <ul>
            <li><b>Inputs:</b> 4 PSII photon events; 2 × H₂O entities available.</li>
            <li><b>Outputs:</b> 1 × O₂ entity, 4 × H⁺ entities, 4 e⁻ to PSII chain.</li>
            <li><b>Progression:</b> Each PSII photon advances the OEC S-state by +1.</li>
            <li><b>Trigger:</b> At S<sub>4</sub>, consume 2 H₂O, spawn 1 O₂, emit 4 H⁺ to lumen,
                deliver 4 e⁻ toward P680/Pheophytin, then reset to S<sub>0</sub>.</li>
            <li><b>Counts/UI:</b> Increment O₂ and H⁺ counters; decrement H₂O by 2.</li>
            <li><b>Failure case:</b> If H₂O &lt; 2 at S<sub>4</sub>, wait until available.</li>
            <li><b>Placement:</b> Lumen-facing; proton spawn direction upward.</li>
          </ul>
          <p><b>Pseudo-event flow:</b></p>
          <pre>for each PSII_photon:
OEC.advance_S_state()
if OEC.at_S4() and H2O &gt;= 2:
consume(2 × H2O)
spawn(1 × O2)
spawn(4 × H+)
deliver_electrons(4)
OEC.reset_to_S0()</pre>
        </td>
      </tr>
    </table>
  </td>
</tr>

<!-- SCRIPT LINK -->
<tr style="border:0;">
  <td colspan="3" valign="top" width="720" style="border:0; padding:6px;">
    <table width="720" cellspacing="0" cellpadding="6" border="1">
      <tr><th align="left">Script</th></tr>
      <tr>
        <td>
          <a href="../Project/Scripts/OEC.gd" target="_blank" rel="noopener noreferrer">View the OEC.gd script →</a>
        </td>
      </tr>
    </table>
  </td>
</tr>
</table>
