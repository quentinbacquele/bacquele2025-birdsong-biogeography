# The Global Biogeography of Passerine Songs

Code and analysis scripts for the paper:

**Bacquelé Q.**, Barnagaud J.-Y., Violle C., Theunissen F., Mathevon N. (2025). *The global biogeography of passerine songs.*

## Abstract

Birdsongs are essential for courtship and territorial defense, and have long served as models for the evolution of vocal communication. However, the extraordinary diversity of songs has lacked a unifying framework accounting for their variation across species and environments. By analyzing the acoustic architecture of songs from over 3,000 passerine species across the globe, we show that songs are built from just eight elementary acoustic motifs. The morphology, the social organization, and the mating system influence which motifs compose the songs of a bird species. Notably, the robustness of an acoustic motif to information loss during propagation through the environment affects its global distribution. Our findings demonstrate that the evolution of animal signalling is channeled along geographically structured pathways, guided by the interplay of species biological characteristics and environmental physics.

## Interactive Visualization

Explore the global vocal repertoire of passerines: [acoustic-biogeography.vercel.app](https://acoustic-biogeography.vercel.app)

## Repository Structure

```
repo_bacquele_etal2025/
├── data/                    # Acoustic feature data (not included - see Data Availability)
├── mps/                     # Modulation Power Spectrum extraction
├── hypervolume/             # Acoustic space construction and motif clustering
├── phylogeny/               # Phylogenetic analyses
├── geo models/              # Spatial regression models
├── maps/                    # Global mapping visualizations
└── species level model/     # Species-level trait analyses
```

## Folders and Files

### `mps/` - Modulation Power Spectrum Extraction

| File | Description |
|------|-------------|
| `extract_mps.py` | Computes Modulation Power Spectra (MPS) from audio recordings. MPS quantifies spectro-temporal modulations encoding information such as species identity, individual identity, and singer quality. Uses a 500 ms window with 67% overlap and 2D Fast Fourier Transform. |

### `hypervolume/` - Acoustic Space and Motif Clustering

| File | Description |
|------|-------------|
| `acoustic_space_500ms.ipynb` | Jupyter notebook for constructing the 37-dimensional acoustic space from 116,792 passerine vocalizations using weighted PCA. Includes dimensionality reduction validation and UMAP visualization. |
| `gmm_grid_analyzer.py` | Gaussian Mixture Model clustering to identify the eight fundamental acoustic motifs (Flat Whistles, Slow/Fast/Ultrafast Trills, Slow/Fast Modulated Whistles, Harmonic Stacks, Chaotic Notes). Implements AIC/BIC model selection. |
| `dendogram.py` | Computes and visualizes Euclidean distances between acoustic motif clusters in the 37-PC space. |
| `species_cluster_distance_analysis.py` | Analyzes species-level acoustic motif usage patterns, including specialization indices and motif diversity per species. |

### `phylogeny/` - Phylogenetic Analyses

| File | Description |
|------|-------------|
| `consensus_tree.py` | Constructs majority-rule consensus tree from 1,000 phylogenetic trees (Jetz et al. 2012). Prunes tree to species in the acoustic dataset. |
| `phylo_signals.R` | Calculates phylogenetic signal (Pagel's Lambda, Blomberg's K) for acoustic motif usage. Compares signals between oscine and suboscine passerines. |
| `tree_refined.R` | Reconstructs ancestral states for dominant acoustic motifs and generates the circular phylogram visualization (Fig. 2A). |

### `geo models/` - Spatial Regression Models

| File | Description |
|------|-------------|
| `tei_geo_models copy.Rmd` | Spatial regression models (INLA SPDE) for the Transmission Efficiency Index (TEI). Tests effects of climate (temperature, humidity), vegetation structure, topography, human footprint, and phylogenetic diversity on global TEI patterns. |
| `fdis_geo_models_new.Rmd` | Spatial regression models for Functional Dispersion (FDis) of acoustic traits within species assemblages. |
| `Biomes_congruence.Rmd` | Tests alignment between acoustic motif distributions and terrestrial biome boundaries. Compares baseline spatial models with biome-effect models using WAIC and LCPO. |

### `maps/` - Global Mapping

| File | Description |
|------|-------------|
| `richness_map.py` | Maps passerine species richness and motif-specific richness per 1° x 1° grid cell globally. |
| `SES_maps.py` | Computes and maps Standardized Effect Sizes (SES) for motif prevalence using realm-constrained null models. Identifies over/under-representation of each acoustic motif relative to species richness. |
| `dominant_strategy_map.py` | Maps the dominant (most over-represented) acoustic motif per grid cell based on rank-normalized assemblage profiles. |

### `species level model/` - Species-Level Analyses

| File | Description |
|------|-------------|
| `species_model.Rmd` | Bayesian phylogenetic Dirichlet regression models testing how functional traits (social organization, body size, beak morphology, mating system) predict acoustic motif composition across species (Fig. 2B). |

## The Eight Acoustic Motifs

The study identifies eight fundamental acoustic motifs that structure passerine songs:

1. **Flat Whistles** - Pure tones with no frequency modulation; highest transmission efficiency
2. **Slow Modulated Whistles** - Whistles with slow frequency sweeps
3. **Fast Modulated Whistles** - Whistles with rapid frequency modulation; associated with smaller body size and polygyny
4. **Slow Trills** - Rhythmic repetitions at low rates
5. **Fast Trills** - Rhythmic repetitions at moderate rates
6. **Ultrafast Trills** - Extremely rapid rhythmic patterns
7. **Harmonic Stacks** - Complex harmonic structures; lowest transmission efficiency
8. **Chaotic Notes** - Atonal, broadband sounds

## Data Availability

Acoustic data were acquired from [xeno-canto](https://xeno-canto.org/). The processed acoustic features and metadata are archived at Zenodo (DOI: 10.5281/zenodo.XXXXXXX).

**Note:** The `data/` folder containing the acoustic feature matrices (`X_500ms.npy`, `metadata_500ms.npz`) is not included in this repository due to file size limitations. These files are available upon request or via Zenodo.

## Requirements

### Python
- Python 3.11+
- numpy, scipy, scikit-learn
- librosa (audio processing)
- soundsig (MPS computation)
- umap-learn (dimensionality reduction)
- matplotlib, seaborn (visualization)

### R
- R 4.4.3+
- ape, phytools (phylogenetics)
- brms (Bayesian modeling)
- R-INLA (spatial regression)
- mFD (functional diversity)
- sf, terra (spatial data)

## Citation

```bibtex
@article{bacquele2025biogeography,
  title={The global biogeography of passerine songs},
  author={Bacquel{\'e}, Quentin and Barnagaud, Jean-Yves and Violle, Cyrille and Theunissen, Fr{\'e}d{\'e}ric and Mathevon, Nicolas},
  journal={},
  year={2025}
}
```

## Authors

- **Quentin Bacquelé** - ENES Bioacoustics Research Lab, University of Saint-Etienne, France *(corresponding author: qbacquele@gmail.com)*
- **Jean-Yves Barnagaud** - CEFE, University of Montpellier, CNRS, France
- **Cyrille Violle** - CEFE, University of Montpellier, CNRS, France
- **Frédéric Theunissen** - Department of Neuroscience, University of California, Berkeley, USA
- **Nicolas Mathevon** - ENES Bioacoustics Research Lab, University of Saint-Etienne, France; Institut Universitaire de France

## Funding

- University of Saint-Etienne
- Ecole Pratique des Hautes Etudes
- University Paris-Sciences-Lettres (PhD stipend to QB)
- Labex CeLyA (NM)
- CNRS, Inserm
- Institut Universitaire de France (NM)
- ACOUCENE group (CESAB, French Foundation for Research on Biodiversity)

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgements

We are deeply grateful to the [xeno-canto](https://xeno-canto.org/) citizen science database and all its contributors.
