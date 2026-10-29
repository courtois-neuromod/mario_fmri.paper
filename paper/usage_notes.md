# Usage Notes

The dataset is intended for reuse in naturalistic-task neuroimaging, skill-learning, and
brain-encoding studies. The `mario_fmri` package reproduces every analysis in this
descriptor through `invoke` tasks, and the companion
[`mario.tutorials`](https://github.com/courtois-neuromod/mario.tutorials) notebooks
illustrate end-to-end use on a single participant, including event-based GLM analysis,
reinforcement-learning agents trained on the same gameplay, and brain-encoding models mapping
agent activations onto BOLD. Because every play is reconstructable from the deterministic
`.bk2` replays, users can derive arbitrary additional annotations beyond those provided.
The strongest reuse opportunity for replication is the independently acquired *mariostars*
dataset, which shares participants and game engine.

**Limitations.**
The cohort is small by design ($N=5$, dense rather than wide) and a single game is studied;
results emphasise within-subject, individualised modelling rather than population inference.
Gameplay actions and in-game events can co-occur, so condition regressors are partially
correlated; the discovery and practice phases are imbalanced in
duration ({numref}`Table %s <tab-behavior>`). The cross-dataset comparison with *mariostars*
uses the same five participants and therefore tests replication across tasks and acquisitions,
not generalisation to an independent cohort. **[TODO: add any further game-specific caveats.]**
