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
The oxygen-evolving complex is an Mn<sub>4</sub>CaO<sub>5</sub> cluster within photosystem II. It is the very molecule that<br>
binds and de-electronises water to provide electrons for the photosynthetic electron transfer chain.
<br> Water de-electronation also results in release of protons and O₂ inside the thylakoids.
</div> 
</div>

<br><br>

<!-- 3) SIMULATED BEHAVIOR -->
<table width="1000" align="center" cellspacing="0" cellpadding="6" border="0">
<tr>
<td colspan="2" align="center" style="background-color:#111; color:white;">
<b>Simulated behavior</b>
</td>
</tr>

<!-- Step 1 -->
<tr>
<td width="400" valign="top" align="center">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="OEC step 1"
height="140"
/>
</td>
<td width="600" valign="middle">
<p style="margin:0;">
<b>Binding of water:</b> Two H₂O molecules bind to the oxygen-evolving complex.
<a href="SOURCES.md#H₂O molecules are pulled toward the OEC through the Pulling_area and begin to approach the Center" target="_blank" rel="noopener noreferrer" title="Open source for this claim">🔎</a>
</p>
</td>
</tr>

<!-- Step 2 -->
<tr>
<td width="400" valign="top" align="center">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="OEC step 2"
height="140"
/>
</td>
<td width="600" valign="middle">
<p style="margin:0;">
<b>Step&nbsp;2 – Locking:</b> Two waters reach the <code>Center</code>, pause physics, disable their
colliders, and smoothly lock to anchor positions.
<a href="../SOURCES.md#oec-step-2-locking" target="_blank" rel="noopener noreferrer" title="Open source for this claim">🔎</a>
</p>
</td>
</tr>

<!-- Step 3 -->
<tr>
<td width="400" valign="top" align="center">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="OEC step 3"
height="140"
/>
</td>
<td width="600" valign="middle">
<p style="margin:0;">
<b>Step&nbsp;3 – Oxidation:</b> The routine <code>deelectronation_of_H2O()</code> runs in two steps per water
(H<sub>2</sub>O → OH → O), spawning electrons to the chain and protons to the lumen.
<a href="../SOURCES.md#oec-step-3-oxidation" target="_blank" rel="noopener noreferrer" title="Open source for this claim">🔎</a>
</p>
</td>
</tr>

<!-- Step 4 -->
<tr>
<td width="400" valign="top" align="center">
<img
src="../Project/Graphics/Oxygen-evolving_complex/oxygen_evolving_complex_SimpleSprite.png"
alt="OEC step 4"
height="140"
/>
</td>
<td width="600" valign="middle">
<p style="margin:0;">
<b>Step&nbsp;4 – Release:</b> When both sites show O, monitoring resumes, atoms are freed as “O” bodies,
and nearby O’s are gently steered together to visualize O<sub>2</sub> formation.
<a href="../SOURCES.md#oec-step-4-release" target="_blank" rel="noopener noreferrer" title="Open source for this claim">🔎</a>
</p>
</td>
</tr>


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

