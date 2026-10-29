# Technical Validation

We validate the dataset by showing that the functional data are of high quality and that
annotation-driven beta maps are reproducible, discriminable, and interpretable, while the
longitudinal design captures behavioral skill acquisition. The same analyses are applied to the
independently acquired *mariostars* dataset (same participants) and shown alongside
*mario* in each figure as a within-cohort replication. Each subsection below reports one
analysis and carries the same name as the corresponding Methods subsection. All panels contain
empirical data; statistics are exported directly from the plotted derivatives by
`invoke paper.stats`.

(sec-validation-traj)=
## Behavioral learning trajectories

The longitudinal, two-phase design makes skill acquisition directly observable, providing a
behavioral validity check on the dataset. Repetition counts per level and the discovery/practice
split are summarised in {numref}`Fig. %sA–C <fig-overview>`. After controlling level difficulty by defining
early, middle, and late thirds within each level, the mean cleared-repetition rate across
participants increased from 45.6% to 65.5% over *mario* discovery and from 61.7% to
74.2% over *mario* practice ({numref}`Fig. %sF <fig-overview>`). Median normalized score likewise
increased from 31.6% to 41.4% during discovery and from 41.8% to 49.5% during practice
({numref}`Fig. %sG <fig-overview>`), while median time to clear decreased from 112.2 to 106.9 s and from
94.8 to 90.0 s, respectively ({numref}`Fig. %sH <fig-overview>`). In the independent *mariostars*
practice data, early-to-late summaries were comparatively stable for cleared-repetition rate
(73.6% to 74.9%) and normalized score (55.6% to 54.6%), while time to clear decreased from
93.5 to 88.4 s. One-sided early–late tests were directionally consistent with improvement for
the principal *mario* summaries, but none survived BH-FDR correction across the nine
planned tests (minimum adjusted $p=0.0938$). These five-participant results therefore document
the longitudinal behavioral content rather than establish population-level learning effects.
Beyond these summaries, per-level learning curves
(completion rate, horizontal distance, hits taken, and duration over chronological repetitions)
and spatial traces of the player's path — cleared repetitions versus deaths, localising difficult
sections — are released as derivatives (`processed/learning_curves/` and
`processed/learning_traces/`; `invoke traj.learning-curves`, `traj.traces`).

(sec-validation-qc)=
## Signal quality: framewise displacement and tSNR

Across 464 available *mario* QC runs, mean FD was 0.180 mm (median 0.177,
IQR 0.078), 67.5% of run means were below 0.2 mm, and 3.82% of volumes exceeded
0.5 mm. Across 180 *mariostars* QC runs, the corresponding values were 0.156 mm
(median 0.160, IQR 0.080), 77.8%, and 2.89% ({numref}`Fig. %sA <fig-qc>`). Mean temporal
signal-to-noise ratio (tSNR) maps are shown separately for every participant and dataset
({numref}`Fig. %sB,C <fig-qc>`), while the run, session, subject, network, and key-region summaries –
including the across-run tSNR variance – retain the complete within-subject hierarchy
({numref}`Fig. %sD <fig-qc>`). Mean tSNR pooled over networks and key regions was 31.4 in *mario*
and 32.0 in *mariostars*.

:::{figure} ../figures/fig2_signal_quality.png
:name: fig-qc
:width: 100%

**Signal quality control for *mario* and *mariostars*.**
Columns correspond to the same five participants throughout. (**A**) Distributions of
per-run mean framewise displacement (top; diamonds denote means) and percentages of volumes
exceeding 0.5 mm (bottom; volume-weighted within participant), with datasets offset within
each participant. The dotted top-panel reference is 0.2 mm. (**B**)
Participant-specific four-view cortical mean-tSNR maps for *mario*.
(**C**) Corresponding maps for *mariostars*; both datasets use the same color
scale. (**D**)
Within-participant tSNR summaries across runs, sessions, participants, seven cortical
networks, and five subcortical or cerebellar regions. Small translucent points are runs,
open points are sessions, diamonds are participant estimates, and network/region error bars
show the square root of the across-run tSNR variance. Brick-red and deep-navy marks denote
*mario* and *mariostars*, respectively.
:::

(sec-validation-repro)=
## Reproducibility: beta-map correlations

Across 15 shared annotations, mean same-participant correlations exceeded different-participant
correlations in both *mario* ($r=0.472$ vs. $0.221$) and *mariostars*
($r=0.495$ vs. $0.247$; both one-sided paired Wilcoxon $W=120$, FDR-adjusted
$p=3.05\times10^{-5}$, matched rank-biserial $r=1.00$; {numref}`Fig. %sB <fig-validation>`).
Same-participant cross-dataset correlations averaged $r=0.461$ and also exceeded the
different-participant tier of either dataset (both $W=120$, FDR-adjusted
$p=3.05\times10^{-5}$, rank-biserial $r=1.00$), supporting replication across independently
acquired tasks while preserving participant specificity.

(sec-validation-discrim)=
## Discriminability: multivariate decoding

The five participant-specific decoders achieved mean balanced accuracies of 0.814–0.831
(mean 0.826), well above the 30-class chance rate of 0.033 (one-sided paired Wilcoxon across
participants, $W=15$, $p=0.0313$, matched rank-biserial $r=1.00$;
{numref}`Fig. %sC <fig-validation>`). Strong annotation-matched diagonals occur for both datasets.
Off-diagonal structure is most visible for related motor classes, particularly directional
actions, while adjacent cross-dataset cells for the same annotation provide a direct visual
index of shared representations.

(sec-validation-interp)=
## Interpretability: cortical effect overlays

The *Kill* and *Hit* contrasts produce spatially structured, participant-specific
cortical patterns in both datasets ({numref}`Fig. %sA <fig-validation>`). Warm and cool regions show
dataset-specific suprathreshold support, whereas purple regions identify vertices supported in
both tasks. Cross-dataset overlap, especially for *Hit*, alongside individual variation
in extent, provides an anatomical complement to the quantitative map correlations without
assigning a post-hoc functional label to untested clusters.

:::{figure} ../figures/fig3_validation.png
:name: fig-validation
:width: 100%

**Technical validation** along three axes. (**A**) Interpretability:
unweighted mean session contrast estimates for *Kill* (upper row) and *Hit*
(lower row), masked by subject-level maps at a two-sided cluster-forming threshold of
$|z|>3.1$ and a minimum extent of 10 voxels, then projected to four inflated fsaverage5 views
(left/right lateral and medial). Red, blue, and purple encode support in *mario* only,
*mariostars* only, or both, respectively; colour intensity encodes absolute contrast
magnitude. (**B**) Reproducibility: per-annotation beta-map correlations across the
within-subject and between-subject tiers of each dataset and the within-subject cross-dataset
tier; error bars show $\pm 1$ SD across contributing session-map pairs. (**C**)
Discriminability: the across-participant mean row-normalised MVPA confusion matrix, accompanied
by the five participant-specific matrices. Rows are true classes and columns predicted
classes; each annotation's *mario*/*mariostars* pair is adjacent, so confusion
within a same-annotation pair indexes cross-dataset generalisation. All panels use empirical
derivatives.
:::
