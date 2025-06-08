# “A tree of data, from the root to leaves”

Thinking non-linearly has often exposed us to a wider range of efficient management of data. The Tree data structure breaks away from the traditional linear setups and goes to a more “Hierarchical” approach. The parent-child-ancestor-descendant relationship makes data organization much more natural and intuitive.  [Are tree-based data structures really that useful? : r/compsci](https://www.reddit.com/r/compsci/comments/1cvtlmh/are_treebased_data_structures_really_that_useful/)

A tree always starts with a root node - the origin of everything. While a tree can be empty but if it’s not, it’s bound to have one single root node. From this root, the structure branches out into other nodes appearing in a parent-child relation. The nodes are connected with edges, forming multiple sub-trees within the larger tree. 

We may consider each node v in a tree T which has a unique parent node w. Every node with parent w is a child of w and nodes having the same parent are called siblings. Nodes with no children are called leaf nodes. Tree’s have paths which show us how the nodes are connected, symbolized by the direction of the edges from one node to another. 
![[Tree Representation.png]]

The important rule for a tree is that it cannot have a cyclic path to it. Consider the path : A-C-E-A . It’s a cyclic path and represents an acyclic graph in general terms. We can’t have that. The nodes must branch off like that of a real tree. 
![[Tree Height & Depth.png|400]]
Each tree has a level to it, classified according to its hierarchical pattern. We then have the concept of depth/height as well. 

Depth of a node is the level in which that node is present. In a more formal definition - It’s the number of edges present in its path from the root node. 

Height on the other hand, is the number of edges on the longest path from the node to a leaf. We can see the root node A having height of 3 while B, C have different heights.

