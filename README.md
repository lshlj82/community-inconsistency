# Inconsistent communities · 비일관적인 커뮤니티

Interactive notes on the inconsistency of network communities: what to do with the different answers a stochastic community detection algorithm gives on the same network.

**Live demo:** https://lshlj82.github.io/community-inconsistency/ (한국어: https://lshlj82.github.io/community-inconsistency/ko.html)

Created by **Claude Opus 5.5**, based on the lecture slides “Appendix: inconsistency of network communities” by **Sang Hoon Lee** and the papers listed below. It is a companion to the demos on [network communities](https://lshlj82.github.io/network-community/) and [the Louvain algorithm](https://lshlj82.github.io/Louvain-algorithm/).

## What's inside

1. **An ensemble of answers.** A 13-node network with two dense groups joined by three bridge nodes, as in Fig. 1 of Kim & Lee (2019). Run the Louvain algorithm with a random node order once, 10 or 100 times at an adjustable resolution γ and watch the bridge nodes change sides. The distinct configurations and their frequencies p<sub>α</sub> make up the community ensemble.
2. **The co-occurrence matrix** φ<sub>ij</sub>, the fraction of realizations in which nodes i and j share a community (red: always accompanied, blue: always separated).
3. **Companionship inconsistency (CoI)** Φ<sub>i</sub> = 1 − Σ<sub>j≠i</sub>(1 − 2φ<sub>ij</sub>)²/(N − 1), shown next to betweenness centrality, which singles out only the central bridge node.
4. **Partition and membership inconsistency.** The element-centric similarity S<sub>αβ</sub> between configurations, the partition inconsistency Ω = (Σ p<sub>α</sub>p<sub>β</sub>S<sub>αβ</sub>)<sup>−1</sup> (the effective number of independent configurations), and the membership inconsistency Ψ<sub>i</sub> of each node, from Jaccard indices of its community memberships.
5. **The consistency landscape.** Scan γ, build an ensemble at each value, and plot Ω with the average number of communities ⟨n<sub>c</sub>⟩ for Zachary's karate club, a network of three planted groups, and a network of groups within groups. Consistent ranges (Ω ≈ 1 on an integer plateau of ⟨n<sub>c</sub>⟩) are shaded; click the chart to see the most probable configuration, or the MeI and CoI of every node, at that resolution.
6. **Bulk and boundary.** In a planted network with heterogeneous externality, push γ beyond the consistent range: MeI marks the bulk of the inconsistent region (it correlates positively with externality), CoI its boundary.
7. **In real networks.** Outsiders and multiplayers in social networks, and hierarchical community structure in the Chilean power grid and the photosystem II network, as reported in the papers.

The page uses its own JavaScript implementation of the Louvain algorithm (random node order, full multilevel aggregation), so the numbers differ in detail from the papers, which use GenLouvain.

## References

- H. Kim and S. H. Lee, “Relational flexibility of network elements based on inconsistent community detection,” *Physical Review E* **100**, 022311 (2019).
- D. Lee, S. H. Lee, B. J. Kim, and H. Kim, “Consistency landscape of network communities,” *Physical Review E* **103**, 052306 (2021).
- A. J. Gates, I. B. Wood, W. P. Hetrick, and Y.-Y. Ahn, “Element-centric clustering comparison unifies overlaps and hierarchy,” *Scientific Reports* **9**, 8574 (2019).
- V. D. Blondel, J.-L. Guillaume, R. Lambiotte, and E. Lefebvre, “Fast unfolding of communities in large networks,” *Journal of Statistical Mechanics* P10008 (2008).
- W. W. Zachary, “An information flow model for conflict and fission in small groups,” *Journal of Anthropological Research* **33**, 452–473 (1977).

## Running it

Everything is in `index.html` (English) and `ko.html` (Korean), with all CSS and JavaScript inline; MathJax and Google Fonts load from CDNs. Open either file in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

To publish with GitHub Pages, go to **Settings → Pages**, choose **Deploy from a branch**, and select the main branch and the `/ (root)` folder.
