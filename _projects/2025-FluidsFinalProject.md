---
layout: project
title: Wind Turbine Optimization
description: MAE 4272 Final Report
technologies: [Matlab]
image: /assets/images/windturbine.jpg
---


<html lang="en">
<head>
<meta charset="UTF-8">
<title>Wind Turbine Blade Design Summary</title>

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

h1 {
  text-align: center;
  font-size: 20pt;
}

p {
  font-size: 12pt;
  line-height: 1.5;
  text-align: justify;
}
</style>
</head>

<body>
<div class="container">

<h1>Wind Turbine Blade Design Summary</h1>

<p>
This project focused on the design and experimental validation of a small horizontal-axis wind turbine blade optimized to maximize power extraction under a realistic wind speed distribution. A Weibull probability model was used to identify the wind speed that contributes most strongly to average power production, leading to a design wind speed of approximately 4.8 m/s. A MATLAB-based aerodynamic model was developed to guide blade geometry selection, operating conditions, and predicted performance prior to manufacturing and testing.
</p>

<p>
Airfoil selection and blade geometry were driven by aerodynamic efficiency at low Reynolds numbers and by manufacturing and safety constraints. Several candidate airfoils were evaluated, and the NACA 4412 airfoil was selected due to its high lift-to-drag ratio over a broad range of angles of attack, with a peak near 9 degrees. The blade length was set to the maximum allowable 6 inches, with a tapered chord distribution set from a taper ratio of 4, chosen to balance structural integrity near the hub with reduced aerodynamic losses near the tip. A spanwise twist distribution was then calculated to maintain the optimal angle of attack of 9 degrees along the blade at the design operating condition.
</p>

<div class="figure">
  <img src="../../assets/images/figure34.png" style="max-width:100%;">
  <br>Figure 1. Model outputs, Predicted power vs RPM (left) and Bending stress distribution (right) 
</div>

<p>
The final design RPM was determined by iterating through candidate rotational speeds and evaluating predicted power output, torque, free-spin speed, and bending stress while enforcing operational limits. The optimized design operated at a predicted 1050 RPM and was expected to produce approximately 3.6 W at the design wind speed while remaining safely below torque, speed, and material stress limits.
</p>


<p>
During wind tunnel testing, the blade successfully extracted power across a range of wind speeds from 4.1 to 5.8 m/s. The maximum measured power was 1.8 W at 5.8 m/s, and the blade had an optimal operating rotation speed of approximately 1770 RPM, higher than the model predicted. Observed differences between model and experiment were attributed to unmodeled effects such as friction, tip losses, and approximated induction factors. Power curves showed expected trends, with higher wind speeds producing increased torque and RPM, although the blade experienced slight resonant effects at mid-range speeds. Overall, the blade demonstrated robust performance, validating the design methodology and highlighting areas for improving predictive accuracy in future models.
</p>

<div class="figure">
  <img src="../../assets/images/figure89.png" style="max-width:100%;">
  <br>Figure 2, Experimental data: Power vs. RPM (Left), Power vs wind speed (Right) at different RPMs is marked by the dashed line.
</div>

<p>
Despite the discrepancies in absolute power and rotational speed, the results confirm that systematic optimization of airfoil selection, taper, and twist produces a functional turbine blade capable of extracting meaningful power under realistic operating conditions. As I lead the development process of the iterative matlab code to inform our design choices and verify these safety operations, it was satisfying to confirm relative success of the model. 
</p>

<p>
See below for more thorough breakdown of the design and testing results.
</p>

</div>
</body>
</html>



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

<div style="height: 50px;"></div>
<div style="height: 50px;"></div>
<div style="height: 50px;"></div>
<div style="height: 50px;"></div>
<div style="height: 50px;"></div>
<div style="height: 50px;"></div>

<h1>Blade Design Final Report</h1>

<div class="authors">
MAE 4272, Fall 2025<br>
Lab 408, Group 3, Blade 83<br>
Ashley Padres, Julia Deffner, Ella Yellin, Anna-Sophie Schaldenbrand<br>
December 12, 2025
</div>

<h2>1. Executive Summary</h2>

<p>
This report outlines the process of designing and testing a small horizontal-axis wind turbine to maximize extracted power under an oncoming wind velocity distribution. Specifically, the wind turbine is optimized for use in an oncoming wind velocity of 4.8 m/s, the average velocity that would extract max power under its experienced Weibull distribution of velocities.
</p>

<p>
To design the blade, a MATLAB model was developed to optimize the design. This included selecting an airfoil designation of NACA 4412, determining chord length and pitch as a function of radius, solving for the forces and stresses experienced by the blade, predicting output power curves, and iterating to determine the design angular velocity.
</p>

<p>
The chosen design predicted a design RPM of 1050 that would extract 3.61 W at an oncoming wind speed of 4.82 m/s. The designed wind turbine was then tested at five different oncoming wind speeds, and experimental power graphs were recorded for each.
</p>

<p>
Comparing the model predicted behavior with the experimental behavior, the actual wind turbine produced less power but spun faster, likely a result of the model’s assumptions. The maximum power extracted observed was 1.8 W at an oncoming wind speed of 5.8 m/s.
</p>

<p>
Ultimately, while the wind turbine underperformed relative to what the model predicted, the performance demonstrates how optimizing the taper, twist, and CL/CD can result in a blade that maximizes power output under a Weibull distribution.
</p>


<h2>2. Context, Objectives, and Constraints</h2>

<p>
Our objective was to design a small-scale horizontal-axis wind turbine that extracts maximum power from oncoming wind, while conforming to several constraints related to geometry, material, and operating conditions.
</p>

<p>
Our geometric, material, and operational constraints were as follows:
</p>

<p><strong>Geometric:</strong></p>

<ul>
<li>Max blade length, from root to tip: 6in</li>
<li>Maximum axial distance of the blade at the hub to remain clear of the nacelle: 2in</li>
<li>Blade must interface accurately with hub mounting</li>
</ul>

<p><strong>Other:</strong></p>

<ul>
<li>Material: Accura 25</li>
<li>Blade must optimize power under wind speeds defined by a Weibull probability function</li>
<li>Turbine must be designed to optimize power for a chosen RPM</li>
<li>Operations must not put the torque break or blades at risk of failure</li>
</ul>


<h2>3. Design Process and Assumptions</h2>

<p>
To achieve our objectives, we needed to determine our blade geometry and operating conditions to optimize output power while staying within the bounds of safe operation. To do this, we followed the general procedure:
</p>

<div class="figure">
  <img src="../../assets/images/figure1.png" style="max-width:60%;">
  <br>Figure 1. Design process flowchart
</div>


<h3>1. Account for Weibull Distribution:</h3>

<p>
First, we utilized the Weibull distribution to determine what wind velocity our blade should be optimized for. By solving for total power, we determined what velocity (following this distribution) would produce the maximum average power:
</p>

<div class="equation">$$P = F U$$</div>

<div class="equation">
$$P \propto k U^2 U = k U^3 \quad \text{where } k=\frac{1}{2}\rho A C_p$$
</div>

<div class="equation">
$$P_{Total Avg}=\int_{0\ \text{m/s}}^{15\ \text{m/s}} P(U)p(U)\,dU,
\quad \text{where } p(U)=\frac{k}{c}\left(\frac{U}{c}\right)^{k-1}
\exp\left[-\left(\frac{U}{c}\right)^k\right]$$
</div>

<div class="equation">
$$U_{Total Avg,\ eff}=\left(\frac{3}{k}\right)^{1/k}=3^{1/1.7}\ \text{m/s}=4.82\ \text{m/s}$$
</div>

<p>
Thus, we want to design our wind turbine to maximize power generation at an effective axial wind velocity of 4.82 m/s. With our design wind velocity determined, the next step is to determine the optimal airfoil to proceed with.
</p>

<h3>2. Choose Airfoil Geometry:</h3>

<p>
To choose our airfoil shape, we researched optimal NACA airfoil designs for small horizontal axis wind turbines at low oncoming wind speeds. One paper we found designates NACA 6409, NACA 6412, and NACA 4412 to be the three most efficient airfoils for a wind turbine around 11.6 m/s.
</p>

<p>
We then plotted these three airfoils at a Re of 50,000, which we are assuming will sufficiently represent our blade’s operating conditions, and chose the one with the highest CL/CD for a small range of AOA’s: NACA 4412.
</p>

<div class="figure">
  <img src="../../assets/images/figure2.png" style="max-width:70%;">
  <br>Figure 2. Plot of Cl/Cd vs Alpha for three airfoils, obtained from airfoiltools.com. (placeholder)
</div>


<p>
The NACA 4412 appears to have the highest lift drag ratio for the majority of AOA’s, and specifically has a maximum lift-to-drag ratio at an angle of attack of 9 degrees, a key input for the next step of our design process.
</p>

<h3>3. Calculate / Determine Key Blade Parameters</h3>

<h3>3a. Assign geometric parameters</h3>

<p>
By maximizing our other geometrical constraints to maximize potential output torque, we set the blade length to be 6’’ and its chord length at the hub to be 1.97’’. With this, the final geometric feature determined from research was our taper ratio, from which we found a taper ratio of 4 would be sufficient. From this, we get a linear chord distribution of:
</p>

<div class="equation">$$chord(r)=-0.2461r+0.0563$$</div>

<h3>3b. Calculate geometric parameters</h3>

<p>
The final geometric feature to be defined was the pitch. Given a design RPM, our MATLAB model solved for the pitch distribution required to give us an AOA of 9 degrees at all points along the blade’s length.
</p>

<p>
To do this, our model first calculates the local inflow angle
</p>

<div class="equation">
$$\phi=\tan^{-1}\left(\frac{U(1-a)}{\omega r(1+a')}\right)$$
</div>

<p>
where a is the axial induction factor, with a numerical value of ⅓, and a’ is the induction factor for tangential flow, with a numerical value of 0.01.
</p>

<p>
Using $\phi$ we can find the local angle of attack, which is
</p>

<div class="equation">$$\alpha=\phi-pitch$$</div>

<p>
Therefore, with a given optimal RPM, a design oncoming windspeed and the angle of attack set to 9 degrees, our model is able to solve for the pitch at each discretized value of r.
</p>

<h3>4–5. Solve for Forces and Stresses, and Iterate Through Potential Design RPMs</h3>

<p>
The last facet of our blade design process was to determine what our design RPM would be to maximize power output, and verify that the blade would not fail under those operating conditions. We performed the following set of calculations iteratively for a range of design RPMs:
</p>

<h3>4a. For a given design RPM, solve for the blade’s power curve under 4.82 m/s wind.</h3>

<p>
First, given our design RPM, we created a power curve for that blade to understand its performance. This is done by calculating the tangential force (Ft) along the span of the blade and extracting the tangential components of the lift and drag acting on the blade.
</p>

<p>
For each rotation rate within the power curve, we find net oncoming velocity of
</p>

<div class="equation">
$$V_{rel}=\sqrt{U(1-a)^2+(r(i)\omega(1+a'))^2}$$
</div>

<p>
and local inflow angle $\phi(r)$, which, for each rotation rate, gives us
</p>

<div class="equation">
$$F_t=\frac{1}{2}\rho V_{rel}^2 chord(i)
(C_L\sin(\phi(i))-C_D\cos(\phi(i)))$$
</div>

<p>
By integrating $F_t r$ and then multiplying by 3, we were able to find the net torque on the turbine, which when multiplied by rotation rate $\omega$, gives us power.
</p>

<h3>4b. Solve for bending loads</h3>

<p>
Similarly, for each rotation rate within the power curve, the axial force was determined as:
</p>

<div class="equation">
$$F_x=\frac{1}{2}\rho V_{rel}^2 chord(i)
(C_L\cos(\phi(i))+C_D\sin(\phi(i)))$$
</div>

<p>
Then, by integrating $M(r)$ we got the bending moment distribution
</p>

<div class="equation">
$$M(r)=\int_r^{r_{tip}} F_x(r')(r'-r)\,dr'$$
</div>

<p>
which we could use to find the bending stress as:
</p>

<div class="equation">
$$\sigma(r)=\frac{M(r)y(r)}{I(r)}$$
</div>

<p>
$I(r)$ is the area moment of inertia and $y(r)$ is the max distance from the neutral axis to the outermost fiber. To calculate the moment of inertia, our model determines the values of $I$ and $y$ along the blade by scaling the geometric properties of the NACA 4412 airfoil.
</p>

<h3>4c. Verify design within operating limits</h3>

<p>
When iterating through potential design RPM to maximize power, it is imperative to verify the blade remains within operating limits. Therefore, the MATLAB model verifies the free spin RPM remains below 3500 RPM, the torque applied to the torque break is below 0.035 Nm, and the bending stress remains below the material’s limit of 55 MPa.
</p>

<h3>Final Design:</h3>

<p>
After iterating through different design speeds, we found that a design RPM of 1050 produces a blade that reaches its maximum power at that same speed. With this design RPM, we got an optimal pitch distribution of
</p>

<div class="equation">
$$pitch(r)=89.7e^{-26.7r}$$
</div>

<p>
a maximum torque of 0.033 N-m at 1025 RPM and a maximum bending stress of 12.28 MPa at a free spin RPM of 2119 RPM, all of which remain under the operating limits. With this design, we got the following power curve and bending stress distribution:
</p>

<div class="figure">
  <img src="../../assets/images/figure34.png" style="max-width:100%;">
  <br>Figures 3 and 4. Model outputs, Predicted power vs RPM (left) and Bending stress distribution (right) (placeholders)
</div>

<div class="figure">
  <img src="../../assets/images/figure56.png" style="max-width:100%;">
  <br>Figures 5 and 6. Final CAD model (left) wind turbine and installment in the wind tunnel (right) (placeholders)
</div>



<h3>Operating Assumptions:</h3>

<p>
The main assumptions we operated under include:
</p>

<ul>
<li>
Ignoring tip effect and neglecting kinetic and static friction in the torque brake.
These both would lead to a potential over-prediction of output torque, as both of these would induce additional drag and friction on the blades that would slow them down.
</li>

<li>
Assuming that the axial induction factor a=⅓ and tangential induction factor a’=0.01.
Induction factors vary along the length of the blade and depend on a variety of factors, so these likely are not accurate. Small changes in these induction factors can likely result in large changes in our model’s predicted output torque and RPM.
</li>

<li>
Cl and Cd are collected assuming we operate under a constant Reynold’s number of 50,000.
In reality, the Reynolds number varies along the blade’s radius, and averages around 22,000, which is a Reynolds number that airfoiltools cannot accommodate for.
</li>

<li>
Neglecting the impact of pitch on the bending stress distribution.
The area moment of inertia would change drastically as a function of the radius if we accounted for this, so we neglected it, potentially under-predicting the bending stress.
</li>
</ul>

<h2>4. Testing Approach</h2>

<p>
Our testing began by assembling the turbine (attaching blades, mounting the hub, reinstalling the nose cone) and confirming LabView was correctly set up, with pressure transducer calibrated and with successful data collection verified. Then, before turning on the wind tunnel, we set the torque break voltage to zero, applying no resistive torque.
</p>

<div class="figure">
  <img src="../../assets/images/figure7.png" style="max-width:80%;">
  <br>Figure 7. Experimental testing procedure flowchart (placeholder)
</div>


<p>
Iterating through the oncoming wind speeds (starting from the smallest oncoming wind speed for which the blade began to spin), we first increased the fan frequency of the wind tunnel, monitoring the ramp up to ensure the turbine never exceeded 3500 RPM, and if it approached that limit, we would quickly shut off the wind tunnel.
</p>

<p>
If free spin was safely reached, data collection would begin. Once the fan stabilizes, a data point is collected, then the torque brake voltage is increased in small increments of 0.3 V with subsequent data collection until the turbine stalls.
</p>

<p>
If the turbine appeared to be approaching the 3500 RPM limit too closely for a given wind speed, we decreased the wind speed, applying some torque to the turbine via the torque break, then increase the wind speed, to avoid surpassing that rotational speed limit.
</p>

<p>
In total, five wind speeds were tested: 4.1 m/s, 4.8 m/s, 4.9 m/s, 5.3 m/s, and 5.8 m/s.
</p>


<h2>5. Results</h2>

<p>
A power curve was collected for each of the five wind speeds.
</p>

<div class="figure">
  <img src="../../assets/images/figure89.png" style="max-width:100%;">
  <br>Figures 8 and 9, Experimental data: Power vs. RPM (Left), Power vs wind speed (Right) at different RPMs is marked by the dashed line (placeholders)
</div>

<p>
The data follows expected trends; a higher wind speed results in more power extraction and higher RPMs. Between 2100-2400 RPM the data flattens out, likely due to the blade’s rotation rate leading to the blade experiencing its resonant frequency, slowing it down. This is found in all power curves that spin at this range, indicating it is experiencing resonance.
</p>

<p>
To determine the best operating RPM for the blades– defined by the RPM for which the blade consistently extracted max power– four different RPMs were plotted for power vs. wind speed. The RPMs selected for the plot were RPMs for which the vertical intercepts got closest to the maximums of all tested wind velocities.
</p>

<p>
This is shown with the blue, orange, and yellow lines on Figure 8. The fourth RPM in purple was chosen to comparatively see how the blade operated at a much higher RPM.
</p>

<p>
These chosen RPMs were adjusted slightly to find the RPM that consistently extracted maximum power throughout all wind speeds, which ended up being 1770 PRM.
</p>

<p>
This differed from the design angular velocity of 1050 RPM with a 69% error. The blade was also not able to spin at 1050 RPM, likely due to kinetic friction, which was not accounted for in the model.
</p>

<p>
Further comparing the model predictions to the experimental results, the model consistently overpredicted the max power extracted. This is likely due to the assumptions built into the model that ignore tip effect, which neglects additional drag and friction forces on the blades that slowed them down.
</p>

<div class="figure">
  <img src="../../assets/images/figure10.png" style="max-width:100%;">
  <br>Figure 10. Experimental vs Model power curves at 4.8 and 5.8 m/s (placeholder)
</div>



<<p>
Wind Speed
Predicted Max Power
Experimental Max Power
% Error
</p>

<table>
<tr>
<th>Wind Speed</th>
<th>Predicted Max Power</th>
<th>Experimental Max Power</th>
<th>% Error</th>
</tr>
<tr>
<td>4.8 m/s (design)</td>
<td>3.61 W</td>
<td>0.70 W</td>
<td>81%</td>
</tr>
<tr>
<td>5.8 m/s (max tested)</td>
<td>6.50 W</td>
<td>1.80 W</td>
<td>72%</td>
</tr>
</table>

<p>
Table 1. Maximum Power for Experimental Data vs. Model Predictions
</p>

<p>
In addition, the model also overpredicts free spin, a prediction that worsens as wind speed increases.
</p>

<div class="figure">
  <img src="../../assets/images/figure11.png" style="max-width:100%;">
  <br>Figure 11. all experimental vs model power curves comparing predicted free spin speed.
</div>


<p>
This is likely due to a combination of the assumptions used to build the model, the most likely contributing factor being the assumed axial and tangential induction factors a=⅓ and a’=0.01 respectively. Induction factors vary along the blade and depend on numerous conditions, so the values used here are approximated. Minor variations in these factors can produce significant changes in the predicted rotational speed.
</p>

<p>
Since one of the main objectives was to optimize average extracted power given a specific wind speed probability distribution, we wanted to return to the Weibull distribution when analyzing our results. Overall, we were successful in collecting data for a range of wind speeds across the distribution, but were unable to obtain data for wind speeds below 4 m/s due to stalling.
</p>

<p>
Based on our collected data and the distribution, we were able to experimentally estimate the average power that would be collected by our turbine by finding the “expected value” of power over the distribution, using the following formula.
</p>

<div class="equation">
$$E(P(u)) = \int P(u)\,p(u)\,du$$
</div>

<p>
Here, E(P(u)) is the “expected value” (average) of power, P(u) is the power as a function of incoming wind velocity at our design rotation rate (1050 RPM), and p(u) is the probability distribution of wind speeds.
</p>

<p>
For better visualization, we plotted P(u) and p(u) on the same set of axes (see figure below), which shows that at our chosen design RPM and geometry, we are missing out on the lower half of the wind speed distribution.
</p>

<p>
After computing the integral, we estimate an average power of 1.11 W across the entire distribution, which is still relatively high.
</p>

<div class="figure">
  <img src="../../assets/images/figure1213.png" style="max-width:100%;">
  <br>Figures 12. and 13. Experimental data compared to wind velocity probability distribution (placeholders)
</div>



<h2>6. Conclusion</h2>

<p>
Overall, our blade design was effective at extracting power in a wind tunnel, achieving a maximum measured output of 1.8W. This result demonstrates that our blade design methodology, which optimizes CLCD, taper, and twist, was effective at producing a functional turbine blade.
</p>

<p>
However, the model inaccurately predicted optimal operating RPM and maximum power output. The model underpredicted operating RPM, selecting a design RPM of 1050 RPM compared to an experimentally determined optimum of 1770 RPM, and overpredicted maximum power, estimating 6.5 W versus the measured 1.8 W at a wind speed of 5.8 m/s.
</p>

<p>
Future work should focus on improving model fidelity to better align predicted and experimental performance. Key improvements include more accurate calculation of axial and tangential induction factors, incorporation of losses from tip effects, and accounting for frictional losses and stress concentrations at the hub connection.
</p>



</div>
</body>
</html>

