> Imported from [DeepFin at 32370b099f6d](https://github.com/jjoshua2/DeepFin/blob/32370b099f6d8d4ec965de135e70a752fc95a7a9/scratchpad/bt4_joint20/publication_20260908_softsf_results_v1/tactical_attenuation/PLAN.md). [Original bytes](https://github.com/jjoshua2/DeepFin-research/blob/8536ec99471478efee257e9b7bbeb4d3e614854b/scratchpad/bt4_joint20/publication_20260908_softsf_results_v1/tactical_attenuation/PLAN.md) and source history remain available. Historical commands and local artifact paths describe their original run.

# SF tactical attenuation: descriptive readiness

Use only the existing qualified 4,096-row training sample. No new engine calls,
inference, corpus rewrite or training. This measures intervention size, not whether
SF is right. The original corpus has d9 observations; search-depth stability is
unavailable and must not be claimed.

For each legal move let delta be best raw effective SF cp minus its raw effective
cp, and B be normalized BT4 policy sharpened at temperature 0.5. On rows without
mate-encoded scores, define weight = max(0.1, exp(-max(0, delta - gap)/100)).
Normalize B times weight. Inspect gap 100 and 200 cp as two substantive readiness
choices, not a fitted sweep. All mate-containing rows remain unchanged in this
first candidate; raw mate encodings are not ordinary cp. The 0.1 bound is a
relative multiplier, not an absolute probability floor.

Report weighted mass exposed to suppression, total variation, top-move changes,
entropy change and mate-row exclusion. Verify probabilities, preserved ordering
and ratios among unattenuated moves, and unchanged mate rows. Preserve input hashes.
Weights are inherited sampling weights, not iid evidence. No strength verdict,
optimal threshold, tactical correctness or population confidence interval follows.

Budget: one pass through 64 saved NPZ files, CPU 2/3 with numerical threads 2,
maximum 120 seconds, no GPU. A later launch requires exact stored-target semantics,
matched B100 control, unchanged value targets and a separate playing protocol.
