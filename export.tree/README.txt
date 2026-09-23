EEG and liking responses to sonic-seasoning soundscapes.

Per participant: one combined EEG file (eyes-open + eyes-closed baseline + ~17 s exposure to jungle and deconstruct
soundscapes), events.tsv marking segments, with liking ratings and baseline-state survey items in participants.tsv,
and stimulus audio in /stimuli. Released as recorded (EPOC X hardware bandpass only; no additional software filtering). Recording timestamps removed.
Participant IDs are de-identified (sequential sub-NN); the mapping to original recording IDs is held privately and
is not part of this dataset. See the associated Data in Brief article for full description.

All participants completed the four conditions in the same fixed order: eyes-open, eyes-closed, jungle, deconstruct.
The soundscape order was not counterbalanced.

QUALITY CHANNELS
----------------
Each EDF carries, alongside the 14 EEG channels, the manufacturer's continuously logged quality signals,
all sampled at 128 Hz and listed in each channels.tsv:
  CQ_<electrode>  per-channel contact quality, ordinal 0-4 (0 = no contact, 4 = good)
  CQ_Overall      overall contact quality, percent
  CQ_CMS, CQ_DRL  contact quality of the CMS and DRL reference electrodes, ordinal 0-4
  EQ_<electrode>  per-channel EEG quality, ordinal 0-4
  EQ_Overall      overall EEG-quality index, percent
  EQ_SampleRate   achieved/nominal sampling-rate ratio, -1 to 1
Across the 30 released sessions contact quality was uniformly high (CQ_Overall M = 100.0, SD = 0.2,
range 99.2-100.0; no channel fell below the acceptable level in any session), while the EEG-quality index
was considerably more variable (EQ_Overall M = 62.0, SD = 18.4, range 22.1-90.4). Re-users are encouraged
to apply their own thresholds to the per-channel indices rather than relying on a single summary.

EEGLAB USERS
------------
A processed, EEGLAB-ready version of the two soundscape conditions (jungle, deconstruct)
is provided under derivatives/eeglab/ as per-condition .set files that import directly
into an EEGLAB STUDY with conditions assigned. See derivatives/eeglab/README for details.
These derivative files contain the 14 EEG channels only; the quality channels are in the
raw EDFs at the repository root, which remain the primary, archival data.

READING THESE FILES
-------------------
Use an EDF reader that handles the EMOTIV header correctly (e.g. pyedflib in Python, or EEGLAB's
BIOSIG importer). Some general-purpose readers misinterpret the header and return flat or
zero-valued signals; if a channel loads as all zeros, the reader is at fault, not the data.
Always sanity-plot one channel after loading.

RESTING CALIBRATION (eyes-open / eyes-closed) — IMPORTANT NOTE
-------------------------------------------------------------
The eyes-open and eyes-closed segments are resting baselines, not length-matched counterparts
to the 17 s soundscape exposures. Each had a fixed intended duration of ~20 s, but in the
experiment builder each advanced on a participant-controlled "continue" button (not a hard
timer). Segment markers therefore span from segment start to that button press, so recorded
durations vary across participants: eyes-open 23.9-202.1 s (M = 32.1) and eyes-closed
26.3-63.4 s (M = 32.5). The button-press times were not logged and are unrecoverable.
The full segments are released unmodified; how to trim or average them is left to the user.
=> If a length-matched comparison with the soundscape exposures is wanted, the first 17 s of
   each calibration segment falls within the fixed instructed window for all participants and
   precedes any post-task advance interval.
