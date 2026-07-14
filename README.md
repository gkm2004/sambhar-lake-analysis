# Sambhar Lake Analysis

Exploratory analysis of surface water patterns in Sambhar Lake, Rajasthan, using Sentinel-2 satellite imagery and unsupervised clustering.

## Background

Sambhar Lake is a saline, ephemeral lake in Rajasthan, India, whose surface water extent changes noticeably with seasonal monsoon rainfall. Rather than precise hydrological modelling, this project visually explores how surface water patterns vary across years, and whether distinct spatial zones consistently emerge within the lake.

## Data

- **Satellite imagery:** Multispectral Sentinel-2 imagery, provided by the European Space Agency through the Copernicus Programme. One cloud-free image from the post-monsoon period was selected for each year, 2022–2024.
- **Climate data:** Annual precipitation and temperature summaries for the Sambhar region (see `Table 1-1` in the full report), used to compare rainfall against surface water patterns.

## Methods

1. **NDWI calculation** — The Green (B03) and near-infrared (B08) Sentinel-2 bands were used to compute the Normalised Difference Water Index (NDWI), which highlights surface water by contrasting water-absorbing and water-reflecting wavelengths. NDWI rasters were clipped to the Sambhar Lake boundary.
2. **Unsupervised clustering** — K-means clustering (k = 5) was applied separately to each year's NDWI raster, grouping pixels with similar NDWI values without predefined labels. Clusters were relabelled by relative NDWI magnitude to allow comparison across years.

**Note:** This is an exploratory analysis based on remotely sensed surface indicators, not in-situ hydrological or geochemical measurements. Clusters are interpreted qualitatively and are not intended as definitive geological classifications.

## Results

NDWI maps and clustering reveal clear spatial variability in surface water presence across the lake, with noticeable inter-annual differences:

| Cluster | Relative NDWI | Interpretation |
|---|---|---|
| 0 (Dark Green) | Very high | Persistent Wet Core — stable, water-retaining zones |
| 1 (Light Cyan/Teal) | Moderately high | Seasonally Inundated Fringe — shallow/periodically flooded |
| 2 (Yellow/Olive) | Intermediate | Transitional Moist Zone — rain-sensitive, high variability |
| 3 (Pink/Magenta) | Low | Ephemeral Drying Areas — temporarily wet, undergoing drying |
| 4 (Purple/Violet) | Very low | Persistent Dry/Salt-Crust Zone — highly evaporative surfaces |

Years with higher precipitation generally correspond to increased NDWI values, though the magnitude of response varies by cluster. Some clusters remain spatially stable year to year, while intermediate zones show frequent transitions — indicating higher sensitivity to rainfall fluctuations. The driest clusters show limited responsiveness to precipitation, likely reflecting salt-crust or evaporative zones.

## Discussion

These clustering patterns align with prior geochemical and sedimentological research describing Sambhar Lake as a spatially heterogeneous evaporative system. NDWI doesn't directly measure water depth or salinity, and surface reflectance in saline environments can also be influenced by biological activity (e.g. algal or microbial blooms) — so observed clusters likely reflect combined surface processes rather than water presence alone.

## Conclusion

NDWI-based clustering effectively reveals structured yet dynamic surface water patterns in Sambhar Lake across multiple years. Combining satellite imagery, simple unsupervised learning, and climate context supports an intuitive, visual understanding of a complex environmental system, and can serve as a starting point for deeper hydrological or geochemical investigation.

## Repository structure

```
sambhar-lake-analysis/
├── Sambhar_Lake_Analysis.ipynb        # Main analysis notebook
├── data/                               # Satellite imagery / derived data
├── docs/
│   └── Remote Sensing of Sambhar Lake.pdf # Full written report
├── requirements.txt
└── README.md
```

## Getting started

### Option 1: Run in Google Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/gkm2004/sambhar-lake-analysis/blob/main/Sambhar_Lake_Analysis.ipynb)

### Option 2: Run locally

```bash
git clone https://github.com/YOUR-USERNAME/sambhar-lake-analysis.git
cd sambhar-lake-analysis
python3 -m venv venv
source venv/bin/activate       # Windows: venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook Sambhar_Lake_Analysis.ipynb
```

## Full report

See [`docs/Remote Sensing of Sambhar Lake.pdf`](Remote Sensing of Sambhar Lake.pdf) for the complete write-up, including all cluster-stability charts and yearly NDWI cluster maps.

## Future work

- [ ] Add more recent imagery as it becomes available
- [ ] Correlate area/cluster change with rainfall more rigorously (beyond qualitative comparison)
- [ ] Explore salinity or water quality alongside surface water indices
- [ ] Ground-truth clusters against in-situ hydrological or geochemical data

## License

This project is licensed under the MIT License.
