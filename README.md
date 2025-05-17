#Source code
html>
<html>
<head>
  <title>Urban Planning Tool</title>
  <meta charset="utf-8" />
  <link rel="stylesheet" href="https://unpkg.com/leaflet/dist/leaflet.css" />
  <style>
    #map { height: 90vh; }
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; }
    .controls {
      padding: 10px;
      background: #f0f0f0;
      display: flex;
      gap: 10px;
    }
  </style>
</head>
<body>

<div class="controls">
  <select id="markerType">
    <option value="Building">Building</option>
    <option value="Park">Park</option>
    <option value="School">School</option>
  </select>
  <button onclick="clearMarkers()">Clear Markers</button>
</div>

<div id="map"></div>

<script src="https://unpkg.com/leaflet/dist/leaflet.js"></script>
<script>
  const map = L.map('map').setView([13.0827, 80.2707], 13); // Centered on Chennai

  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '© OpenStreetMap contributors'
  }).addTo(map);

  const markers = [];

  function addMarker(latlng, type) {
    const color = {
      "Building": "blue",
      "Park": "green",
      "School": "red"
    }[type];

    const marker = L.circleMarker(latlng, {
      radius: 8,
      color: color,
      fillColor: color,
      fillOpacity: 0.8
    }).bindPopup(type).addTo(map);

    markers.push(marker);
  }

  map.on('click', function(e) {
    const type = document.getElementById("markerType").value;
    addMarker(e.latlng, type);
  });

  function clearMarkers() {
    markers.forEach(marker => map.removeLayer(marker));
    markers.length = 0;
  }
</script>

</body>
</html>
