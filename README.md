<!DOCTYPE html>
<html lang="en">
<body>
<h1>Dynamic Pricing for Urban Parking Lots</h1>
<p><strong>An intelligent, real-time pricing engine for 14 urban parking spaces</strong>—built with Pathway streaming, three custom pricing models, and interactive Bokeh/Panel visualizations.</p>

<h2>📖 Overview</h2>
<p>Urban parking is a scarce, time-sensitive resource. Static pricing leads to overcrowding or empty lots. This project simulates a dynamic pricing system that:</p>
<ul>
  <li>Ingests real-time data (occupancy, queue, traffic, special days, vehicle type)</li>
  <li>Applies three pricing models of increasing sophistication</li>
  <li>Streams updates via Pathway</li>
  <li>Visualizes prices and triggers in an interactive dashboard</li>
</ul>

<h2>🛠 Tech Stack</h2>
<ul>
  <li><strong>Language & Data:</strong> Python, Pandas, NumPy</li>
  <li><strong>Streaming:</strong> Pathway</li>
  <li><strong>Visualization:</strong> Bokeh, Panel</li>
  <li><strong>Notebook:</strong> Google Colab</li>
</ul>

<h2>🏗 Architecture Diagram</h2>
<pre class="code-block">
├── dataset.csv               # Source dataset containing parking lot stats
├── notebook.ipynb            # Main Colab-compatible notebook with full workflow
├── requirements.txt          # Required dependencies
├── README.md                 # Project documentation and overview
├── Output/                   
    └── bokeh_plot.png        # Image of a graph
</pre> <h2>🔍 Project Architecture & Workflow</h2> <h3>Data Ingestion</h3> <ul> <li>Load <code>dataset.csv</code></li> <li>Convert Occupancy, Capacity, QueueLength, TrafficConditionNearby, IsSpecialDay to numeric</li> <li>Parse and sort by Timestamp & ID</li> </ul> <h3>Feature Engineering</h3> <ul> <li>Compute occupancy rate (<code>occ_rate</code>)</li> <li>Normalize QueueLength & TrafficConditionNearby per lot</li> <li>Map VehicleType → weight</li> </ul> <h3>Pricing Models</h3> <ul> <li><strong>Model 1 (Baseline Linear):</strong><br/> <code>price[t+1] = price[t] + α·(Occupancy/Capacity)</code> </li> <li><strong>Model 2 (Demand-Based):</strong><br/> <code>Demand = a·occ_rate + b·queue_norm − c·traffic_norm + d·IsSpecialDay + e·VT_weight</code><br/> <code>price = BasePrice · (1 + λ·normalize(Demand))</code> </li> <li><strong>Model 3 (Competitive):</strong><br/> If full & competitor logic → discounted price + reroute flag<br/> Else → uplift based on local traffic pressure </li> </ul> <h3>Smoothing & Streaming</h3> <ul> <li>Apply EWMA (α = 0.2) to each price series</li> <li>Write <code>parking_stream_final.csv</code></li> <li>Replay with Pathway for real-time simulation</li> </ul> <h3>Visualization & Export</h3> <ul> <li>Build interactive Bokeh figure with dual y-axis (price vs. occ_rate), hover tool, reroute highlights</li> <li>Embed in Panel layout</li></ul> <h2>📁 Repository Structure</h2> <pre class="code-block">
├── dataset.csv               # Original parking dataset
├── notebook.ipynb            # Main Colab notebook
├── requirements.txt          # Required dependencies
├── README.md                 # Project description and documentation
├── Output/                   
│   └── bokeh_plot.png        # Image of the output
</pre> <h2>▶️ Getting Started</h2><p><strong>Install dependencies</strong></p> <pre class="code-block"> pip install -r requirements.txt </pre> <p><strong>Open the Notebook</strong></p> <ul> <li>On your local Jupyter or Google Colab: <code>notebooks/notebook.ipynb</code></li> <li>Clear outputs, run all cells</li> </ul>
<h2>🔗 License & Access</h2> <p>This repository is public.</p> <p>Feel free to explore, fork, and provide feedback.</p> </body> </html>
