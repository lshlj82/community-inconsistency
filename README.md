# Consistency landscape explorer

An interactive, single-file web demo of the community inconsistency measures introduced in:

> Daekyung Lee, Sang Hoon Lee, Beom Jun Kim, and Heetae Kim,
> "Consistency landscape of network communities,"
> *Physical Review E* **103**, 052306 (2021).
> [doi:10.1103/PhysRevE.103.052306](https://doi.org/10.1103/PhysRevE.103.052306)

The demo runs a stochastic community detection algorithm many times at each resolution γ. It then measures how much the results disagree and draws the resulting "consistency landscape". Everything runs in the browser, and there is nothing to install or build.

## Features

- **Resolution scan.** Plots the partition inconsistency Ω and the mean number of communities ⟨n_c⟩ against γ, with standard-error bars. Ranges where Ω ≈ 1 and ⟨n_c⟩ sits on an integer plateau above 1 are shaded automatically, and the threshold can be adjusted.
- **Built-in networks.**
  - Zachary's karate club network.
  - The single-level planted community model (Sec. III A 1 of the paper).
  - The double-level hierarchical model (Sec. III A 2).
  - Any pasted edge list, weighted or unweighted.
- **Node-level view.** Click any γ to see the network colored by community, by membership inconsistency Ψᵢ, or by companionship inconsistency Φᵢ. A table ranks the most inconsistent nodes.
- **Bring your own partitions.** Paste the output of any community detection algorithm, one partition per line. The demo returns:
  - Ω for the whole set of results
  - Ψᵢ and Φᵢ for every node
  - the distinct configurations and how often each appeared
  - the element-centric similarity matrix between them

## Measures implemented

Each result is compared with the others only by which nodes are grouped together; the community label numbers are ignored.

| Measure | Paper | Meaning |
|---|---|---|
| Partition inconsistency Ω | Eq. (2) | Effective number of independent configurations in the ensemble (1 = every run agrees) |
| Element-centric similarity S_αβ | Eq. (1) | Similarity between two configurations (Gates *et al.*, 2019) |
| Membership inconsistency Ψᵢ | Eqs. (3)–(5) | Effective number of distinct memberships of node i |
| Companionship inconsistency Φᵢ | Eqs. (6)–(7) | How far node i's co-occurrence probabilities are from 0 or 1 |

## Implementation notes

- **Detection algorithm.** The paper uses GenLouvain. This demo uses the Louvain method for modularity with a resolution parameter, Q = Σᵢⱼ [Aᵢⱼ − γ kᵢkⱼ / 2m] δ(gᵢ, gⱼ), with a new random node order on every run. Landscapes are therefore qualitatively similar to the paper's but not numerically identical.
- **Element-centric similarity.** For partitions, the personalized PageRank on the cluster-induced element graph has the closed form f_ij = d/|Cᵢ| + (1 − d)δᵢⱼ. The 1/(2d) normalization in Eq. (1) therefore cancels d. The demo uses this exact closed form, which needs only the per-node overlap |ψ_iα ∩ ψ_iβ|.
- **Normalization of Φ.** The printed Eq. (7) uses 1/(m − 1). This demo normalizes by N − 1, the number of other nodes, which gives the stated bounds 0 ≤ Φᵢ ≤ 1. This matches the original definition in H. Kim and S. H. Lee, *Phys. Rev. E* **100**, 022311 (2019).
- **Standard error of Ω.** Estimated from 10 random, equal-sized subsamples of the runs at each γ. The paper uses 50 subsamples.
- **Model network sizes.** The planted models default to smaller sizes than in the paper so that scans finish in seconds in a browser:
  - single-level: 150 nodes (paper: 1200)
  - double-level: 270 nodes (paper: 900)

  Sizes and densities can be changed in the controls.

## Citation

If you use this demo in academic work, please cite the original paper:

```bibtex
@article{Lee2021Consistency,
  author  = {Lee, Daekyung and Lee, Sang Hoon and Kim, Beom Jun and Kim, Heetae},
  title   = {Consistency landscape of network communities},
  journal = {Physical Review E},
  volume  = {103},
  number  = {5},
  pages   = {052306},
  year    = {2021},
  doi     = {10.1103/PhysRevE.103.052306}
}
```

## Credits

- **Method:** Daekyung Lee, Sang Hoon Lee, Beom Jun Kim, and Heetae Kim.
- **Implementation:** this interactive demo was built with **Claude Opus 5.5** by [Anthropic](https://www.anthropic.com).

This is an independent implementation and is not affiliated with or endorsed by the paper's authors.

## License

No license has been chosen yet. Add a `LICENSE` file (for example, MIT) before publishing if you want others to reuse the code.
