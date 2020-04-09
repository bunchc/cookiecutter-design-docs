---
authors:
    - {{cookiecutter.full_name}}
date: {{cookiecutter.release_date}}
---

# Architecture Overview

This section provides an overview of the architecture. It should include a conceptual overview, and if relevant, a process / transaction flow diagram as well.

## Conceptual Overview

This should be an introduction paragraph for the diagram that follows. The components outlined in the diagram will explored in depth.

> **Note:** The diagram that follows is described in GraphViz dot format. When this document is processes by mkdocs, it will be rendered into a png.

```dot
digraph overview {
  rankdir="TD";
  style="rounded, filled";
  node[ shape=rectangle, colorscheme=x11, style="rounded, filled", fontsize=14 ];
  fontsize=18;
  labeljust="l";
  edge[ style=invis, fontsize=12, arrowhead=none ];

  // Define the various nodes
  inf1 [ label="Infra", fillcolor=aquamarine2 ];
  db1 [ label="Database", fillcolor=cadetblue2 ];
  dmz1 [ label="DMZ", fillcolor=cadetblue ];
  inf2 [ label="Infra", fillcolor=aquamarine3 ];
  db2 [ label="Database", fillcolor=cadetblue3 ];
  dmz2 [ label="DMZ", fillcolor=cadetblue4 ];
  gold [ label="Gold", fillcolor=gold ];
  silver [ label="Silver", fillcolor=ghostwhite ];
  vm1 [ label="VM1", fillcolor=slateblue ];
  vm2 [ label="VM2", fillcolor=slateblue ];

  subgraph cluster_architecture { // Draw the diagram
    label="Conceptual Overview";
    fontcolor=grey25;
    subgraph cluster_compute { // Compute box
      label="Compute";
      fillcolor=grey75;
      {
        rank=same;
        inf1 -> db1 -> dmz1;
      }
    }
    subgraph cluster_network { // Network box
      label="Network";
      fillcolor=grey75;
      {
        rank=same;
        inf2 -> db2 -> dmz2;
      }
    }
    subgraph cluster_storage { // Storage box
      label="Storage";
      fillcolor=grey75;
      {
        rank=same;
        gold -> silver;
      }
    }
    subgraph cluster_vms { // Draw the VMs
      style=invis;
      {
        rank=same;
        vm1 -> vm2;
      }
    }
    // Line up the graphs
    inf1 -> inf2 -> gold -> vm1;
    dmz1 -> dmz2 -> silver -> vm2;
    vm2 -> silver -> dmz2 -> dmz1 [style=dashed];
    vm1 -> gold -> inf2 -> inf1 [style=dashed];
  }
}
```
