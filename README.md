Determining Rooftop Candidates for Hosting GPS Error Correction RTK Sites

As GPS technology becomes increasingly central to navigation, mapping, and autonomous systems, the demand for higher precision is growing and, in some cases, it can be a matter of life and death. Although standard GPS provides location accuracy within meters, this level of precision falls short for applications that demand pinpoint accuracy. To bridge this gap, several GPS error correction techniques are employed, such as Post-Processing, Differential GPS (DGPS), and Real-Time Kinematics (RTK). These methods require strategic enhancements to consistently achieve centimeter-level accuracy. This project focuses on improving the accuracy of the RTK method, which provides real-time correction signals to mobile receivers. The effectiveness of RTK systems depends on the placement of its base stations on rooftops with minimal signal obstruction and maximum sky visibility. To meet this requirement, in this project we evaluated the horizon profile of each building in an area using spatial data such as building footprints, elevation, and height. Additionally, for each building, we generated 360° horizon graphs to capture blocking angles, allowing us to visually and quantitatively assess potential interference. We also conducted geospatial analysis of 2,834 buildings in the GMU campus area to determine ideal rooftop candidates. Each rooftop was assessed against a strict interference threshold to ensure unobstructed sky visibility. The analysis incorporated atmospheric dome modeling to account for landscape curvature and elevation differences. As a result, we identified 49 optimal rooftops for RTK base station installation. These findings led to the development of a visibility ranking system that determines high-potential rooftop installation sites.

Table of Contents

Project Overview

Dependencies

Data Preparation

Methodology

Results

Usage Instructions

Team Members

License

Contact

Project Overview

(See above for full project description)

Dependencies

Hardware: Minimum 4 GB RAM, Dual‑core Intel Core i5 or better

Software:

QGIS

PostgreSQL

PGAdmin or DBeaver

OSGeo4W (Windows)

Data Preparation

Import Building Footprints into PostGIS using OSGeo4W:

ogr2ogr -f "PostgreSQL" \
  PG:"host=<host> dbname=<db> user=postgres password=<pw>" \
  "<path/to/json>" -nln test_bldgs -a_srs EPSG:4326 -overwrite

Compute Horizon Profiles: Generate 360° radial lines (up to 30 km) per rooftop.

Intersect & Measure: Find intersections between horizon rays and taller buildings.

Methodology

Horizontal Profiling:

Sample each rooftop’s skyline at 1° azimuth increments.

Compute blocking angles where adjacent buildings protrude above the horizon.

Atmospheric Dome Modeling:

Approximate the open-sky dome with 1° elevation slices.

Map blocked azimuth–elevation cells to dome facets to estimate sky obstruction.

Candidate Scoring:

Filter rooftops with no blocking angles above 10°.

Incorporate building elevation (absolute height) into selection.

Rank by unobstructed sky area and height suitability.

Results

Total Buildings Analyzed: 2,834

RTK‑Suitable Rooftops Identified: 49

Deliverables:

eligible_candidates table (PostGIS)

CSV exports and interactive 3D visualization scripts

Sky visibility ranking report

Usage Instructions

Clone this repository:

git clone https://github.com/<your-org>/rtk-rooftop-selection.git
cd rtk-rooftop-selection

Load data into PostGIS (see Data Preparation).

Run SQL scripts in sql/ folder via PGAdmin or psql.

Generate plots and export CSVs using provided Python or R scripts.

Visualize results in QGIS or via the interactive dashboards.

Team Members

Sabari Mukundth Jayaram

Vyoma Harshitha Podapati

Kirubel Tadesse

Satya Sai Varun Chidagam

Sai Sree Varshitha Lingamneni

Sai Pranav Beesetti
