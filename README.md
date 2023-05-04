Download Link: https://assignmentchef.com/product/solved-cs526-final-project-assignment
<br>
The goal of this assignment is to give students an opportunity to design and implement two heuristic algorithms to find a shortest path in a graph. You need to read the problem description carefully, design algorithms, select appropriate data structures, and write a program to implement the algorithms.

<h1><u>Problem Description</u></h1>

Your program reads two input files – (1) <em>graph_input.txt</em> and (2) <em>direct_distance.txt</em>.

The first input file contains structural information about the input graph. Your program must read the graph input file and store the information in an appropriate data structure. You can use any data structure to store the input graph.




The <em>graph_input.txt</em> file contains a textual representation of a graph. The following example illustrates the input file format.




Consider the following graph. Each node has a name (an uppercase letter in a circle) and each edge is associated with a number. The number associated with an edge, which is called <em>weight</em> of the edge, represents the distance between the two vertices that are connected by the edge. We assume that all distances are positive integers.










The graph is represented in the input file as follows:




<h1>  H    I    L    M    N    Z H 0 146 138 0    0 0 I 146 0    97   0    0    0 L 138 97   0 0    0    101 M      0    0    0    0    0    90 N      0    0    0    0    0    85 Z 0    0 101 90   85   0</h1>




This representation of a graph is called <em>adjacency matrix</em>. In the input file, the vertex names (uppercase letters) and integers are separated by one or more spaces. Le <em>n</em> be the number of vertices in a graph. There are <em>n</em> + 1 columns and <em>n</em> + 1 rows in the input file. The top row and the first column show the names of vertices. The main part of the input file is an <em>n</em> x <em>n</em> two-dimensional array (or matrix) of integers. The meaning of a non-zero integer at the intersection of row <em>i</em> and column <em>j</em> is that there is an edge connecting the vertex corresponding to row <em>i</em> and the vertex corresponding to column <em>j</em>, and the integer is the distance between the two vertices. For example, the “138” at the intersection of the first row and the third column in the matrix means there is an edge between the vertex <em>H</em> and the vertex <em>L</em> and the distance is 138. The entry 0 means that there is no edge connecting two corresponding vertices. For example, the “0” in the sixth row and the first column in the matrix means that there is no edge between the two vertices <em>Z</em> and <em>H</em>. <em> </em>




Suppose that a network of cities is represented by a weighted, undirected graph as shown below. Each node in the graph represents a city, the edge between two nodes represents a road connecting the two cities, and the weight of an edge represents the distance between the two cities on the connecting road.










The second input file, named <em>direct_distance.txt</em>, has the <em>direct distance</em> from each node to the destination node <em>Z</em>. The direct distance from a node <em>n </em>to node <em>Z</em> is the distance measured along an <em>imaginary straight line</em> (or geographically straight line) from node <em>n</em> to node <em>Z</em> and is not necessarily the same as the sum of the weights of the edges connecting <em>n</em> to <em>Z</em>.




The second input file, corresponding to the above input graph, contains:




<ul>

 <li>380</li>

 <li>374</li>

 <li>366</li>

 <li>329</li>

 <li>244</li>

 <li>241</li>

 <li>242</li>

 <li>160</li>

 <li>193</li>

 <li>253</li>

 <li>176</li>

 <li>100</li>

 <li>77</li>

 <li>80</li>

 <li>161</li>

 <li>151</li>

 <li>199</li>

 <li>226</li>

 <li>234</li>

 <li>92</li>

</ul>

Z 0




You are required to implement two heuristic algorithms that are described below. Both algorithms try to find a shortest path from a given input node to node Z using heuristic approaches. In a shortest path, a node may appear at most once (i.e., a node cannot appear twice or more in a path).




Note that these two heuristic algorithms do not always find a correct shortest path.




Both algorithms start with the given input node and iteratively determine the next node in a shortest path. In determining which node to choose as the next node, they use different heuristics.




Let <em>w</em>(<em>n</em>, <em>v</em>) be the weight of the edge between node <em>n</em> and node <em>v</em>. Let <em>dd</em>(<em>v</em>) be the <em>direct distance</em> from <em>v</em> to the destination node Z.




When choosing the next node from a current node <em>n</em>:




Algorithm 1: Among all nodes <em>v</em> that are adjacent to the node <em>n</em>, choose the one with the smallest <em>dd</em>(<em>v</em>).




Algorithm 2: Among all nodes <em>v</em> that are adjacent to the node <em>n</em>, choose the one for which <em>w</em>(<em>n</em>, <em>v</em>) + <em>dd</em>(<em>v</em>) is the smallest.




<h2><strong>Example 1</strong>: Start node is J</h2>




Algorithm 1:




Current node = J

Adjacent nodes: A, C, I, K

A: <em>dd</em>(A) = 380

B: <em>dd</em>(C) = 366,  I: <em>dd</em>(I) = 193  K: <em>dd</em>(K) = 176.

K is selected

Shortest path: J → K




Current node = K

Adjacency node: J, Z J is already in the path Z is the destination node. Stop.

Shortest path = J → K → Z

Shortest path length = 99 + 211 = 310




Algorithm 2:




Current node = J

Adjacent nodes: A, C, I, K

A: <em>w</em>(J, A) + <em>dd</em>(A) = 151 + 380 = 531

C: <em>w</em>(J, C) + <em>dd</em>(C) = 140 + 366 = 506 I: <em>w</em>(J, I) + <em>dd</em>(I) = 80 + 193 = 273 K: <em>w</em>(J, K) + <em>dd</em>(K) = 99 + 176 = 275 I is selected.

Shortest path: J → I




Current node = I

Adjacent nodes: J, H, L

Node J is already in the path H: <em>w</em>(I, H) + <em>dd</em>(H) = 146 + 160 = 306 L: <em>w</em>(I, L) + <em>dd</em>(L) = 97 + 100 = 197

L is selected

Shortest path: J → I → L




Current node = L

Adjacent node: H, I, Z

H: <em>w</em>(L, H) + <em>dd</em>(H) = 138 + 160 = 298

I is already in the path

Z: <em>w</em>(L, Z) + <em>dd</em>(Z) = 101 + 0 = 101

Z is selected

Z is the destination. Stop.




Shortest path: J → I → L → Z

Shortest path length = 80 + 97 + 101 = 278




<h2><strong>Example 2</strong>: Start node is G</h2>




Algorithm 1:




Current node = G

Adjacent nodes: F, H

F: <em>dd</em>(F) = 241

H: <em>dd</em>(H) = 160

H is selected

Shortest path: G → H




Current node = H

Adjacent nodes: G, I, L, T

G is already in the path

I: <em>dd</em>(I) = 193

L: <em>dd</em>(L) = 100

T: <em>dd</em>(T) = 92

T is selected

Shortest path: G → H → T




Current node = T

Adjacent node: H H is already in the path.

<strong>Dead end</strong>.

<strong>Backtrack to H: G → H → T → H </strong>Node L is selected

Shortest path = G → H → L




Current node = L

Adjacent nodes: H, I, Z

H is already in the path I: <em>dd</em>(I) = 193 Z: <em>dd</em>(Z) = 0 Z is selected

Z is the destination. Stop.

Shortest path: G → H → L → Z

Shortest path length = 120 + 138 + 101 = 359




Algorithm 2




Current node = G

Adjacent nodes: F, H

F: <em>w</em>(G, F) + <em>dd</em>(F) = 75 + 241 = 316

H: <em>w</em>(G, H) + <em>dd</em>(H) = 120 + 160 = 280

H is selected

Shortest path: G → H




Current node = H

Adjacent nodes: G, I, L, T

G is already in the path

I: <em>w</em>(H, I) + <em>dd</em>(I) = 146 + 193 = 339

L: <em>w</em>(H, L) + <em>dd</em>(L) = 138 + 100 = 238

T: <em>w</em>(H, T) + <em>dd</em>(T) = 115 + 92 = 207

T is selected

Shortest path: G → H → T




Current node = T

Adjacent node: H H is already in the path <strong>Dead end</strong>.

<strong>Backtrack to H: G → H → T → H </strong>

L is selected.

Shortest path = G → H → L




Current node = L

Adjacent nodes: H, I, Z

H is already in the path

I: <em>w</em>(L, I) + <em>dd</em>(I) = 97 + 193 = 290 Z: <em>w</em>(L, Z) + <em>dd</em>(Z) = 101 + 0 = 101 Z is selected.

Z is the destination. Stop.

Shortest path: Shortest path = G → H → L → Z

Shortest path length = 120 + 138 + 101 = 359




Note that the above examples are just illustration. You need to design your own algorithms and develop pseudoceds based on the above description and the examples.




We assume the followings:




<ul>

 <li>The number of nodes in an input graph is 26 or smaller (Your program must be able to handle a graph with up to 26 nodes).</li>

 <li>Each node is represented by a single uppercase letter.</li>

 <li>The destination node is Z.</li>

 <li>The destination node Z is reachable from all other nodes.  All distances (edge weights) are positive integers.</li>

</ul>










<h2>Specific Requirements</h2>




<ol>

 <li>Implement both algorithms in one program. Your program may include multiple files.</li>

 <li>Your program must prompt the user to enter the start node. Your program must check the validity of the user-entered start node and, if the input is invalid, your program must prompt the user to enter an input again.</li>

 <li>Then, your program must find a shortest path from the input node to node Z using each algorithm and print the output on the screen.</li>

 <li>Your output must include the following three components for each algorithm: (1) The sequence of all nodes that were initially included in a shortest path. This sequence must include any backtrackings (see the example below), (2) The final shortest path found by the algorithm, (3) Shortest path length.</li>

</ol>




Output Example:




<ul>

 <li>User enters node J as the start node</li>

</ul>




Algorithm 1:




Sequence of all nodes: J -&gt; K -&gt;  Z

Shortest path: J -&gt; K -&gt;  Z

Shortest path length: 310




Algorithm 2:




Sequence of all nodes: J -&gt; I -&gt; L -&gt; Z

Path: J -&gt; I -&gt; L -&gt; Z

Length: 278




<ul>

 <li>User enters node G as the start node</li>

</ul>




Algorithm 1:




Sequence of all nodes: G -&gt; H -&gt; T -&gt; H -&gt; L -&gt; Z

Shortest path: G -&gt; H -&gt; L -&gt; Z

Shortest path length: 359




Algorithm 2:




Sequence of all nodes: G -&gt; H -&gt; T -&gt; H -&gt; L -&gt; Z

Shortest path: G -&gt; H -&gt; L -&gt; Z

Shortest path length: 359







Note:

<ul>

 <li>These two algorithm do not always find a correct shortest path.</li>

 <li>You can use the given graph to test your program. When your facilitator grades your program, they will use a different graph which may have a different number of nodes.</li>

 <li>You must hardcode input file names in your program at a conspicuous location so that your facilitator may be able to find and change them easily. In your documentation, you must clearly state in which part of your program input file names are hardcoded.</li>

</ul>





