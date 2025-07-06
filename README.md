# 🌍 Global Air Quality Monitor
<details>
<summary><b>📌 Click to expand/collapse project description</b></summary>

A real-time air quality monitoring dashboard with interactive visualizations, health recommendations, and pollution analytics.


## ✨ Features
<div>
  <button onclick="toggleFeatureDetails()" style="background:#4CAF50;color:white;border:none;padding:8px 16px;border-radius:4px;cursor:pointer">Toggle Feature Details</button>
</div>

<div id="featureDetails" style="display:none; margin-top:10px">
- 🌐 <b>Real-time air quality data</b> <span class="tooltip">ℹ️<span class="tooltiptext">Updates every 15 minutes from 10,000+ stations</span></span>
- 🗺️ <b>Interactive map visualization</b> <span class="tooltip">ℹ️<span class="tooltiptext">Click any point to see detailed readings</span></span>
- 📊 <b>Pollutant concentration charts</b> <span class="tooltip">ℹ️<span class="tooltiptext">Compare PM2.5, O3, NO2 levels</span></span>
</div>

<style>
.tooltip {
  position: relative;
  display: inline-block;
  cursor: help;
}

.tooltip .tooltiptext {
  visibility: hidden;
  width: 200px;
  background-color: #555;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px;
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -100px;
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
  opacity: 1;
}
</style>

## 🌦️ Live Demo
<!-- HTML for interactive demo panel -->
<div style="border:1px solid #ddd;padding:15px;border-radius:8px">
  <div style="display:flex;gap:10px;margin-bottom:15px">
    <input type="text" id="demoLocation" placeholder="Enter city name" style="flex-grow:1;padding:8px">
    <button onclick="fetchDemoData()" style="background:#2196F3;color:white;border:none;padding:8px 16px;border-radius:4px;cursor:pointer">Check Air Quality</button>
  </div>
  
  <div id="demoResult" style="background:#f5f5f5;padding:15px;border-radius:5px;min-height:100px">
    <p style="text-align:center;color:#777">Enter a location to see sample data</p>
  </div>
</div>

<script>
function fetchDemoData() {
  const location = document.getElementById("demoLocation").value;
  if (!location) return;
  
  document.getElementById("demoResult").innerHTML = `
    <div style="text-align:center">
      <div class="loader"></div>
      <p>Fetching data for ${location}...</p>
    </div>
  `;
  
  // Simulate API call
  setTimeout(() => {
    const aqi = Math.floor(Math.random() * 300);
    const category = aqi <= 50 ? "Good" : 
                   aqi <= 100 ? "Moderate" :
                   aqi <= 150 ? "Unhealthy for Sensitive" :
                   aqi <= 200 ? "Unhealthy" : "Hazardous";
                   
    document.getElementById("demoResult").innerHTML = `
      <h3 style="margin-top:0">${location} Air Quality</h3>
      <div style="display:flex;align-items:center;gap:15px">
        <div style="font-size:24px;font-weight:bold;color:${
          aqi <= 50 ? '#50C878' : 
          aqi <= 100 ? '#F5D300' :
          aqi <= 150 ? '#FF9966' :
          aqi <= 200 ? '#FF3333' : '#7E0023'
        }">${aqi} AQI</div>
        <div>${category}</div>
      </div>
      <p>Updated: ${new Date().toLocaleTimeString()}</p>
      <button onclick="showRecommendations()" style="background:#4CAF50;color:white;border:none;padding:6px 12px;border-radius:4px;cursor:pointer;margin-top:10px">Show Health Recommendations</button>
      <div id="recommendations" style="display:none;margin-top:10px;padding:10px;background:#e8f5e9;border-radius:5px"></div>
    `;
  }, 1500);
}

function showRecommendations() {
  const recDiv = document.getElementById("recommendations");
  recDiv.style.display = "block";
  recDiv.innerHTML = `
    <h4 style="margin-top:0">Health Advice:</h4>
    <ul style="margin-bottom:0">
      <li>${Math.random() > 0.5 ? "Consider reducing outdoor activities" : "Air quality is good for most people"}</li>
      <li>${Math.random() > 0.5 ? "Sensitive groups may experience symptoms" : "No significant health risk expected"}</li>
    </ul>
  `;
}
</script>

<style>
.loader {
  border: 4px solid #f3f3f3;
  border-top: 4px solid #3498db;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  animation: spin 1s linear infinite;
  margin: 0 auto 10px;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>

## 📊 AQI Scale Reference
<table>
  <thead>
    <tr>
      <th onclick="sortTable(0)">AQI Range ▲▼</th>
      <th onclick="sortTable(1)">Category ▲▼</th>
      <th>Color</th>
      <th>Health Implications</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0-50</td>
      <td>Good</td>
      <td><div style="width:20px;height:20px;background:#50C878"></div></td>
      <td>Air quality is satisfactory</td>
    </tr>
    <tr>
      <td>51-100</td>
      <td>Moderate</td>
      <td><div style="width:20px;height:20px;background:#F5D300"></div></td>
      <td>Acceptable quality</td>
    </tr>
    <tr>
      <td>101-150</td>
      <td>Unhealthy for Sensitive</td>
      <td><div style="width:20px;height:20px;background:#FF9966"></div></td>
      <td>Mild health effects</td>
    </tr>
  </tbody>
</table>

<script>
function sortTable(n) {
  // Table sorting logic would go here
  alert("Sorting functionality would be implemented in a live environment");
}
</script>

## 🛠️ Try It Yourself
```python
# Sample code snippet
import requests

def get_aqi(location):
    api_url = f"https://api.waqi.info/feed/{location}/?token=YOUR_TOKEN"
    response = requests.get(api_url)
    data = response.json()
    return data['data']['aqi']

# Try editing this value!
print(f"Current AQI: {get_aqi('London')}")
