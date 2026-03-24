# PCRAG

## Abstract

Knowledge Graph-based Retrieval-Augmented Generation (KG-RAG) systems typically retrieve facts independently, losing the relational structure that multi-hop reasoning requires. Restoring this structure through exhaustive graph exploration is computationally prohibitive on large graphs, creating a fundamental trade-off between retrieval quality and efficiency. To address this path coherence gap, we propose Path-Coherent Retrieval-Augmented Generation (PCRAG), a context-aware retrieval method that retrieves compact, path-coherent sets of triples organized into explicit reasoning chains via branch pruning. Starting from the most query-relevant nodes in each KG community, PCRAG explores the graph hop-by-hop, permanently discarding unpromising branches and their entire downstream subtrees to strictly bound the search space. Each candidate triple is evaluated through a composite score balancing direct query relevance, contextual non-redundancy, and relation pertinence. Experiments on two fact-checking benchmarks (MOCHEG and HoVer) show that PCRAG outperforms existing graph-based approaches in Accuracy and F1-score, while reducing context length by up to 97\% and execution time by over 98\% compared to the strongest baseline.



## Pruning Workflow

<table>
  <tr>
    <td align="center">
      <img src="imgs/Workflow_hop_1.svg" width="90%" />
      <br />
      <em>(a) Hop 1</em>
    </td>
    <td align="center">
      <img src="imgs/Workflow_hop_2.svg" width="90%" />
      <br />
      <em>(b) Hop 2</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="imgs/Workflow_hop_3.svg" width="90%" />
      <br />
      <em>(c) Hop 3</em>
    </td>
    <td align="center">
      <img src="imgs/Workflow_hop_4.svg" width="90%" />
      <br />
      <em>(d) Hop 4</em>
    </td>
  </tr>
</table>

**Figura 1:** Branch pruning within a community. The graph expands hop-by-hop from the root node $v^*$. At each hop, candidate triples are scored using Equation (1); a branch is expanded further only if its score exceeds the threshold $\tau$, otherwise the entire downstream subtree is discarded. Grey nodes represent the current frontier and blue nodes are those selected at the current hop.
