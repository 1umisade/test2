<!-- OEC.md (pure HTML, narrower) -->

<table width="720" align="center" cellspacing="0" cellpadding="6" border="0">
<tr>
  <!-- 1) IMAGE (left) -->
  <td width="240" valign="top">
    <table width="240" cellspacing="0" cellpadding="6" border="1">
      <tr>
        <th align="left">Oxygen-evolving complex (OEC)</th>
      </tr>
      <tr>
        <td align="center">
          <img src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
               alt="Oxygen-evolving complex (OEC)" height="180" />
          <div><small>Part of Photosystem&nbsp;II; lumenal side</small></div>
        </td>
      </tr>
    </table>
  </td>

  <!-- 2) DESCRIPTION (middle) -->
  <td width="240" valign="top">
    <table width="240" cellspacing="0" cellpadding="6" border="1">
      <tr>
        <th align="left">Description</th>
      </tr>
      <tr>
        <td>
          <p>
            The Oxygen-evolving complex (OEC), also called the water-splitting complex,
            is the catalytic Mn<sub>4</sub>CaO<sub>5</sub> cluster of Photosystem&nbsp;II (PSII).
            It oxidizes water, releasing molecular oxygen, protons, and electrons that
            feed the PSII electron transfer chain.
          </p>
          <p>
            <b>Overall reaction:</b>
            <code>2 H₂O → O₂ + 4 H⁺ + 4 e⁻</code>
          </p>
          <p>
            The OEC advances through the Kok S-state cycle (S<sub>0</sub>→S<sub>1</sub>→S<sub>2</sub>→S<sub>3</sub>→S<sub>4</sub>→S<sub>0</sub>),
            driven by four successive PSII charge-separation events (photons). Electrons
            are transferred via the redox-active tyrosine (Y<sub>Z</sub>) to P680<sup>+</sup>.
          </p>
        </td>
      </tr>
    </table>
  </td>

  <!-- 3) BEHAVIOR IN SIMULATION (right) -->
  <td width="240" valign="top">
    <table width="240" cellspacing="0" cellpadding="6" border="1">
      <tr>
        <th align="left">Behavior in Simulation</th>
      </tr>
      <tr>
        <td>
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
          <pre>
for each PSII_photon:
OEC.advance_S_state()
if OEC.at_S4() and H2O >= 2:
  consume(2 × H2O)
  spawn(1 × O2)
  spawn(4 × H+)
  deliver_electrons(4)
  OEC.reset_to_S0()
          </pre>
        </td>
      </tr>
    </table>
  </td>
</tr>
</table>
