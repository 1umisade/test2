<!-- 1) TITLE -->
<h1 align="center">Oxygen-evolving complex</h1>

<!-- 2) TOP ROW: OEC image (left) | Description (right) -->
<table width="1000" align="center" cellspacing="0" cellpadding="6" border="0">
<!-- Title row -->
<tr>
<td colspan="2" align="center" width="1000" style="background-color:#111; color:white;">
<b>Oxygen-evolving complex (OEC)</b>
</td>
</tr>

<tr>
<!-- Left cell -->
<td width="400" valign="top">
<div align="center" style="margin-top:6px;">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="Oxygen-evolving complex (OEC)"
height="180"
/>
</div>
</td>

<!-- Right cell: DESCRIPTION -->
<td width="600" valign="middle" align="center">
<div style="max-width:500px; text-align:center; margin:auto;">
<p>
The Oxygen-evolving complex (OEC), also called the water-splitting complex,
is the catalytic Mn<sub>4</sub>CaO<sub>5</sub> cluster of Photosystem&nbsp;II (PSII).
It oxidizes water, releasing molecular oxygen, protons, and electrons that
feed the PSII electron transfer chain.
</p>
<p><b>Overall reaction:</b> <code>2 H₂O → O₂ + 4 H⁺ + 4 e⁻</code></p>
</div>
</td>
</tr>
</table>

<!-- 3) SIMULATED BEHAVIOR (new structured version) -->
<table width="1000" align="center" cellspacing="0" cellpadding="6" border="0">
<!-- Title row -->
<tr>
<td colspan="2" align="center" width="1000" style="background-color:#111; color:white;">
<b>Simulated behavior</b>
</td>
</tr>

<tr>
<!-- Left cell: Four vertically stacked images -->
<td width="400" valign="top" align="center">
<div style="margin-top:6px;">
<img
src=“../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png”
alt="OEC behavior step 1"
height="120"
style="display:block; margin-bottom:8px;"
/>
<img
src="../Project/Graphics/Oxygen-evolving_complex/OEC_Behavior_2.png"
alt="OEC behavior step 2"
height="120"
style="display:block; margin-bottom:8px;"
/>
<img
src="../Project/Graphics/Oxygen-evolving_complex/OEC_Behavior_3.png"
alt="OEC behavior step 3"
height="120"
style="display:block; margin-bottom:8px;"
/>
<img
src="../Project/Graphics/Oxygen-evolving_complex/OEC_Behavior_4.png"
alt="OEC behavior step 4"
height="120"
style="display:block;"
/>
</div>
</td>

<!-- Right cell: Explanatory text -->
<td width="600" valign="middle">
<div style="max-width:540px; text-align:left; margin:auto;">
<p>
The simulation models the dynamic sequence of events inside the Oxygen-evolving complex (OEC).
Water molecules enter the complex, bind at specific sites, and undergo progressive oxidation,
releasing protons and electrons that feed Photosystem II.
</p>

<p>
Each image on the left represents a major step:
</p>

<ol>
<li><b>Step 1:</b> H<sub>2</sub>O molecules are drawn toward the OEC center through <code>Pulling_area</code>.</li>
<li><b>Step 2:</b> Bound waters lose electrons to the manganese cluster, forming OH intermediates.</li>
<li><b>Step 3:</b> Further oxidation yields O atoms ready to pair into molecular oxygen.</li>
<li><b>Step 4:</b> O<sub>2</sub> release and restoration of the catalytic site.</li>
</ol>

<p>
Each phase corresponds to one or more transitions in the <code>deelectronation_of_H2O()</code> routine,
which spawns protons and electrons and updates molecule visuals frame by frame.
</p>
</div>
</td>
</tr>
</table>

<!-- 4) AREAS & STATES -->
<table width="1000" align="center" cellspacing="0" cellpadding="6" border="0">
<tr>
<td align="center" style="background-color:#111; color:white;">
<b>Areas &amp; States</b>
</td>
</tr>
<tr>
<td align="center">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_Documentation_Tree.png"
alt="OEC — Areas &amp; States"
height="180"
/>
<div><small></small></div>
</td>
</tr>
</table>

<!-- 5) SCRIPT LINK -->
<table width="720" align="center" cellspacing="0" cellpadding="6" border="0">
<tr>
<td align="center" style="background-color:#111; color:white;">
<b>Script</b>
</td>
</tr>
<tr>
<td align="center">
<a href="../Project/Scripts/OEC.gd" target="_blank" rel="noopener noreferrer">
View the OEC.gd script →
</a>
</td>
</tr>
</table>


