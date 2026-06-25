<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>F1 Telemetry Analysis: Low-Speed vs. High-Speed Cornering</title>
    <style>
        body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif; line-height: 1.6; padding: 20px; max-width: 900px; margin: auto; }
        h1, h2, h3 { border-bottom: 1px solid #eaecef; padding-bottom: 0.3em; }
        table { border-collapse: collapse; width: 100%; margin-bottom: 20px; }
        th, td { border: 1px solid #dfe2e5; padding: 6px 13px; }
        th { background-color: #f6f8fa; }
        code { background-color: #rgba(27,31,35,0.05); border-radius: 3px; padding: 0.2em 0.4em; font-family: monospace; }
        .plot-placeholder { background-color: #f6f8fa; border: 2px dashed #d1d5da; padding: 40px; text-align: center; color: #586069; margin: 20px 0; }
    </style>
</head>
<body>

    <h1>Formula 1 Telemetry Analysis: Quadratic Modeling of Cornering Profiles</h1>

    <h2>Overview</h2>
    <p>This repository contains a dual-model mathematical framework comparing vehicle kinematics across two geometrically distinct track sectors: a low-speed mechanical corner (Turn 6) and a high-speed aerodynamic corner (Turn 13). Using telemetry data from Lando Norris (Lap 7), we derive quadratic functions via vertex systems, compare longitudinal acceleration, and use numerical integration to isolate time performance losses.</p>

    <h2>1. The Telemetry Dataset</h2>
    <p>The data represents high-frequency captures isolating the entry, apex, and exit stages of both corners at fixed intervals of h = 0.5 s.</p>

    <table>
        <thead>
            <tr>
                <th>Turn Location</th>
                <th>Time t (s)</th>
                <th>Velocity v(t) (m/s)</th>
                <th>Corner Phase Status</th>
            </tr>
        </thead>
        <tbody>
            <tr><td>Turn 6 (Slow)</td><td>0.0</td><td>35.000</td><td>Corner Entry</td></tr>
            <tr><td>Turn 6</td><td>1.0</td><td>13.914</td><td>Corner Apex (Minimum Speed)</td></tr>
            <tr><td>Turn 6</td><td>2.0</td><td>35.000</td><td>Full Exit Recovery</td></tr>
            <tr><td>Turn 13 (High)</td><td>0.0</td><td>80.003</td><td>Corner Entry</td></tr>
            <tr><td>Turn 13</td><td>1.5</td><td>57.683</td><td>Corner Apex (Minimum Speed)</td></tr>
            <tr><td>Turn 13</td><td>3.0</td><td>80.003</td><td>Full Exit Recovery</td></tr>
        </tbody>
    </table>

    <h2>2. Quadratic Derivation and Modeling</h2>
    <p>We modeled the velocity for both corners using the standard quadratic equation: <code>v(t) = at<sup>2</sup> + bt + c</code>.</p>

    <h3>Turn 6 (Low-Speed Mechanical)</h3>
    <p>Turn 6 features a minimum apex speed of 13.914 m/s at 1.0 s. Using the boundary entry coordinate (0.0, 35.000), the expanded standard form is:</p>
    <p><code>v<sub>6</sub>(t) = 21.086t<sup>2</sup> - 42.172t + 35.000</code></p>
    
    <div class="plot-placeholder">
        <p>[Plot: Turn 6 Velocity vs. Time Profile]</p>
        <img src="plots/turn6_velocity.png" alt="Turn 6 Velocity Curve" style="max-width:100%; display:none;">
    </div>

    <h3>Turn 13 (High-Speed Aerodynamic)</h3>
    <p>Turn 13 features a minimum apex speed of 57.683 m/s at 1.5 s. Using the boundary entry coordinate (0.0, 80.003), the expanded standard form is:</p>
    <p><code>v<sub>13</sub>(t) = 9.920t<sup>2</sup> - 29.760t + 80.003</code></p>

    <div class="plot-placeholder">
        <p>[Plot: Turn 13 Velocity vs. Time Profile]</p>
        <img src="plots/turn13_velocity.png" alt="Turn 13 Velocity Curve" style="max-width:100%; display:none;">
    </div>

    <h2>3. Differential Analysis: Acceleration</h2>
    <p>By differentiating the continuous velocity functions, we obtained instantaneous longitudinal acceleration equations:</p>
    <ul>
        <li><strong>Turn 6:</strong> <code>a<sub>x,6</sub>(t) = 42.172t - 42.172</code></li>
        <li><strong>Turn 13:</strong> <code>a<sub>x,13</sub>(t) = 19.840t - 29.760</code></li>
    </ul>
    <p>Evaluating at corner entry (t = 0), Turn 6 experiences a peak braking force of -42.172 m/s<sup>2</sup> (&approx; -4.3g). In contrast, Turn 13 experiences -29.760 m/s<sup>2</sup> (&approx; -3.0g). This tighter turning radius in the low-speed corner requires a significantly steeper deceleration profile.</p>

    <div class="plot-placeholder">
        <p>[Plot: Turn 6 vs Turn 13 Acceleration Profiles]</p>
        <img src="plots/acceleration_comparison.png" alt="Acceleration Comparison" style="max-width:100%; display:none;">
    </div>

    <h2>4. Numerical Integration and Performance Degradation</h2>
    <p>Using the Trapezoidal Rule, we calculated the total distance (d) of each corner zone to isolate the time performance losses:</p>
    <ul>
        <li><strong>Turn 6 Loss:</strong> The ideal straight-line baseline to clear 51.14 m at 35.000 m/s is 1.461 s. The actual time is 2.000 s, resulting in a loss of <strong>0.539 s</strong>.</li>
        <li><strong>Turn 13 Loss:</strong> The ideal baseline to clear 200.00 m at 80.003 m/s is 2.500 s. The actual time is 3.000 s, resulting in a loss of <strong>0.500 s</strong>.</li>
    </ul>

    <h2>5. Conclusion</h2>
    <p>Despite Turn 13 operating at speeds nearly four times higher than Turn 6, it accounts for an incredibly similar time penalty (&approx; 0.50 s). This mathematical insight proves that high-speed corner momentum management is just as critical to an optimal lap time as executing severe braking zones in slow hairpins.</p>

</body>
</html>
