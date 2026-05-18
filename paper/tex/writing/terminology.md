# Terminology

## Preferred terms

| Use | Avoid |
|---|---|
| source characterization | source imaging, source localization |
| source mapping | source imaging, source localization |
| covariance matrix fitting (CMF) | covariance-based method |
| focus grid | source grid, scan grid |
| source strength | source power, source level |
| microphone array | sensor array |
| snapshot | sample, frame |

## Correlation terms

- `incoherent sources`: the source CSM `Q` is diagonal at the analyzed frequency, so all cross-spectral terms vanish.
- `correlated sources`: the source CSM `Q` has at least one nonzero off-diagonal entry.
- `coherent sources`: a special case of correlated sources with fixed phase relation and maximal correlation magnitude.

## Abbreviations

| Abbreviation | Full form |
|---|---|
| CMF | covariance matrix fitting |
| CMF-C | covariance matrix fitting for correlated sources |
| CSM | cross-spectral matrix |
| DUN | deep unfolded network |
| FISTA | fast iterative shrinkage-thresholding algorithm |
| LISTA | learned iterative shrinkage-thresholding algorithm |
| SNR | signal-to-noise ratio |

## Style notes

- Use `source characterization` for source properties such as source strength, location, spectrum, or directivity.
- Use `source mapping` for the spatial distribution reconstructed on the focus grid.
- Do not use `beamforming` as a synonym for CMF or other inverse methods.
- Use `robust` only with a stated qualifier when it does not mean robustness to dictionary mismatch.
