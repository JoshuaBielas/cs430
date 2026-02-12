1. Sudoku has 81 variables (cells) but only 27 constraints (9 rows + 9 columns + 9 boxes). Explain why each constraint actually represents multiple binary constraints between pairs of cells. How many total binary constraints exist in a 9×9 Sudoku?

    each unit has 36 binary constraints (9 choose 2). There are 36 * 27 binary constraints in a 9x9 Sudoku. This leads to 972 binary constraints.

2. A Sudoku puzzle is only solvable if it has exactly one solution. From a CSP perspective, what would it mean for a puzzle to have zero solutions versus multiple solutions? How would you detect these conditions?

    If a CSP has zero solutions, it would mean there is no way of satisfying the constraints. If a CSP has multiple solutions, it would mean there is multiple ways of satisfying the constraints. You would detect these conditions based on whether there is still multiple values in a domain after all of the constraints are satisfied (p. 190)

3. Naive backtracking explores the search tree depth-first without any lookahead. Describe a scenario where this leads to significant wasted work—specifically, where the algorithm makes many assignments before discovering a conflict that could have been detected earlier.

    If the algorithm makes multiple assignments before it ensures that those assignments meet the other constraints, it will have to waste work by backtracking and removing values that it has assigned. Then it will have to assign new values.

4. The solver selects variables in a fixed order (left-to-right, top-to-bottom). Explain why this ordering is arbitrary and potentially inefficient. What information about the CSP state would be useful for choosing which variable to assign next?

    This is inefficient because the best way to solve Sudoku is by repeatedly finishing the unit that is closest to being solved. It's fixed order is arbitrary because there are many ways of solving Sudoku. Information about what variables have been used the most, and information about units that are the most populated would be useful for choosing whcih variable to assign next. 

5. Notice that the number of assignments grows dramatically for harder puzzles. Using the branching factor concept, explain why CSP search complexity is exponential. If each empty cell has an average of 5 possible values, approximately how many nodes would be explored in the worst case for a puzzle with 50 empty cells?

    CSP search complexity is exponential because there are many choices for each cell, and it is important to check that a choice for a value matches other constraints. Each cell will have an average of 5 values as options. For a cell at depth d, you must consider every combination for the cells before it. 5^50 = 8.88 * 10^34. 

6. Forward checking maintains arc consistency between the current variable and its neighbors. Explain what happens when a neighbor's domain becomes empty (domain wipeout). Why is this more efficient than discovering the conflict through multiple future assignments?

    When a neighbor's domain becomes empty, it means that there are no values that can be placed in that cell. This means that you can't place the value you are currently trying to in the cell. This is more efficient to discover at this point because it eliminates much of the backgtracking. 

7. Notice the "domain reductions" metric. Each reduction eliminates a potential branch of the search tree. Calculate approximately how many search nodes were pruned by forward checking in the example. How does this relate to the speedup observed?

    9*9*9*9 = 6561-1140 = 5421
    5421/6561 * 100% = 82.62%

    Approximately 17.38% of the search nodes were pruned by forward checking. This is pretty similar to the amount that it sped up. It was about 20% faster which is similar to the 17.38& of the nodes removed. 

8. The AC-3 algorithm uses a queue to process arcs. Explain why arcs must be re-added to the queue when domains change. What would happen if we only processed each arc once without re-queuing?

    It would think that it solved it when it actually didn't. We would end up with duplicated or misplaced elements within units. If they weren't readdedto the queue, then they wouldn't be able to be changed in response to changes made elsewhere.

9. Some easy Sudoku puzzles can be solved by AC-3 alone without any search. Explain what this reveals about the puzzle's structure. What property must a puzzle have for AC-3 to solve it completely through constraint propagation?

    It reveals that Sudoku puzzles are structured on a path of solving. Solving one cell adds a constraint on another cell which can lead to it being solveable. If this path is followed through the puzzle, it can be solved without search. It must have the property that solving one leads to constraints that allow for solving the others. We need to be able to reduce the domains for cells down to 1 possible value.


10. The MRV heuristic chooses the "most constrained" variable first, which seems counterintuitive—why tackle the hardest decisions first? Explain the "fail-first" principle and how detecting failures early reduces total search effort.

    Choosing the most constrained variable first allows there to be a higher chance that we place the correct value in the node because the constraints limit what values can be placed there. The fail-first principle says that we want to reach failure as fast as possible if we are going to fail. This is achieved by making the hard decisions first. It reduces total search effort because it makes backtracking occur over smaller distances. 

11. The LCV heuristic orders values by how little they constrain neighbors. Describe the philosophical difference between MRV (fail-first for variables) and LCV (succeed-first for values). Why do these opposite strategies work well together?

    The philosophical difference is that MRV wants to fail as fast as possible if its going to, so it can spend less time backtracking. LCV wants to succeed first without failing which can work well if it finds a solution to the problem without failing. MRV is focused on a single cell at a time. LCV looks at a set of cells that effect MRV. When LCV and MRV agree on a value for a cell, we can be pretty confident that it is a good choice. 

12. The degree heuristic breaks ties in MRV by choosing variables with the most unassigned neighbors. Explain the reasoning: why would constraining more variables make a variable selection better? Consider both immediate effects and future search reduction.

    Constraining more variables gives fewer options. The immediate effect is that you can narrow the domain of a cell and be more confident you are placing the correct value. It impacts future search reduction by significantly decreasing it because it limits how many values there are that can be placed in the future nodes. 

13. Observe how the performance gap between naive backtracking and intelligent techniques grows with puzzle difficulty. Explain why the benefit of heuristics and constraint propagation is more pronounced on harder puzzles. What does this reveal about the structure of the search space?

    The performance gap grows very quickly. The benefits of heuristics and constraint propagation are more pronounced on harder puzzles because the heuristics and constraint propagation are able to reduce the number of choices for each cell while the naive approach will still consider impossible combinations. The search space has a very high branching factor, and early eliminations significantly reduce the search space. 

14. The "hard" puzzle has only 21 givens compared to 36 for the easy puzzle. Discuss why fewer givens doesn't always mean harder—the pattern and distribution of givens matters. What makes a Sudoku puzzle truly "hard" from a CSP perspective?

    What matters more than the number of givens in a sudoku puzzle is how they are arranged. How hard it is to solve units is more important than number of givens. A Sudoku puzzle is "hard" from a CSP perspective if it has a higher branching factor. 

15. If you were building a production Sudoku solver, which combination of techniques would you choose? Consider the trade-off between implementation complexity, computational cost, and solving power. Would you use the same configuration for all puzzles or adapt based on puzzle characteristics?

    Starting with Heuristics and then switching to AC-3 when the problem is more constrained might be a good option because the Heuristics perform the best on hard puzzles and AC-3 performs the best on easy and medium puzzles. If the problem is very simple, using Naive might be the best because the code is simpler. 

16. The min-conflicts heuristic chooses values that minimize immediate conflicts. Compare this greedy, local decision-making to backtracking's systematic exploration. Why does backtracking's ability to undo multiple decisions give it an advantage for CSPs?

    When the min-conflicts heuristics chooses a value, it isn't considering future conflicts. It just considers the immediate conflicts. This can cause it to run into bigger conflicts in the future. Backtracking works forward and then backtracks as necessary if it sees a conflict. Backtracking has an advantage for CSPs because if you can't complete avoid conflicts, it needs to be able to backtrack out of them and make new choices. 

17. Local search performs well for some CSPs (like N-queens) but poorly for Sudoku. Hypothesize about what properties make a CSP amenable to local search versus requiring systematic search. Consider factors like constraint density, solution density, and landscape topology.

    Smaller branching factors are good for local search. There is more constraints in Sudoku than N-queens. Each of the queens in n-queens is the same, but there are multiple values that can be chosen for a cell in Sudoku. There are also more board constraints in Sudoku. More cells need to be filled in Sudoku. One value can't eliminate entire rows and columns like a queen can. 

18. Z3 uses a declarative approach where you specify constraints and let the solver find solutions. Compare this to the procedural backtracking approaches from earlier exercises. What are the advantages and disadvantages of each paradigm for solving CSPs?

    Z3 is able to use the specific constraints to essentially do the same thing as backtracking without the lookahead. It can use its constraints to determine not to choose a value. Z3 runs the puzzle until it finds a conflict. When it reaches a conflict, it creates a new rule to prevent the conflict from happening again. An advantage of z3 is that its rules that it creates when it reaches a conflict prevent it from running into conflicts more than once. It is also faster than backtracking. An advantage to backtracking is that it is a simpler algorithm. 

19. The Distinct() constraint in Z3 is a built-in primitive that handles "all different" efficiently. Earlier exercises checked constraints pairwise manually. Explain how a solver could optimize the Distinct() constraint internally using techniques beyond pairwise checking. Consider arc consistency and conflict analysis.

    Bipartite matching is a way of checking all relationships at once. It "finds the maximum number of pairs (edges) that can be selected from a bipartite graph such thta no two edges share a common vertex" (Google AI Overview). Bipartite matching is more efficient than manual pairwise checking. The solver can use bipartite matching to optimize the distinct constraint. AC-3 complexity is O(n^2d^3). Bipartite matching complexity is O(sqrt(n)nd). Bipartite matching is faster. 

20. Z3 uses techniques like conflict-driven clause learning (CDCL) which learns from failures to avoid repeating similar mistakes. Compare this to plain backtracking which forgets why branches failed. How does learning from conflicts relate to the constraint propagation and heuristics you've explored in previous exercises?

    Plain backtracking doesn't prevent future conflicts or future need for backtracking. Conflict-driven clause learning is a way of not repeating the same mistake. This eliminates a lot of backtracking. CDCL is sort of like a heuristic in that we can make certain branches be recognized based on a pattern. Then they can be avoided. 