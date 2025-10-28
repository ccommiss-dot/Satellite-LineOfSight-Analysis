# Satellite Line-of-Sight Analysis Tool - Woods Canyon Test Case

A Python-based tool for analyzing satellite visibility and line-of-sight calculations using Digital Elevation Models (DEMs). This implementation specifically demonstrates the analysis for **Woods Canyon near Laguna Beach, California** using a modified GOES-17 satellite position.

![Example Output](docs/example_output.png)

## ⚠️ Important Notes

### Test Area Specificity
- **This code is configured for Woods Canyon, CA** (33.52°N, -117.75°W)
- The DEM boundaries and coordinate transformations are specific to this region
- **To use for other regions**: You'll need to modify the coordinate bounds and potentially the UTM zone in Cell 2

### Satellite Configuration
- Uses **GOES-17** orbital position (longitude) for realistic azimuth
- **Artificially lowered elevation angle to 8°** for demonstration purposes
- Real GOES-17 elevation from this location would be ~30° (too high for terrain blocking)
- The 8° angle allows demonstration of line-of-sight blocking in gentle terrain

## Features

- 🛰️ Modified satellite position for terrain interaction analysis
- 🏔️ Terrain-based line-of-sight calculations for Woods Canyon
- 🗺️ Interactive visualization maps showing blocked/clear areas
- 📍 KML export for Google Earth visualization
- 🎯 Configurable mesh resolution (100 to 5000+ points)
- 📊 Statistical analysis of visibility (typically ~93% clear, ~7% blocked at 8° elevation)

## Quick Start

### Prerequisites
- Python 3.8 or higher
- Anaconda or pip for package management
- ~50MB disk space for DEM file

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/satellite-los-analysis.git
cd satellite-los-analysis
Install required packages:
bash

pip install -r requirements.txt
Download the Woods Canyon DEM:

Visit OpenTopography.org
Search for area around: 33.52°N, -117.75°W
Select approximately 5km × 5km area
Download as GeoTIFF format (SRTM 30m recommended)
Save to data/dem/ folder
Rename to woodsCanyonRectangular.tif or update filename in Cell 2
Run the Jupyter notebook:

bash

jupyter notebook satellite_los_analysis.ipynb
How the Analysis Works
1. Satellite Position Modification (Cell 8)
python

# Real GOES-17 would be at ~30° elevation
# We force it to 8° for terrain interaction
TARGET_ELEVATION = 8.0  # degrees
This artificial lowering simulates:

Low elevation satellite passes
Communication satellites near the horizon
Future LEO constellation visibility
2. Line-of-Sight Calculation
For each point in the mesh:

Calculate direct path to satellite
Check if terrain along path exceeds line-of-sight
Mark as "blocked" (red) or "clear" (green)
3. Expected Results for Woods Canyon
With 8° satellite elevation:

~93% Clear visibility: Most ridges and slopes
~7% Blocked: Deep canyon bottoms and north-facing slopes
Blocking occurs where terrain rise > ~140m per 1km distance
Adapting for Other Regions
To analyze a different area, modify:

Cell 2 - Update DEM Configuration:
python

# Change DEM filename
DEM_FILENAME = 'your_area.tif'  # Your DEM file

# Verify/update UTM zone if needed
# Woods Canyon uses UTM Zone 11N
# Your area might use different zone
Cell 2 - Update Location Verification:
python

# Change expected coordinates
expected_lat = 33.52  # Your area's latitude
expected_lon = -117.75  # Your area's longitude
Cell 8 - Adjust Satellite Parameters:
python

# Modify elevation angle as needed
TARGET_ELEVATION = 8.0  # Adjust for your analysis
# Consider: 5° for more blocking, 15° for less blocking
Project Structure
satellite-los-analysis/
├── satellite_los_analysis.ipynb  # Main notebook (Woods Canyon configured)
├── README.md                      # This file
├── requirements.txt               # Python dependencies
├── data/
│   └── dem/                      # Place DEM files here
├── output/
│   ├── kml/                      # KML outputs for Google Earth
│   └── maps/                     # HTML visualization maps
└── docs/
    └── dem_download_guide.md     # Instructions for DEM acquisition
Understanding the Output
Visualization Colors:
🟢 Green areas: Clear line-of-sight to satellite
🔴 Red areas: Terrain blocks satellite visibility
⚪ White marker: DEM center point
Statistics Output:
📊 RESULTS:
  Clear: 4650 (92.3%)    # Points with visibility
  Blocked: 391 (7.7%)     # Points blocked by terrain
Limitations
Single Satellite: Currently analyzes one satellite position at a time
Static Analysis: Doesn't account for satellite movement over time
Atmospheric Effects: Doesn't model atmospheric refraction
Vegetation: DEM doesn't include tree canopy height
Troubleshooting
"DEM not found" error:

Ensure DEM is in data/dem/ folder
Update DEM_FILENAME in Cell 2
"Satellite below horizon" warning:

This is expected with 8° forced elevation
The analysis still works correctly
Different results than expected:

Verify your DEM covers Woods Canyon area
Check coordinate transformation in Cell 2
Ensure Cell 9 (coordinate fix) has been run
Technical Details
Coordinate Systems:
Input DEM: UTM Zone 11N (EPSG:32611)
Analysis: WGS84 (EPSG:4326)
Output: KML uses WGS84 for Google Earth
Performance:
100 points: ~10 seconds
5000 points: ~8-10 minutes
Speed: ~5-15 iterations/second typical
Contributing
Contributions welcome! Potential improvements:

Multiple satellite analysis
Dynamic TLE updates
GUI interface
GPU acceleration for large meshes
License
MIT License - see LICENSE file

Acknowledgments
Digital Elevation Model: OpenTopography
Satellite calculations: Skyfield
Test area: Woods Canyon Wilderness Park, Laguna Beach, CA
Author
[Your Name]
[Your Contact/GitHub]

Citation
If using this code for research:

[Your Name]. (2024). Satellite Line-of-Sight Analysis Tool - Woods Canyon Test Case. 
GitHub repository: https://github.com/yourusername/satellite-los-analysis
Disclaimer
This is a demonstration tool using artificially modified satellite positions. For real satellite communication analysis, use actual orbital parameters and consider atmospheric effects.


## 4. **Create docs/dem_download_guide.md**

```markdown
# DEM Download Guide for Woods Canyon Analysis

## Quick Download for Woods Canyon

### Coordinates for Woods Canyon, Laguna Beach, CA:
- **Center**: 33.52°N, -117.75°W
- **Recommended area**: 5km × 5km around center

### Step-by-Step OpenTopography Download:

1. Go to [OpenTopography.org](https://www.opentopography.org/)
2. Click "Find Data" → "Global Data"
3. Select "SRTM GL1 (30m)" 
4. In the map, navigate to Southern California
5. Draw a box around these coordinates:
   - North: 33.545°
   - South: 33.495°
   - East: -117.725°
   - West: -117.775°
6. Click "Submit"
7. Choose "GeoTiff" format
8. Download the file
9. Rename to `woodsCanyonRectangular.tif`
10. Save to `data/dem/` folder

## For Other Regions

### Modify the coordinates in step 5 above to your area of interest

### Recommended DEM Sources by Region:

**United States**:
- USGS 3DEP (1-10m resolution)
- SRTM (30m, global coverage)

**Europe**:
- EU-DEM (25m)
- SRTM (30m)

**Global**:
- SRTM GL1 (30m) - Recommended
- ASTER GDEM (30m)

## File Requirements

- **Format**: GeoTIFF (.tif or .tiff)
- **Size**: Keep under 100MB for GitHub
- **Projection**: Any (code auto-detects)
- **Resolution**: 30m recommended (1-90m supported)
