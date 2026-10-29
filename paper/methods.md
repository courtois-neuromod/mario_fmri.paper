# Methods

All processing and analysis are implemented in the open-source `mario_fmri` Python
package and orchestrated through `invoke` tasks; every output is accompanied by a JSON
sidecar recording the git commit, parameters, and software versions. The validation pipeline
parallels the *shinobi* analysis {cite:p}`harel2025shinobi` so that results are directly
comparable across games.

## Participants

Five participants of the Courtois NeuroMod project (`sub-01`, `sub-02`,
`sub-03`, `sub-05`, `sub-06`; aged 31–47 at recruitment in 2018)
contributed in-scanner gameplay; `sub-04` did not take part. Prior gameplay experience
varied: `sub-01` and `sub-06` had previously played *Super Mario Bros.*;
`sub-01` and `sub-02` were regular video-game players; `sub-03` reported no
prior video-game experience. All participants provided informed consent for the open release of
their de-identified data {cite:p}`cneuromod2025,boyle2025ccn`. **[TODO: add the approving research
ethics board / protocol number.]**

## Stimulus and apparatus

Participants used the CNeuroMod fiber-optic MR-compatible controller {cite:p}`harel2023controller`
to play the original *Super Mario Bros.* running on a console emulator through OpenAI
`gym-retro` {cite:p}`openai2018gymretro`, recorded at 60 Hz. Because the game is fully
deterministic, only player inputs were stored; the companion `.bk2` replay files
reconstruct every play frame-by-frame.

## Experimental design

We use *run* for a single fMRI acquisition and *repetition* for a single play of a
level (from start to completion or loss of all three lives), each corresponding to exactly one
`.bk2` replay. Twenty-two of the original game's levels were used; underwater and boss
levels were excluded because their mechanics differ markedly from the rest. The experiment
comprised two phases: a *discovery* phase, in which every level was played in order with
unlimited attempts until at least one completion before advancing, and a longer *practice*
phase of randomly selected levels. At the end of each run, participants completed the Flow Short
Scale (FSS-2) plus two affect items (fatigue, frustration).

## MRI acquisition

Imaging was performed on a 3T Siemens Prisma Fit with a 64-channel head/neck coil at the Unité
de Neuroimagerie Fonctionnelle (CRIUGM). Functional runs used an accelerated
simultaneous-multislice gradient-echo EPI sequence (HCP-style; multiband factor 4,
TR $=1.49$ s, TE $=37$ ms, flip angle $52^\circ$, $2\times2\times2$ mm voxels, 60 slices,
acquisition matrix $96\times96$) {cite:p}`xu2013multiband,glasser2016hcp`. A short reversed
phase-encode acquisition was collected for susceptibility-distortion correction. Full
acquisition details follow the CNeuroMod core protocol {cite:p}`cneuromod2025`.

## fMRI preprocessing

Functional data were preprocessed with *fMRIPrep* 20.2.5 {cite:p}`esteban2019fmriprep`
(slice-timing correction disabled), producing preprocessed BOLD in
`MNI152NLin2009cAsym` space together with a standard set of confound regressors.
**[TODO: state the exact confound subset / nilearn load_confounds strategy used in the GLM.]**

## Behavioral annotation

Behavioral events were extracted from the deterministic `.bk2` replays and written as
BIDS `events.tsv` regressors. Three categories of frame-accurate events are provided:
button presses (every controller input), in-game events derived from emulator RAM (enemy kills,
deaths/hits, power-ups, coins, brick smashes, level completions), and one replay event per
repetition. Twelve gameplay conditions were modelled: six player actions (JUMP,
RUN/THROW, DOWN, LEFT, RIGHT, UP) and six game
events (*Kill*, *Hit*, *Powerup_collected*, *Coin_collected*,
*Brick_smashed*, *Level_complete*). Four continuous low-level features — frame
luminance, optical-flow magnitude, audio-envelope intensity, and per-TR button-press count —
were always included as nuisance regressors so that condition estimates are not confounded by
coarse audiovisual or motor drive. All regressors were convolved with the SPM canonical
hemodynamic response function; the design-matrix correlation structure (released as a derivative,
`invoke viz.regressor-correlations`) confirms condition estimates are not driven by
collinearity with the audiovisual/motor features.

## Behavioral learning trajectories

Level-matched learning trajectories were computed from the behavioral records of both datasets.
Repetitions were ordered by global play index separately within each participant, phase, and
level, then split into near-equal early, middle, and late thirds. Clear rate was computed over
decided repetitions, score as the median percentage of the maximum observed score for that level,
and time-to-clear as the median duration of cleared repetitions only. Metrics were computed per
level before levels were equally averaged within participant ({numref}`Fig. %sF–H <fig-overview>`).
For each dataset–phase–metric combination, early and late participant summaries were compared
with a one-sided paired Wilcoxon signed-rank test ($N=5$), using matched rank-biserial effect
sizes and Benjamini–Hochberg FDR correction across the nine tests. Separate released trajectory
derivatives use centred 10-repetition rolling means for completion, distance, hits, and duration.

## Signal quality: framewise displacement and tSNR

Two complementary signal-quality metrics were computed for every available run. Framewise
displacement (FD) was taken from the fMRIPrep confounds and summarised per run as the mean FD
and as the percentage of frames exceeding 0.5 mm, volume-weighted within participant. Temporal
signal-to-noise ratio (tSNR) was computed voxel-wise per run as the temporal mean divided by the
temporal SD, then aggregated hierarchically over runs, sessions, and participants, retaining the
across-run variance alongside the mean. Subject mean tSNR maps were projected to the inflated
fsaverage5 surface and rendered in four views (left and right lateral and medial) on a colour
scale shared by both datasets. Network summaries used the seven Yeo cortical networks and five
subcortical or cerebellar regions ({numref}`Fig. %s <fig-qc>`).

## General linear model

GLMs were fit with *nilearn* {cite:p}`abraham2014nilearn`. At the *session level*, a
fixed-effects model combined all runs within a session (SPM HRF; 5 mm FWHM isotropic Gaussian
smoothing; AR(1) noise model; drift handled through fMRIPrep confounds), producing one beta map
and one $z$-map per condition. At the *subject level*, session-level $z$-maps for each
condition were combined with a one-sample $F$-test across sessions (random effects). Statistical
maps can be thresholded with voxel-wise false-discovery-rate (FDR) control at $q<0.05$. These
session- and subject-level maps are the common input to the three map-based validation analyses
described next.

## Reproducibility: beta-map correlations

Map reliability was quantified as the voxel-wise Pearson correlation between full session-level
beta maps within the brain mask. For each annotation represented in both datasets, five tiers
were formed: same-participant session pairs and different-participant pairs separately within
*mario* and *mariostars*, and same-participant pairs across datasets. Correlations
were averaged within annotation and tier, with error bars reporting the SD of the contributing
map-pair correlations ({numref}`Fig. %sB <fig-validation>`). Directional tier comparisons used one-sided
paired Wilcoxon signed-rank tests across the 15 available annotations, with matched rank-biserial
correlations as effect sizes and Benjamini–Hochberg FDR correction across the four planned
comparisons.

## Discriminability: multivariate decoding

To test whether gameplay conditions evoke distinguishable spatial patterns, a linear support
vector machine {cite:p}`pedregosa2011sklearn` was trained separately for each participant on
session-level $z$-maps to classify 30 dataset–annotation classes (the 15 annotations shared by
both datasets, split by dataset). Models used leave-one-session-out cross-validation, voxel-wise
standardisation, and ANOVA feature screening retaining the top 20% of voxels. Fold confusion
counts were summed and row-normalised for display ({numref}`Fig. %sC <fig-validation>`). Subject-level
mean balanced accuracy was compared with the 30-class chance rate ($1/30$) using a one-sided
paired Wilcoxon signed-rank test across
the five participants; the matched-pairs rank-biserial correlation is reported as effect size.

## Interpretability: cortical effect overlays

Unweighted mean session contrast estimates for *Kill* and *Hit* were masked by the
corresponding subject-level maps using a two-sided cluster-forming threshold of $|z|>3.1$ and a
minimum extent of 10 voxels, projected to the inflated fsaverage5 surface, and displayed in four
views ({numref}`Fig. %sA <fig-validation>`). The overlay encodes support in *mario*,
*mariostars*, or both datasets and the absolute effect magnitude; effect sign is not
shown.

## Cross-dataset comparison with *mariostars*

A second CNeuroMod dataset, *mariostars*, was acquired independently with the same five
participants and the same MRI sequence. It uses a 16-bit remake of *Super Mario Bros.*
that updates the graphics while preserving the original gameplay mechanics and level designs,
and samples levels using a randomized protocol. The shared participants and game structure,
together with the altered visual presentation and independent acquisition, make
*mariostars* a within-participant, cross-version replication test for annotation-driven
maps. It is shown alongside *mario* throughout the Technical Validation figures
({numref}`Figs. %s <fig-overview>`–{numref}`%s <fig-validation>`); all displayed panels use empirical records or
processed derivatives from both tasks.

## Code availability

All analysis code is implemented in the open-source `mario_fmri` Python package
(<https://github.com/courtois-neuromod/mario_fmri>, version **[TODO: tag/commit]**), including the
GLM, MVPA, correlation/fingerprinting, and learning-trajectory analyses, together with the
`invoke` task runner that reproduces every figure and table. Dependencies are pinned for
reproducibility, and each output carries a JSON sidecar recording the git commit, parameters, and
software versions (Python, *nilearn*, *numpy*, *scipy*,
*scikit-learn*; exact versions: **[TODO: fill from provenance sidecars at release]**).
