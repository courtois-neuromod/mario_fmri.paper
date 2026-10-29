+++ {"part": "abstract"}

We present paired, densely sampled longitudinal functional MRI datasets in which five Courtois
NeuroMod participants played two versions of *Super Mario Bros.*: *mario*, the
original 8-bit game, and *mariostars*, its 16-bit remake, which updates the graphics while
preserving gameplay and level design. Together they comprise 171 participant-sessions, 666 runs,
4,606 level repetitions, and 115.2 hours of gameplay. *Mario* includes an ordered
discovery phase followed by randomized practice, whereas *mariostars* independently
samples the same levels, supporting longitudinal learning analyses and within-participant
cross-task replication. Deterministic replays make every gameplay frame reconstructable from
stored controller inputs and provide frame-accurate actions, in-game events, and audiovisual
features time-locked to the blood-oxygen-level-dependent signal. We document both datasets and
validate their signal quality and annotation-driven brain maps through within- and cross-dataset
reproducibility, multivariate discriminability, and cortical interpretability. The data are
released under a CC0 waiver through the Courtois NeuroMod distribution.

+++

# Background & Summary

Naturalistic paradigms — movies, narratives, and video games — are increasingly used to probe
brain function under rich, continuous, ecologically valid stimulation, and to build models that
generalise across cognitive domains {cite:p}`cneuromod2025`. Video games are a particularly
attractive naturalistic task: they couple continuous audiovisual input with goal-directed motor
action and a measurable performance signal, and they elicit learning over repeated play.
**[TODO: 1–2 sentences situating naturalistic / videogame fMRI and its advantages; add citations.]**

The Courtois NeuroMod project {cite:p}`cneuromod2025,boyle2025ccn` collects dense, individual-level
fMRI on a small cohort scanned repeatedly over years across many naturalistic and controlled
tasks, enabling deep, subject-specific modelling.
**[TODO: within this program we developed ways (what) of recording high-quality brain data during
action videogame play; description of shinobi.]**

Within this program, the *shinobi* dataset established an annotation-based analysis pipeline for
naturalistic gameplay, deriving interpretable general-linear-model (GLM) maps from frame-accurate
behavioral events {cite:p}`harel2025shinobi`. **[TODO: 1–2 sentences on what shinobi showed and
why a second game matters.]**

**[TODO: WHY MARIO ?]**

- high quality game
- action video game, covers a space not occupied by other datasets (e.g. VGDL)
- extensive game design literature
- implicit tutorial
- easy-to-use API via gym-retro

Here we jointly describe two longitudinal tasks acquired in the same five participants.
*Mario* uses the original 8-bit *Super Mario Bros.* and is structured into an
ordered *discovery* phase and a longer randomized *practice* phase. *Mariostars*
uses the 16-bit remake of the same game: its graphics are updated, while gameplay mechanics and
the 22 level designs remain intact. Its independent, randomized acquisition therefore varies
visual presentation and sampling protocol while retaining the underlying game. Together, the
tasks comprise 171 participant-sessions, 666 runs, and 4,606 level repetitions (115.2 hours of
play). This paired design supports longitudinal analyses of skill acquisition as well as
within-participant replication across game versions ({numref}`Fig. %s <fig-overview>`).

To establish the quality and reuse value of the dataset, we provide a technical validation of
the annotation-driven maps along three complementary axes — *reproducibility*,
*discriminability*, and *interpretability* — mirroring the shinobi analysis
pipeline {cite:p}`harel2025shinobi`, together with behavioral learning trajectories across sessions.
These analyses are intended to demonstrate data quality and reusability, and make no claims of
new scientific findings.
