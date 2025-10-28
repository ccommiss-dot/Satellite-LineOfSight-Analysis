# Satellite Line-of-Sight Analysis Tool

A Python-based tool for analyzing satellite visibility and line-of-sight calculations using Digital Elevation Models (DEMs). This tool determines which areas have clear visibility to satellites (like GOES-17) and which are blocked by terrain.

![Example Output](docs/example_output.png)

## Features

- 🛰️ Satellite position calculation using TLE data
- 🏔️ Terrain-based line-of-sight analysis
- 🗺️ Interactive visualization maps
- 📍 KML export for Google Earth
- 🎯 Configurable mesh resolution (100 to 5000+ points)
- 📊 Statistical analysis of blocked vs. clear areas

## Quick Start

### Prerequisites
- Python 3.8 or higher
- Anaconda or pip for package management

### Installation

1. Clone the repository:
```bash
git clone https://github.com/ccommiss-dot/satellite-los-analysis.git
cd satellite-los-analysis