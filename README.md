# SymbolicAI

- Core Problem : Neural networks often predict each output independently. But tasks like path prediction require the outputs to form a valid global structure. Independent predictions lead to broken paths, loops, or disconnected edges. The goal is to inject structural knowledge into neural network training so outputs become globally consistent.

- Boolean Representation : In the grid graph example, every edge has a variable : true if the edge is in the path, false otherwise. The neural network outputs a probability for each edge. Together, these probabilities describe how likely every possible edge combination, every possible path is.

- Encode structure as logical constraints : Next, we formally describe what a valid path means using propositional logic rules. Examples: the path must start at the source, end at the destination, maintain flow through intermediate nodes and not branch. These rules are written as a single logical formula that exactly defines a valid path.

- Semantic Loss : To train the neural network, we penalize it when the total probability of valid paths is low. The paper uses the negative log of that probability because it gives strong gradients, works well with gradient descent, and matches standard cross-entropy when constraints are simple.

- Train with combined loss : Standard prediction loss + weighted semantic loss. The normal loss teaches local accuracy, while semantic loss enforces global structure. In experiments, per-edge accuracy changes little, but the percentage of outputs that form valid paths jumps dramatically (7% to 70%), showing that global structural constraints have been successfully enforced.
