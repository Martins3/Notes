# Program Analysis via Graph Reachability
> Thomas Reps

This paper presents a program-analysis framework based on a somewhat different principle: Analysis
problems are posed as graph-reachability problems. As will be discussed below, we express (or convert)
program-analysis problems to context-free-language reachability problems (“CFL-reachability problems”),
which are a generalization of ordinary graph-reachability problems.
CFL-reachability is defined in Section 2.
- Interprocedural program slicing  
- Interprocedural versions of a large class of dataflow-analysis problems  
- A method for approximating the possible “shapes” that heap-allocated structures can take on  
- Flow-insensitive points-to analysis.

The application of CFL-reachability to shape analysis
applies to both functional and imperative languages that permit the use of heap-allocated storage, but do
not *permit destructive updating of fields*.

There are a number of benefits to be gained from using graph reachability as a vantage point for studying
program-analysis problems: 
- By expressing a program-analysis problem as a graph-reachability problem, we can obtain an efficient
algorithm for solving the program-analysis problem. In a case where the program-analysis problem is
expressed as a *single-source ordinary graph-reachability problem*, the problem can be solved in time
linear in the number of nodes and edges in the graph; in a case where the program-analysis problem is
expressed as a *CFL-reachability problem*, the problem can be solved in time cubic in the number of
nodes in the graph.

- The difference in asymptotic running time needed to solve ordinary reachability problems and
CFL-reachability problems provides insight into possible trade-offs between accuracy and running time for
certain program-analysis problems: Because a CFL-reachability problem can be solved in an
approximate fashion by treating it as an ordinary reachability problem, this provides an automatic way to obtain
an approximate (but safe) solution, via a method that is asymptotically faster than the method for obtaining the more accurate solution.  
> CFL 和 single source 之间装换

- In program optimization, most of the gains are obtained from making improvements at a program’s “hot
spots”, such as the innermost loops, which means that dataflow information is really only needed for
selected locations in the program. Similarly, software-engineering tools that use dataflow analysis often
require information only at a certain set of program points (in response to user queries, for example).
This suggests that applications that use dataflow analysis could be made more efficient by using a
*demand dataflow-analysis algorithm*, which determines whether a given dataflow fact holds at a given
point [11,102,78,30,49,88]. For program-analysis problems that can be expressed as CFL-reachability
problems, demand algorithms are easily obtained by solving single-source, single-target, multi-source, or
multi-target CFL-reachability problems [49]
> 热点 => demand algorithm  => CFL

- Graph reachability offers insight into the “O (n^3) bottleneck” that exists for certain kinds of program analysis problems.
> 提供理论上的洞察力 关于 ...

- The graph-reachability approach provides insight into the prospects for creating parallel programanalysis algorithms. T
> 提供理论上的洞察力 关于并行算法

The remainder of the paper is organized into six sections, as follows:
- Section 2 defines CFL-reachability.
- Section 3 discusses algorithms for solving CFL-reachability problems.
- Section 4 discusses how the graph reachability approach can be used to tackle interprocedural dataflow analysis, interprocedural program slicing, shape analysis, and flow-insensitive points-to analysis.
- Section 5 concerns demand versions of program-analysis problems.
- Section 6 describes some techniques that go beyond pure graph reachability.
- Section 7 discusses related work.

## 2. Context-Free-Language Reachability Proble
A CFL-reachability problem is not an ordinary reachability
problem (e.g., transitive closure), but one in which a path is considered to *connect two nodes only if the
concatenation of the labels on the edges of the path is a word* in a particular context-free language:
> is a word ? label  edge ?
> 
## 3. Algorithms for Solving CFL-Reachability Proble
> 问题可以被解决，但是问题到底是什么，并不清楚。


## 4. Four Example

#### 4.1. Interprocedural Dataflow Analysis
One way to solve an IFDS problem is to convert it into a realizable-path reachability problem

A function’s representation relation captures the function’s semantics in the sense that the representation
relation can be used to evaluate the function.




## 问题
1. 所以为什么需要强调是 context-free ?
2. 
