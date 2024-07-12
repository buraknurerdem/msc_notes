Some notes and reports about my M.Sc. study, which is in progress.

### Things to Check
- ~~Does different ODD_HOLE_TERMINATION_BATCH_SIZE lead to the same objective value when solved to the optimum?~~ 
  **Answer:** Yes. This was for double checking. Our expectations are correct. The same input graph leads to the same optimal objective value under different parameter sets. In some cases, it is also possible to see examples of multiple optima. See the output logs in folder `Checked_1` that includes the outputs of two program runs with the same input graph but with different parameters. Both outputs have obj. value 9. However, one's output graph has 42 edges whereas the other has 48. The input graph has 49 edges. I checked several cases by eye which yielded no exception to the integrality of our program. For an exhaustive and complete test, a program could be written for checking all outputs that are solved to the optimum with the same input graph have the same optimal objective value. For now, I don't see a reason to do so.
- For a few small inputs. Check the feasible solutions found along the way. How do they approach to the optimal output graph? Do they more look alike the empty or complete graphs or the input graph? This would help us identify what *first nontrivial solution* is?
  **Failed Attempt 1:** I printed the feasible solutions along the algorithm and drew them. The small instances are too trivial, generally, the first non-empty, non-complete graphs are the optimal. By eye, it is not doable to come to a conclusion.
  **Next Attempt:** For the feasible graphs found along the way, print out graph density which would be an indication of *distance* to the input graph. Also the change: (change on the graph = change_count / input_graph_edge_count).
  Comparing *distance* from the input graph considering these two sets of numbers will provide a more easier, reliable and quantifiable approach.

### To Do
- Add to txt output:
	- All parameter options. There are some that are missing.
- Add to csv output:
	- All parameter options, explicitly.
	- The ratio of change on the graph = change_count / input_graph_edge_count
	- Is the output empty or complete graph (bool)
	- add real input density
	- add approximate input density
	- add output density
	- ALSO check output txt to see if anything useful is left out on the csv output.
- Program 2: Change the structure of adding cuts: In program 1, anti odd-holes are searched for only if there exist no odd-holes. This leads to asymmetric time results of time performance depending on graph density. Another approach could be to search both odd-holes and anti odd-holes and add all as cuts. This is expected to lead to symmetric results on said comparisons. More importantly, this phenomenon could be the base of a strategy to use according to the graph density. The said strategy is to check for odd-holes (program1) or anti odd-holes, if there exist none, then check for the other. Which one to use would be dependent on the graph density.

### Side Studies
- Only Edge Addition and Only Edge Deletion:
	- Graph Structural Questions:
		- For what kind of graphs does the minimum modification number equals to the minimum edge **addition** number?
		- For what kind of graphs does the minimum modification number equals to the minimum edge **deletion** number?
		- Can we deduce results based on density?
			- For example, when density is high (>0.5), what can we say that the min modification solution add addition ratio? My expectation is high, since it is more favorable to add edges when density is high.
			- For example, when density is high (>0.5), can we say that add deletion opt. obj. value > min. modification obj. value **always**?
		- To be able to answer these questions, the possibility of multiple optima in the min. modification case must be handled with care.
	- Optimization:
		- How does the difference in objective fnc. affect the time performance? (Notice the number of d.v. are decreased. For edge addition case, d.v.s are defined for only non-edges instead of all vertex pairs)
- Can we utilize the valid inequalities used for minimum hitting set or minimum set cover problems?
- Probabilistic Studies on the structures of the random graphs:
	- The expected number of C_5s
	- The expected number of odd-holes
	- The expected number of both odd-holes and anti odd-holes
- How can heuristics be used to improve the cutting plane algorithm?
	- On adding cuts
	- On proposing a solution (graph)
- We can change the input graph, instead of random erdös-renyi. How would this affect the approach? Can the approach be changed according to the structures of input graphs. Some possible input types:
	- C_5 free graphs
	- Generalized Split + Perturbation

### Other Notes
- 15 minute for TIME_LIMIT for each program run is ideal. However, one can inquire the effect of the TIME_LIMIT parameter to the optimality graph under certain inputs (order,density) and certain parameters (ODD_HOLE_TERMINATION_BATCH_SIZE, etc.)
- The *most suitable* ODD_HOLE_TERMINATION_BATCH_SIZE is probably dependent on the expected number of odd-holes (both odd-holes and anti odd-holes depending on the counting principle).
- ON_HOLD. We have talked about a strategy(or parameter) which is a time limit that starts after the *first feasible solution* is found. I am skeptical. First nontrivial graph? How does this fall on the experiment space of the current work?