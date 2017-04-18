
# AI Planning Search

## Synopsis

In this project I create a planning search agent to solve deterministic logistics planning problems, defined in classical Planning Domain Definition Language (PDDL) for an Air Cargo transport system.

![Progression air cargo search](images/Progression.PNG)

- Part 1 - Planning problems:
	- Problems defined in classical PDDL (Planning Domain Definition Language)
	- Implemented Python methods and functions as marked in `my_air_cargo_problems.py`
	- Experimented and documented metrics
- Part 2 - Domain-independent heuristics:
	- Implemented relaxed problem heuristic in `my_air_cargo_problems.py`
	- Implemented Planning Graph and automatic heuristic in `my_planning_graph.py`
	- Experimented and documented metrics

## Project Details
### Part 1 - Planning problems

All problems are in the Air Cargo domain.  They have the same action schema defined, but different initial states and goals.

- Air Cargo Action Schema:
```
Action(Load(c, p, a),
	PRECOND: At(c, a) ∧ At(p, a) ∧ Cargo(c) ∧ Plane(p) ∧ Airport(a)
	EFFECT: ¬ At(c, a) ∧ In(c, p))
Action(Unload(c, p, a),
	PRECOND: In(c, p) ∧ At(p, a) ∧ Cargo(c) ∧ Plane(p) ∧ Airport(a)
	EFFECT: At(c, a) ∧ ¬ In(c, p))
Action(Fly(p, from, to),
	PRECOND: At(p, from) ∧ Plane(p) ∧ Airport(from) ∧ Airport(to)
	EFFECT: ¬ At(p, from) ∧ At(p, to))
```

- Problem 1 initial state and goal:
```
Init(At(C1, SFO) ∧ At(C2, JFK) 
	∧ At(P1, SFO) ∧ At(P2, JFK) 
	∧ Cargo(C1) ∧ Cargo(C2) 
	∧ Plane(P1) ∧ Plane(P2)
	∧ Airport(JFK) ∧ Airport(SFO))
Goal(At(C1, JFK) ∧ At(C2, SFO))
```
- Problem 2 initial state and goal:
```
Init(At(C1, SFO) ∧ At(C2, JFK) ∧ At(C3, ATL) 
	∧ At(P1, SFO) ∧ At(P2, JFK) ∧ At(P3, ATL) 
	∧ Cargo(C1) ∧ Cargo(C2) ∧ Cargo(C3)
	∧ Plane(P1) ∧ Plane(P2) ∧ Plane(P3)
	∧ Airport(JFK) ∧ Airport(SFO) ∧ Airport(ATL))
Goal(At(C1, JFK) ∧ At(C2, SFO) ∧ At(C3, SFO))
```
- Problem 3 initial state and goal:
```
Init(At(C1, SFO) ∧ At(C2, JFK) ∧ At(C3, ATL) ∧ At(C4, ORD) 
	∧ At(P1, SFO) ∧ At(P2, JFK) 
	∧ Cargo(C1) ∧ Cargo(C2) ∧ Cargo(C3) ∧ Cargo(C4)
	∧ Plane(P1) ∧ Plane(P2)
	∧ Airport(JFK) ∧ Airport(SFO) ∧ Airport(ATL) ∧ Airport(ORD))
Goal(At(C1, JFK) ∧ At(C3, JFK) ∧ At(C2, SFO) ∧ At(C4, SFO))
```

#### Implemented methods and functions in `my_air_cargo_problems.py`

#### Experimented and documented metrics for non-heuristic planning solution searches
* Ran uninformed planning searches for `air_cargo_p1`, `air_cargo_p2`, and `air_cargo_p3`; metrics tracked include number of node expansions required, number of goal tests, time elapsed, and optimality of solution for each search algorithm, including breadth-first, depth-first, and uniform cost search.
* The `run_search` script is used for data collection


### Part 2 - Domain-independent heuristics

- *Planning Graph*

#### Implemented heuristic methods in `my_air_cargo_problems.py`

#### Implemented a Planning Graph with automatic heuristics in `my_planning_graph.py`

#### Experimented and documented metrics of A* searches with these heuristics
* Ran A* planning searches using the heuristics implemented on `air_cargo_p1`, `air_cargo_p2` and `air_cargo_p3`. Metrics tracked include number of node expansions required, number of goal tests, time elapsed, and optimality of solution for each search algorithm.

>#### Why a Planning Graph?
>The planning graph is somewhat complex, but is useful in planning because it is a polynomial-size approximation of the exponential tree that represents all possible paths. The planning graph can be used to provide automated admissible heuristics for any domain.
