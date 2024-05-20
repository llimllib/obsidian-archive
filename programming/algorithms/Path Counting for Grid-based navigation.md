---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://www.keanw.com/2022/06/a-paper-on-our-space-analysis-algorithm-in-the-journal-of-artificial-intelligence-research.html

> Counting the number of shortest paths on a grid is a simple procedure with close ties to Pascal’s triangle. We show how path counting can be used to select relatively direct grid paths for AI-related applications involving navigation through spatial environments. Typical implementations of Dijkstra’s algorithm and A* prioritize grid moves in an arbitrary manner, producing paths which stray conspicuously far from line-of-sight trajectories. We find that by counting the number of paths which traverse each vertex, then selecting the vertices with the highest counts, one obtains a path that is reasonably direct in practice and can be improved by refining the grid resolution. Central Dijkstra and Central A* are introduced as the basic methods for computing these central grid paths. Theoretical analysis reveals that the proposed grid-based navigation approach is related to an existing grid-based visibility approach, and establishes that central grid paths converge on clear sightlines as the grid spacing approaches zero. A more general property, that central paths converge on direct paths, is formulated as a conjecture.

The authors wanted to generate paths from grid-based pathfinding algorithms that were straighter and more direct. 

Full paper here https://jair.org/index.php/jair/article/view/13544