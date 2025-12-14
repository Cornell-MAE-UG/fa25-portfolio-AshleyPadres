---
layout: project
title: Wind Turbine Blade Optimization
description: MAE 4272 Final Report
technologies: [Matlab]
image: /assets/images/radio-machine-cad.jpg
---

from pathlib import Path

html = r"""
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Blade Design Final Report – MAE 4272</title>

<!-- MathJax -->
<script>
window.MathJax = {
  tex: { inlineMath: [['$', '$']] },
  svg: { fontCache: 'global' }
};
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js"></script>

<style>
body {
  font-family: "Times New Roman", Times, serif;
  margin: 0;
  padding: 0;
  background: white;
  color: black;
}

.container {
  max-width: 900px;
  margin: auto;
  padding: 40px 24px;
}

h1 { text-align: center; font-size: 20pt; }
h2 { font-size: 14pt; margin-top: 28px; }
h3 { font-size: 12pt; margin-top: 20px; }

p, li {
  font-size: 12pt;
  line-height: 1.5;
  text-align: justify;
}

.authors {
  text-align: center;
  margin-bottom: 30px;
}

.equation {
  text-align: center;
  margin: 12px 0;
}

.figure {
  text-align: center;
  font-style: italic;
  margin: 20px 0;
  border: 1px dashed #aaa;
  padding: 12px;
}

table {
  width: 100%;
  border-collapse: collapse;
  font-size: 11pt;
}

th, td {
  border: 1px solid black;
  padding: 6px;
  text-align: center;
}
</style>
</head>

<body>
<div class="container">

<h1>Blade Design Final Report</h1>

<div class="authors">
MAE 4272, Fall 2025<br>
Lab 408, Group 3, Blade 83<br>
Ashley Padres, Julia Deffner, Ella Yellin, Anna-Sophie Schaldenbrand<br>
December 12, 2025
</div>

<h2>1. Executive Summary</h2>

<p>
This report outlines the process of designing and testing a small horizontal-axis wind turbine to maximize extracted power under an oncoming wind velocity distribution. Specifically, the wind turbine is optimized for an oncoming wind velocity of 4.8 m/s, corresponding to the average velocity that maximizes extracted power under the experienced Weibull distribution.
</p>

<p>
A MATLAB model was developed to optimize the blade design. This included selecting an airfoil (NACA 4412), determining chord length and pitch distributions, solving for aerodynamic forces and structural stresses, predicting power curves, and iterating to determine the optimal design RPM.
</p>

<p>
The final design predicted a maximum power extraction of 3.61 W at 1050 RPM. Experimental testing at five wind speeds showed reduced power output and increased operating RPM, with a maximum measured power of 1.8 W at 5.8 m/s.
</p>

<h2>2. Context, Objectives, and Constraints</h2>

<p>
The objective was to design a small-scale horizontal-axis wind turbine that maximizes power extraction while meeting geometric, material, and operational constraints.
</p>

<ul>
<li>Maximum blade length: 6 in</li>
<li>Maximum axial hub clearance: 2 in</li>
<li>Material: Accura 25</li>
<li>Torque brake limit: 0.035 Nm</li>
<li>Free spin limit: 3500 RPM</li>
</ul>

<h2>3. Design Process and Assumptions</h2>

<div class="figure">Figure 1. Design process flowchart (placeholder)</div>

<h3>3.1 Weibull Distribution Optimization</h3>

<div class="equation">$$P = F \cdot U$$</div>

<div class="equation">
$$P \sim k \cdot U^2 \cdot U = k \cdot U^3$$
</div>

<div class="equation">
$$k = \frac{1}{2}\rho A C_p$$
</div>

<div class="equation">
$$P_{\text{Total Avg}} = \int_{0}^{15} P(U)\,p(U)\,dU$$
</div>

<div class="equation">
$$p(U) = \frac{k}{c}\left(\frac{U}{c}\right)^{k-1}
\exp\left[-\left(\frac{U}{c}\right)^k\right]$$
</div>

<div class="equation">
$$U_{\text{Total Avg, eff}} = \left(\frac{3}{k}\right)^{1/k}$$
</div>

<div class="equation">
$$U_{\text{Total Avg, eff}} = 4.82\ \text{m/s}$$
</div>

<h3>3.2 Airfoil Selection</h3>

<p>
Based on literature review and lift-to-drag ratio analysis at a Reynolds number of 50,000, the NACA 4412 airfoil was selected due to superior $C_L/C_D$ performance at low angles of attack.
</p>

<div class="figure">Figure 2. $C_L/C_D$ vs. angle of attack (placeholder)</div>

<h3>3.3 Blade Geometry</h3>

<div class="equation">
$$c(r) = -0.2461r + 0.0563$$
</div>

<h3>3.4 Pitch Distribution</h3>

<div class="equation">
$$\phi = \tan^{-1}\left(\frac{U(1-a)}{\omega r (1+a')}\right)$$
</div>

<div class="equation">
$$\alpha = \phi - \theta$$
</div>

<div class="equation">
$$\theta(r) \approx 89.7 e^{-26.7r}$$
</div>

<h3>3.5 Forces and Structural Analysis</h3>

<div class="equation">
$$V_{rel} = \sqrt{(U(1-a))^2 + (\omega r (1+a'))^2}$$
</div>

<div class="equation">
$$F_t = \frac{1}{2}\rho V_{rel}^2 c(r)(C_L \sin\phi - C_D \cos\phi)$$
</div>

<div class="equation">
$$F_x = \frac{1}{2}\rho V_{rel}^2 c(r)(C_L \cos\phi + C_D \sin\phi)$$
</div>

<div class="equation">
$$M(r) = \int_r^{r_{tip}} F_x(r')(r'-r)\,dr'$$
</div>

<div class="equation">
$$\sigma(r) = \frac{M(r)y(r)}{I(r)}$$
</div>

<div class="figure">Figures 3–6. Model outputs and CAD renderings (placeholders)</div>

<h2>4. Testing Approach</h2>

<div class="figure">Figure 7. Experimental procedure flowchart (placeholder)</div>

<p>
Testing was conducted in a wind tunnel at five wind speeds: 4.1, 4.8, 4.9, 5.3, and 5.8 m/s. Torque brake voltage was increased incrementally until stall while monitoring RPM limits.
</p>

<h2>5. Results</h2>

<div class="figure">Figures 8–11. Experimental and model power curves (placeholders)</div>

<table>
<tr>
<th>Wind Speed</th>
<th>Predicted Max Power</th>
<th>Experimental Max Power</th>
<th>% Error</th>
</tr>
<tr>
<td>4.8 m/s</td>
<td>3.61 W</td>
<td>0.70 W</td>
<td>81%</td>
</tr>
<tr>
<td>5.8 m/s</td>
<td>6.50 W</td>
<td>1.80 W</td>
<td>72%</td>
</tr>
</table>

<div class="figure">Figures 12–13. Weibull distribution comparison (placeholders)</div>

<h2>6. Conclusion</h2>

<p>
The final blade achieved a maximum measured output of 1.8 W and demonstrated the effectiveness of aerodynamic optimization. Discrepancies between predicted and experimental results highlight the need for improved modeling fidelity.
</p>

</div>
</body>
</html>
"""

Path("index.html").write_text(html, encoding="utf-8")
print("index.html generated")
