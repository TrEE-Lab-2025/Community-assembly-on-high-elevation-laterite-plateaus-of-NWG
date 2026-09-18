Objective 1.1: Computing biodiversity metrics

•	Data required: 
Species presence/absence per site (for richness), 
species abundance per site (for Shannon-Wiener diversity)

•	Data matrices used: 
site_species_qualitative_data_matrix.csv 
site_species_quantitative_data_matrix.csv

•	Analysis done: 
Species richness (sum of species present per site),
Shannon-Wiener diversity index (H′)

Objective 1.2: Testing species-area relationship (Spearman correlation)

•	Data required: 
Species richness per site, 
plateau area per site 

•	Data matrices used: 
site_attributes_data_matrix.csv: It contains latitude, longitude, area, species richness, and species diversity per site (richness and diversity values as computed in Objective 1.1)

•	Analysis done: Spearman's rank correlation between species richness and plateau area

 
Objective 2.1: Partitioning beta diversity into turnover and nestedness

•	Data required: 
Species presence/absence per site

•	Data matrices used:
site_species_qualitative_data_matrix.csv

•	Analysis done:
Multi-site Sørensen beta diversity (βSOR), 
partitioned into turnover (βSIM) and nestedness (βSNE) components

Objective 2.2: Testing distance-decay relationship

•	Data required: 
Pairwise compositional dissimilarity (Jaccard and Bray-Curtis) at species level, 
genus- and family-level aggregated abundance, 
pairwise geographic distance between sites

•	Data matrices used: 
geographic_distance_matrix.csv
jaccard_dissimilarity_matrix.csv: Computed using species-level data
bray_curtis_dissimilarity_matrix.csv: Computed using species-level data
site_genus_data_matrix.csv
site_family_data_matrix.csv

•	Analysis done:
Mantel tests (Jaccard × distance, Bray-Curtis × distance),
repeated Bray-Curtis Mantel test at genus and family resolution

 
Objective 3.1: Characterizing environmental gradients across plateaus (PCA)

•	Data required: 
Monthly historical climate data (July–October) extracted per transect from the WorldClim database at 1 km² spatial resolution: elevation (m), mean/minimum/maximum temperature (°C), water vapour pressure (kPa), wind speed (m s⁻¹), solar radiation (kJ m⁻² day⁻¹), and precipitation (mm). 

Values were averaged across transects within each site and month to produce one row per site × month combination (n = 32). 

•	Data matrices used:
site_environment_data_matrix.csv: site × month environmental data matrix
(n = 32 rows = 8 sites x 4 months)

•	Analysis done:
1. Averaged environmental values across transects within each site and month, then standardized (z-scored) all eight variables. 
2. Computed a pairwise Pearson correlation matrix among the eight variables and excluded one variable from each highly correlated pair (|r| > 0.8), retaining five uncorrelated variables: elevation, mean temperature, water vapour pressure, solar radiation, and precipitation (Fig. S3). 
3. Performed a Principal Component Analysis (PCA) on this reduced, standardized set using `prcomp()`. 
4. Extracted the percentage of variance explained by each axis and the variable loadings on each axis (Table S5). 
5. Visualized the ordination with site × month scores plotted along PC1 and PC2, with convex polygons grouping points by site, point shapes indicating sampling month, and arrows showing the loading vectors of each environmental variable (Fig. 3B). 
Objective 3.2: Spatial and environmental predictors of species turnover (GDM)

•	Data required: 
Species presence-absence and abundance per site,
site-level environmental variables (elevation, mean temperature, water vapour pressure, solar radiation, precipitation),
site coordinates for geographic distance.

•	Data matrices used: 
site_species_qualitative_data_matrix.csv
site_species_quantitative_data_matrix.csv 
site_environment_data_matrix.csv

•	Analysis done:
Generalised Dissimilarity Modelling: two models, one based on Jaccard dissimilarity (presence-absence) and one based on Bray-Curtis dissimilarity (abundance)

 
Objective 3.3: Quantifying and disentangling the role of environment and space in shaping community structure

•	Data required: 
Species abundance per site, resolved at monthly resolution (July–October),
site × month environmental data used in Objectives 3.1 and 3.2,
site-level coordinates for deriving UTM coordinates and dbMEMs.

•	Data matrices used: 
site_species_monthly_quantitative_data_matrix.csv: site x species x month
site_environment_data_matrix.csv: site × month environmental data matrix (same file used in Objectives 3.1 and 3.2)
site_attributes_data_matrix.csv

•	Analysis done: 
1.	Redundancy Analysis (RDA): Hellinger-transformed the species abundance matrix, reduced the environmental predictors to the same five uncorrelated variables retained in Objective 3.1, forward-selected significant predictors, and fit the final RDA. Tested significance via global, per-axis, sequential (Type I), and marginal (Type III) permutation tests, with permutations additionally restricted within sites to account for repeated monthly sampling.
2.	Variance partitioning: Projected site coordinates to UTM, derived distance-based Moran's Eigenvector Maps (dbMEMs) to represent spatial structure, and forward-selected significant dbMEM axes. Partitioned variation in species composition among the RDA-selected environmental variables (X1), significant dbMEM axes (X2), and pure spatial coordinates (X3), with permutation tests confirming the significance of each component.

Compilation of data matrices used:
1.	site_species_qualitative_data_matrix.csv
2.	site_species_quantitative_data_matrix.csv
3.	site_attributes_data_matrix.csv
4.	geographic_distance_matrix.csv
5.	jaccard_dissimilarity_matrix.csv
6.	bray_curtis_dissimilarity_matrix.csv
7.	site_genus_data_matrix.csv
8.	site_family_data_matrix.csv
9.	site_environment_data_matrix.csv
10.	site_species_monthly_quantitative_data_matrix.csv
