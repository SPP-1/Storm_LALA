
# LALA-Induced Thermal Response Across Northwestern Hawaiian Coral Reefs

## Preliminary analysis
> **Status:** Preliminary / exploratory analysis  
> **Study period:** August 2026  
> **Storm:** LALA   
> **Primary variable:** Sea-surface temperature (SST)  

---

# Abstract

Tropical cyclones can induce pronounced sea-surface cooling through enhanced upper-ocean mixing, entrainment, and other storm-driven processes. However, the magnitude and spatial structure of these cold wakes over coral-reef environments remain poorly resolved, particularly at reef scales.

Here, we examine the thermal response of coral reefs in the Hawaiian region to Tropical Storm LALA using gap-reconstructed GOES-18 sea-surface temperature observations. Coral-reef polygons were consolidated according to a predefined 22 independent reef groups. For each reef group, the shortest distance to the continuous LALA track and the time of closest storm passage were calculated. DAY and NIGHT SST records were analyzed separately, and reef-group SST anomalies were referenced to a storm-relative baseline from −120 to −48 h before closest passage.

Post-passage cooling showed a clear spatial relationship with proximity to LALA. Median SST anomalies during the first 72 h following closest passage became progressively weaker with increasing distance from the storm track. The relationship was significant for both DAY observations (Pearson \(r = 0.513\), \(p = 0.0147\)) and NIGHT observations (\(r = 0.608\), \(p = 0.0027\)). Reef groups located closest to the storm track showed the strongest cooling, including Group 17 at approximately 9 km from the track and Group 18 at approximately 18 km.

A weighted wind-swath exposure index was additionally developed from the spatial overlap of each reef buffer with the 34-, 50-, and 64-kt LALA wind-swath polygons. Wind exposure was more strongly associated with post-passage SST cooling than track distance alone. Wind exposure explained approximately 40% of the DAY SST anomaly variance and 43% of the NIGHT variance, compared with approximately 26% and 37%, respectively, for track distance.

Track distance and wind exposure were themselves strongly correlated (\(r = -0.878\)), indicating substantial collinearity. Multiple-regression analysis therefore showed limited benefit from including both variables simultaneously. Wind exposure alone provided the lowest leave-one-out cross-validation error for both DAY and NIGHT observations.

In contrast, the orientation between the local LALA motion vector and the principal reef-chain axis showed no significant relationship with post-passage SST response. These preliminary results suggest that storm proximity and associated wind exposure are primary controls on reef-scale SST cooling during LALA, whereas reef-chain orientation does not appear to exert a first-order influence.

---

# 1. Introduction

Tropical cyclones can produce substantial changes in upper-ocean thermal structure through wind-driven mixing, entrainment of cooler subsurface water, enhanced turbulent heat fluxes, and changes in local circulation. The resulting reduction in sea-surface temperature is commonly referred to as a **tropical-cyclone cold wake**.

Cold-wake magnitude varies considerably in space and time and depends on several interacting factors, including storm intensity, translation speed, ocean stratification, mixed-layer depth, storm-track geometry, and local bathymetry. Coral-reef environments may respond differently from adjacent open-ocean waters because of their shallow depth, complex bathymetry, island wakes, reef morphology, and local circulation.

The Northwestern Hawaiian Islands provide an opportunity to investigate how a tropical storm modifies reef-scale thermal conditions across a broad gradient of storm exposure. During August 2026, LALA passed through the central Pacific and approached multiple coral-reef systems at distances ranging from less than 10 km to more than 500 km.

The objective of this preliminary analysis is to quantify the reef-scale SST response to LALA and determine whether the magnitude of cooling is related to:

1. distance from the LALA storm track;
2. cumulative exposure to the storm wind swath; and
3. the geometric orientation between local storm motion and the reef-chain axis.

The analysis focuses on storm-relative SST variability rather than predefined PRE/STORM/POST categories, allowing the timing and magnitude of reef cooling to be examined relative to each reef group's individual closest-passage time.

---

# 2. Data and Methods

## 2.1 GOES-18 SST observations and DAY/NIGHT compositing

Sea-surface temperature (SST) observations were obtained from the NOAA GOES-18 Advanced Baseline Imager (ABI) ACSPO Level-3C SST product (collection `G18-ABI-L3C-ACSPO-v2.90`) through the NASA PO.DAAC data service. The product was acquired for the study domain spanning 178.4°W–155.0°W and 16.7°–28.5°N for the period from 1 to 25 August 2026. The downloaded NetCDF files contain geolocated SST fields together with associated quality information.

Prior to temporal compositing, the individual GOES-18 L3C SST observations were screened using the product `quality_level` variable. Only pixels with `quality_level ≥ 4` were retained. SST values outside the physically plausible range of 0–45°C were excluded, and values reported in Kelvin were converted to degrees Celsius when necessary. Longitudes were normalized to the −180° to 180° convention, and input grids were checked for spatial consistency before compositing. 
To separate the diurnal SST cycle, the GOES-18 observations were divided into DAY and NIGHT periods using Hawaiian Standard Time (HST; UTC−10). For each local calendar date, the NIGHT composite included observations acquired from 18:00 HST on the previous day to 06:00 HST on the current day, whereas the DAY composite included observations acquired from 06:00 to 18:00 HST on the current day. 

Within each 12-h DAY or NIGHT window, all valid GOES-18 SST scenes were stacked on the common spatial grid and a pixel-wise median was calculated from the available valid observations. Scenes containing no valid SST pixels were discarded, and files whose latitude–longitude grids did not match the reference grid were excluded from the composite. The use of the median reduced sensitivity to individual anomalous retrievals while retaining the spatial structure of the SST field. 

One NIGHT and one DAY SST composite were generated for each local date when valid observations were available. The resulting composites were saved as georeferenced GeoTIFF files in WGS84 geographic coordinates (EPSG:4326). 

## 2.2 DINEOF reconstruction of DAY and NIGHT SST

The 12-h DAY and NIGHT SST composites were reconstructed independently using a Data Interpolating Empirical Orthogonal Functions (DINEOF) framework. Separate DAY-only and NIGHT-only time series were maintained throughout the reconstruction and subsequent reef-scale analysis to avoid mixing the diurnal SST cycle.

Based on the compositing scheme described above, DAY and NIGHT products were associated with representative observation times of approximately 23:00 UTC and 11:00 UTC, respectively. These representative times were used to preserve the temporal ordering of the DAY and NIGHT records relative to the storm track and reef-specific closest-passage times.

For each period, the SST GeoTIFFs were stacked into a three-dimensional time series and reshaped into a space-by-time matrix. Only spatial pixels containing at least two valid observations were retained as candidate ocean pixels. SST was reconstructed directly in its native temperature space without logarithmic transformation.

Before reconstruction, the space–time matrix was screened to remove pixels and time steps with insufficient valid observations. Missing locations were considered eligible for interpolation when observational support existed in either the temporal or spatial dimension. Temporal connectivity was evaluated within a radius of three neighboring time steps, while spatial connectivity was assessed using the surrounding 3 × 3 pixel neighborhood.

The DINEOF reconstruction was performed iteratively using truncated singular value decomposition. Candidate solutions containing between 1 and 15 empirical orthogonal functions (EOFs) were evaluated. For each EOF number, a subset of observed SST values was withheld for cross-validation, and reconstruction accuracy was quantified using the root-mean-square error (RMSE) between reconstructed and withheld observations. Iterations continued until the change in cross-validation RMSE fell below \(10^{-4}\) or a maximum of 60 iterations was reached. The EOF number producing the minimum cross-validation RMSE was selected for the final reconstruction.

The reconstruction preserved all originally observed SST values and filled only missing pixels satisfying the spatial or temporal interpolation criteria. Missing locations without sufficient observational support remained unfilled. The reconstructed matrices were subsequently restored to their original spatial grids and exported as separate DAY and NIGHT GeoTIFF time series for reef-scale SST analysis.

Maintaining separate DAY and NIGHT reconstructions was particularly important for the interpretation of storm-induced cooling. Nighttime SST is less affected by daytime shortwave heating and the formation of a shallow near-surface warm layer, and therefore provides a useful indicator of the underlying storm-related cooling response. DAY SST was retained as a complementary measure to characterize the full diurnal thermal response.


## 2.3 Coral-reef analysis units

Coral-reef polygons were obtained from the `WCMC008_CoralReefs_2018_v4` dataset and manually reorganized in ArcGIS to define reef-scale analysis units that better represented individual island reef systems.

The original coral-reef polygons were first separated into individual polygon features. These polygons were then manually regrouped according to their spatial relationship to the surrounding islands. Coral-reef polygons associated with the same island were combined and treated as a single reef analysis unit. In addition, spatially separated reef polygons associated with neighboring islands were combined into the same analysis unit when the separation between them was less than 15 km. This procedure was intended to represent closely connected reef systems as a single spatial unit rather than treating every individual polygon as an independent reef.

Following this manual regrouping procedure, a total of 22 reef analysis units were defined across the study region (Figure 1). All polygons belonging to the same reef unit were merged into a single geometry before SST extraction.

A 1-km buffer was generated around each reef geometry to define the surrounding SST sampling region. For each reconstructed DAY and NIGHT SST composite, all valid raster cells intersecting the reef buffer were identified, and their median SST was calculated as the representative temperature of that reef unit. Additional statistics, including the mean, 25th and 75th percentiles, number of valid pixels, and spatial coverage, were calculated for quality assessment. The median SST was retained as the primary reef-scale statistic because it is less sensitive to isolated anomalous pixels or localized reconstruction artifacts than the mean.

<img width="1448" height="784" alt="Screenshot 2026-08-28 at 11 13 09 AM" src="https://github.com/user-attachments/assets/88bb7865-e385-4d3a-bc65-bf8299a2e7dc" />


## 2.4 In situ temperature validation

The reconstructed GOES-18 SST fields were evaluated against independent in situ water-temperature observations from National Data Buoy Center (NDBC) stations located within and adjacent to the study region. Water temperature (`WTMP`) was used as the in situ reference variable. Because GOES-18 SST represents the ocean skin temperature whereas NDBC observations measure bulk water temperature at the station or platform, the comparison was interpreted as an evaluation of consistency between the reconstructed satellite SST field and independently observed near-surface water temperature rather than as an exact measurement-equivalence test.

The NDBC observations were processed using the same DAY and NIGHT temporal framework applied to the GOES-18 composites. Observation times were converted from UTC to Hawaii Standard Time (HST; UTC−10 h) and assigned to either the DAY period (06:00–18:00 HST) or NIGHT period (18:00–06:00 HST). Observations collected between 18:00 and 24:00 HST were assigned to the following NIGHT composite, while observations collected between 00:00 and 06:00 HST were assigned to the NIGHT composite of the same local date. For each station and DAY/NIGHT period, the median in situ water temperature was calculated to provide a temporally consistent comparison with the corresponding 12-h satellite composite.

Reconstructed SST was extracted at each NDBC station coordinate from the corresponding DAY or NIGHT DINEOF raster. The raster cell containing the station location was sampled first. If that pixel did not contain a valid reconstructed SST value, the median of valid SST pixels within a $3 \times 3$ neighborhood centered on the station was used. Station–composite pairs were retained only when both a valid in situ median temperature and a valid reconstructed SST estimate were available.

Validation performance was quantified using the coefficient of determination ($R^2$), root-mean-square error (RMSE), and mean bias. Bias was defined as

$$
\text{Bias} = T_{\text{DINEOF}} - T_{\text{NDBC}}
$$

such that positive values indicate reconstructed SST warmer than the corresponding NDBC observation and negative values indicate reconstructed SST cooler than the in situ observation. Statistics were calculated separately for DAY and NIGHT observations and for all matched observations combined.

To reduce the influence of isolated anomalous matchups, outliers were identified from the residuals between reconstructed and in situ temperatures. Outlier detection was performed independently for each station and for DAY and NIGHT observations using a median absolute deviation (MAD)-based modified z-score:

$$
z^{*} = 0.6745 \frac{r_i - \tilde{r}}{\text{MAD}}
$$

where $r_i$ is the DINEOF–NDBC temperature residual and $\tilde{r}$ is the median residual for the corresponding station and observation period. Matchups with $|z^{*}| > 3.5$ were classified as outliers and excluded from the reported validation statistics, while remaining visible in the time-series diagnostics for quality assessment.

Each matchup was additionally classified according to whether valid satellite SST was present before DINEOF reconstruction. A matchup was classified as **original-existing** when valid SST was already available in the original unfilled GOES-18 composite at the sampled location. A matchup was classified as **DINEOF-filled** when one or more pixels contributing to the station SST estimate were missing in the original composite and subsequently reconstructed by DINEOF. This distinction was used to assess whether reconstructed SST values remained consistent with the independent in situ observations.

Missing-data conditions were also characterized at both local and scene scales. For each NDBC matchup, a local missing-SST rate was calculated from the original unfilled GOES-18 composite using a station-centered $5 \times 5$ pixel window:

$$
M_{\text{local}} = 100 \frac{N_{\text{missing}}}{N_{\text{window}}}
$$

where $N_{\text{missing}}$ is the number of pixels without valid SST within the local window and $N_{\text{window}}$ is the total number of pixels evaluated.

A scene-scale missing rate was calculated independently for each DAY and NIGHT composite from the proportion of the final valid DINEOF domain that did not contain valid SST before reconstruction. This quantity was expressed as

$$
M_{\text{scene}} = 100 - P_{\text{original}}
$$

where $P_{\text{original}}$ is the percentage of final DINEOF-valid pixels that already contained valid SST in the original composite. Under this definition, the scene missing rate is equivalent to the fraction of the final valid SST field supplied by DINEOF reconstruction. The local and scene-scale metrics were used as diagnostic indicators of satellite data availability and to examine whether validation errors increased under more spatially extensive missing-data conditions.



## 2.5 LALA track processing and storm-relative reef exposure

Preliminary best-track data for LALA were obtained from the National Hurricane Center (NHC) and converted to a geospatial point dataset. Storm positions were ordered chronologically and connected sequentially to construct a continuous representation of the LALA trajectory across the study region.

For each of the 22 reef analysis units, the minimum distance between the complete reef geometry and the continuous LALA track was calculated. To obtain distances in metric units while minimizing projection distortion, each reef unit and the surrounding storm-track segments were transformed to a local azimuthal equidistant projection centered on the corresponding reef geometry.

Rather than calculating reef-to-storm distance only from the discrete NHC best-track positions, the minimum distance was evaluated against each line segment connecting consecutive storm locations. This allowed the closest point of approach to occur anywhere along the continuous storm trajectory and avoided constraining the distance estimate to an individual reported best-track position.

For the track segment associated with the minimum reef-to-track distance, the fractional position of the closest point along the segment was determined. The corresponding closest-passage time was then linearly interpolated between the timestamps of the two neighboring NHC track positions. Each reef analysis unit was therefore assigned both a minimum distance to the continuous LALA track and a reef-specific time of closest passage.

Because LALA reached different reef systems at different times, all subsequent SST observations were expressed relative to the closest-passage time of the corresponding reef. Storm-relative time was calculated as

$$
t_{\text{relative}} = t_{\text{SST}} - t_{\text{closest}}
$$

where $t_{\text{SST}}$ is the representative time of the corresponding DAY or NIGHT SST composite and $t_{\text{closest}}$ is the interpolated time of closest LALA passage for that reef analysis unit.

Under this convention, $t_{\text{relative}} = 0$ represents the time of closest passage for each reef independently. Negative storm-relative times indicate observations before closest passage, whereas positive values indicate observations after passage. This transformation places spatially separated reef systems within a common storm-relative temporal framework and allows their thermal responses to be compared despite differences in the calendar date and time of storm exposure.

The minimum reef-to-track distance was retained as the primary geometric measure of storm exposure. For visualization and interpretation, reef analysis units were additionally grouped into four distance classes:

| Distance class | Minimum distance to LALA track |
|---|---:|
| Near | $\le 100\text{ km}$ |
| Intermediate | $> 100\text{ to } 200\text{ km}$ |
| Distant | $> 200\text{ to } 400\text{ km}$ |
| Far control | $> 400\text{ km}$ |

These categories were used primarily for grouped time-series visualization and comparison of the storm-relative SST response. Statistical relationships between storm exposure and reef cooling were evaluated using the continuous minimum track distance rather than the categorical classes.


## 2.6 Reef-specific SST anomalies and thermal-response metrics

Absolute SST varied among reef systems because of geographic location, background oceanographic conditions, and differences between DAY and NIGHT observations. To isolate temperature changes associated with LALA from these background differences, SST anomalies were calculated relative to a reef-specific and period-specific pre-storm baseline.

For each reef analysis unit, the baseline period was defined as

$$
-120 \le t_{\text{relative}} \le -48\text{ h}
$$

corresponding to approximately five to two days before the time of closest LALA passage. DAY and NIGHT observations were treated independently so that normal diurnal differences in SST did not influence the estimated storm response.

For each reef and observation period, the baseline SST was defined as the median temperature within this pre-passage interval:

$$
SST_{\text{baseline}} = \text{median}\left(SST_{-120 \le t_{\text{relative}} \le -48}\right)
$$

The reef-specific SST anomaly was then calculated as

$$
SST' = SST - SST_{\text{baseline}}
$$

Negative values of $SST'$ therefore indicate cooling relative to the pre-LALA thermal state of the same reef and DAY/NIGHT period, whereas positive values indicate warming relative to the baseline. This normalization removes differences in absolute background temperature among reef systems and allows their thermal responses to be compared directly.

The post-passage thermal response was evaluated primarily during the first 72 h following closest passage. Three complementary metrics were calculated for each reef analysis unit and separately for DAY and NIGHT observations. First, the minimum SST anomaly between 0 and 72 h was used to represent the maximum post-passage cooling:

$$
SST'_{\text{min},0\text{--}72} = \min\left(SST'_{0 \le t_{\text{relative}} \le 72}\right)
$$

Second, the median anomaly during the same 0–72 h interval was used as the primary measure of the sustained post-storm thermal response:

$$
SST'_{\text{med},0\text{--}72} = \text{median}\left(SST'_{0 \le t_{\text{relative}} \le 72}\right)
$$

Finally, because the strongest cooling response did not necessarily occur at the instant of closest passage, the median anomaly between 24 and 72 h was calculated to characterize the delayed component of the thermal response:

$$
SST'_{\text{med},24\text{--}72} = \text{median}\left(SST'_{24 \le t_{\text{relative}} \le 72}\right)
$$

These response metrics were subsequently compared with minimum reef-to-track distance to evaluate whether the magnitude and persistence of cooling varied systematically with storm proximity. DAY and NIGHT observations were analyzed separately throughout the storm-relative analysis to preserve differences in diurnal surface heating and to determine whether the LALA-associated cooling signal was consistently expressed across both observation periods.

# 3. Results

## 3.1 Temperature validation with in situ observations

The reconstructed GOES-18 SST fields showed strong agreement with independent NDBC water-temperature observations across the validation stations (Fig. 2). After removal of six statistical outliers, a total of 294 matched satellite–in situ observations were retained. For all observations combined, reconstructed SST explained 74.5% of the variability in the NDBC measurements (R
2
=0.745), with an RMSE of 0.219 °C and a small positive bias of 0.026 °C. The close clustering of observations around the 1:1 line indicates that the reconstruction preserved both the temporal variability and absolute temperature magnitude observed by the in situ measurements.

Validation performance was similarly strong for the DAY and NIGHT composites when evaluated separately. DAY observations produced the highest correspondence with the in situ measurements (R
2
=0.798, RMSE = 0.221 °C, bias = +0.095 °C; n=146). NIGHT observations showed slightly lower, but still strong, agreement (R
2
=0.736, RMSE = 0.218 °C, bias = −0.042 °C; n=148). The nearly identical RMSE between the two periods suggests comparable reconstruction accuracy during daytime and nighttime conditions, whereas the opposite signs of the small biases indicate a slight tendency toward warmer reconstructed temperatures during the day and cooler reconstructed temperatures at night. In both cases, the magnitude of the bias remained small relative to the observed SST variability.

To distinguish directly observed satellite retrievals from values introduced through reconstruction, each matchup was additionally classified according to whether valid SST was present in the corresponding pre-DINEOF composite. Of the 294 retained matchups, 200 corresponded to locations where valid SST already existed in the original composite, whereas 94 involved pixels filled by DINEOF. In Fig. X, DINEOF-filled observations are indicated by black marker boundaries. Both directly observed and reconstructed points generally follow the 1:1 relationship, indicating that the reconstructed values remain consistent with the independent in situ measurements rather than forming a distinct error population.

The dependence of validation error on missing-data conditions was also examined by comparing the absolute DINEOF–NDBC temperature difference with the fraction of unavailable SST surrounding each matchup prior to reconstruction (Fig. 3). Only a weak positive relationship was observed (r=0.191, R
2
=0.036, n=294). Thus, only approximately 3.6% of the variance in absolute validation error was associated with the local missing-data fraction. Although some of the largest errors occurred under relatively high missing-data conditions, similarly small errors were also present when missing-data fractions approached 100%. This result suggests that reconstruction accuracy was not strongly controlled by the instantaneous amount of missing SST surrounding the validation location and that DINEOF was generally able to maintain sub-degree, and typically much smaller, temperature errors even under strongly data-limited conditions.

Overall, the validation demonstrates that the reconstructed GOES-18 SST product reproduces the observed surface-temperature variability with high correspondence and low systematic error across both DAY and NIGHT periods. These results support the use of the DINEOF-reconstructed SST fields for subsequent analysis of the spatial and temporal evolution of the LALA-associated cold wake.
<img width="1790" height="1547" alt="image" src="https://github.com/user-attachments/assets/c3298189-6595-4073-a82c-91e71cd04e72" />
<img width="1781" height="1421" alt="image" src="https://github.com/user-attachments/assets/c04df0a9-817e-4911-b2b7-87ff5cf50dd0" />

(This image can go to Appendix)
<img width="1411" height="1423" alt="image" src="https://github.com/user-attachments/assets/c40c9850-975f-4791-9e99-11e60752d365" />
<img width="1486" height="733" alt="Screenshot 2026-08-28 at 11 01 58 AM" src="https://github.com/user-attachments/assets/eddd2f37-1705-416d-b8c8-e7dc5568c21f" />


## 3.2 Spatial gradient in LALA exposure and storm-relative reef cooling

The 22 coral-reef analysis units encompassed a broad gradient of exposure to LALA, with minimum distances to the continuous storm track ranging from 9.08 to 580.35 km (Table 1). The two closest reef units were Reef 17 and Reef 18, located 9.08 and 17.76 km from the track, respectively. Four reef units were located within 100 km of the storm track, five additional units occurred between approximately 100 and 200 km, and the most distant reefs were located more than 400 km from the storm trajectory.

Because the reef systems were distributed over a broad geographic region, the timing of closest passage varied considerably among reef units. Reef-specific closest-passage times ranged from 16 to 23 August 2026 (Table 1). SST observations were therefore evaluated relative to the individual closest-passage time of each reef, with $$t = 0$$ representing closest LALA passage.

### Table 1. Minimum distance from each coral-reef analysis unit to the continuous LALA track and interpolated time of closest passage.

| Reef unit | Distance to track (km) | Closest passage time | Distance class |
|---:|---:|---|---|
| 17 | 9.08 | 2026-08-20 23:37:42 | Near |
| 18 | 17.76 | 2026-08-21 00:43:33 | Near |
| 1 | 58.15 | 2026-08-16 02:16:59 | Near |
| 3 | 86.13 | 2026-08-16 17:06:23 | Near |
| 4 | 118.34 | 2026-08-16 19:58:24 | Intermediate |
| 2 | 122.31 | 2026-08-16 14:12:04 | Intermediate |
| 19 | 128.25 | 2026-08-21 01:25:29 | Intermediate |
| 5 | 130.21 | 2026-08-16 21:44:52 | Intermediate |
| 16 | 139.56 | 2026-08-21 04:29:09 | Intermediate |
| 6 | 206.60 | 2026-08-17 00:00:00 | Distant |
| 15 | 229.14 | 2026-08-21 08:49:30 | Distant |
| 7 | 254.43 | 2026-08-17 04:45:28 | Distant |
| 8 | 357.52 | 2026-08-17 20:31:09 | Distant |
| 9 | 358.67 | 2026-08-18 06:00:00 | Distant |
| 10 | 402.28 | 2026-08-18 08:52:38 | Far control |
| 11 | 415.36 | 2026-08-18 09:34:02 | Far control |
| 12 | 426.14 | 2026-08-18 13:35:48 | Far control |
| 20 | 426.65 | 2026-08-21 06:00:00 | Far control |
| 13 | 433.30 | 2026-08-18 14:37:34 | Far control |
| 14 | 462.79 | 2026-08-19 17:41:26 | Far control |
| 21 | 532.79 | 2026-08-23 12:00:00 | Far control |
| 22 | 580.35 | 2026-08-23 18:00:00 | Far control |

Storm-relative SST anomalies exhibited a clear spatial contrast among reefs with different distances from the LALA track (Fig. 1-4). Prior to closest passage, median DAY and NIGHT SST anomalies generally remained close to zero across all distance classes, consistent with the pre-storm baseline used to normalize the SST records.

For reefs located within 100 km of the storm track (Fig. 4), SST began to decrease around the time of closest passage and continued to decline during the following several days. Median DAY anomalies decreased from approximately −0.2 °C at closest passage to approximately −0.4 °C by 48–72 h after passage. NIGHT anomalies showed a similar but somewhat stronger post-passage response, reaching approximately −0.5 °C near 72 h after closest passage. The spread among reef units also increased after the storm, indicating substantial spatial variability in the magnitude of cooling within the near-track group. This response was especially pronounced at Reef Group 17, the reef unit closest to the LALA track (9.1 km). Prior to passage, DAY and NIGHT SST remained relatively stable at approximately 27.5–27.8 °C, whereas SST declined rapidly after closest passage. DAY SST fell to approximately 26.7 °C within 24 h and reached ~26.5 °C by 72 h, while NIGHT SST decreased to approximately 26.4 °C by ~84 h after passage. The resulting cooling of roughly 0.8–1.1 °C relative to the pre-storm temperature range highlights the stronger thermal response experienced by reefs located immediately adjacent to the storm track.
<img width="1289" height="690" alt="image" src="https://github.com/user-attachments/assets/09761263-342e-4bd1-a195-72b1f6663d0c" />


A comparable cooling response was observed among reefs located approximately 100–200 km from the track (Fig. 5). Median DAY and NIGHT SST anomalies were approximately −0.25 to −0.30°C at closest passage and generally remained negative during the subsequent 72 h. Minimum group-median anomalies of approximately −0.4°C were observed between 48 and 72 h after closest passage.

<img width="1289" height="690" alt="image" src="https://github.com/user-attachments/assets/5550eea2-b2fa-404f-83dd-5aa015ba3012" />

For reefs located 200–400 km from the LALA track (Fig. 6), SST anomalies were comparatively modest and showed only a weak storm-related cooling signal. Prior to closest passage, both DAY and NIGHT anomalies fluctuated close to the baseline, generally within approximately ±0.1 °C. Around closest passage, anomalies were slightly negative, near −0.1 °C, and both DAY and NIGHT temperatures decreased further during the following day, reaching approximately −0.2 to −0.25 °C at ~24 h after passage. Thereafter, the anomalies gradually weakened, remaining near −0.1 to −0.15 °C through approximately 48–72 h before becoming positive by ~100 h. The similar trajectories of DAY and NIGHT anomalies indicate that, at these distances, the thermal response was relatively small and broadly consistent across the diurnal cycle. The increasing spread at later times further suggests greater variability among reef units as the direct influence of the storm weakened.

<img width="1289" height="690" alt="image" src="https://github.com/user-attachments/assets/469fdae1-b861-40ce-bfcf-b51667d72834" />

Reefs located more than 400 km from the storm track exhibited an even weaker and less coherent response (Fig. 7). DAY and NIGHT anomalies remained close to zero before the storm and were only mildly negative during and after closest passage. DAY anomalies were approximately −0.1 to −0.15 °C around passage and remained within roughly −0.1 to −0.2 °C through 72 h, while NIGHT anomalies were generally slightly less negative, remaining between approximately 0 and −0.1 °C over much of the same period. Unlike the near-track reefs, these far-control reefs did not show a pronounced post-passage drop in SST. Instead, the anomaly trajectories were comparatively flat, with only gradual cooling followed by a return toward positive values by ~100 h. This muted response is consistent with a progressive reduction in storm-associated cooling with increasing distance from the LALA track.
<img width="1289" height="690" alt="image" src="https://github.com/user-attachments/assets/68832f5d-23ca-425f-8dd0-6263082629e1" />

Across the distance classes, the clearest pattern was a distance-dependent and lagged thermal response to LALA. The strongest negative SST anomalies were concentrated in reefs nearest the storm track, whereas the magnitude of cooling progressively weakened in the 200–400 km and >400 km groups. In the near- and intermediate-distance reefs, the largest negative anomalies generally developed after, rather than exactly at, closest passage, indicating that reef-scale surface cooling continued to intensify for approximately 1–3 days following the storm. This delayed response was evident in both DAY and NIGHT observations, although NIGHT anomalies were often slightly more negative and persistent. By contrast, reefs beyond 200 km showed only modest cooling, typically on the order of ~0.1–0.25 °C, and far-control reefs displayed little evidence of a distinct storm-driven thermal perturbation. Together, these results suggest that the SST response to LALA was not only spatially constrained by distance from the storm track, but also temporally lagged, with the most pronounced cooling emerging during the post-passage period rather than at the time of closest approach.

---

