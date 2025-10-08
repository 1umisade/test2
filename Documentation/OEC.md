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
