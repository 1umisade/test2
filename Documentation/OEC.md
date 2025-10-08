<h1 align="center">Oxygen-evolving complex (OEC)</h1>

<p align="center">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="Oxygen-evolving complex (OEC)"
height="300"
/>
</p>
<div align="center">
<div style="display:inline-block; max-width:900px;"> 
  The Oxygen-evolving complex (OEC), also called the water-splitting complex, is the catalytic Mn<sub>4</sub>CaO<sub>5</sub> cluster of 
  Photosystem II. It oxidizes water, releasing molecular oxygen, protons, and electrons that feed the PSII electron transfer chain. 
</div> 
</div>


<p align="center"><b>Overall reaction:</b> <code>2 H₂O → O₂ + 4 H⁺ + 4 e⁻</code></p>



<!-- 3) SIMULATED BEHAVIOR (four stacked rows; each row = image left, text right) -->
<table width="1000" align="center" cellspacing="0" cellpadding="6" border="0">
<!-- Title row (only here) -->
<tr>
<td colspan="2" align="center" width="1000" style="background-color:#111; color:white;">
<b>Simulated behavior</b>
</td>
</tr>

<!-- Row 1 -->
<tr>
<td width="400" valign="top" align="center">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="OEC step 1"
height="140"
/>
</td>
<td width="600" valign="middle">
<p><b>Step&nbsp;1 – Attraction:</b> H<sub>2</sub>O molecules are pulled toward the OEC through
<code>Pulling_area</code> and begin to approach the <code>Center</code>.</p>
</td>
</tr>

<!-- Row 2 -->
<tr>
<td width="400" valign="top" align="center">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="OEC step 2"
height="140"
/>
</td>
<td width="600" valign="middle">
<p><b>Step&nbsp;2 – Locking:</b> Two waters reach the <code>Center</code>, pause physics, disable their
colliders, and smoothly lock to anchor positions.</p>
</td>
</tr>

<!-- Row 3 -->
<tr>
<td width="400" valign="top" align="center">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="OEC step 3"
height="140"
/>
</td>
<td width="600" valign="middle">
<p><b>Step&nbsp;3 – Oxidation:</b> The routine <code>deelectronation_of_H2O()</code> runs in two steps per water
(H<sub>2</sub>O→OH→O), spawning electrons to the chain and protons to the lumen.</p>
</td>
</tr>

<!-- Row 4 -->
<tr>
<td width="400" valign="top" align="center">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="OEC step 4"
height="140"
/>
</td>
<td width="600" valign="middle">
<p><b>Step&nbsp;4 – Release:</b> When both sites show O, monitoring resumes, atoms are freed as “O” bodies,
and nearby O’s are gently steered together to visualize O<sub>2</sub> formation.</p>
</td>
</tr>
</table>



<!-- 4) AREAS & STATES (tree image preserved) -->
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
