Download Link: https://assignmentchef.com/product/solved-cs201-homework-2-skiplists-and-hash-tables
<br>
<h1>Hash Tables</h1>

Figure 1: A sample game state in Conway’s Game of Life. From <a href="http://pi.math.cornell.edu/~lipa/mec/lesson6.html">Chaos and Fractals: Conway’s Game of</a>

<a href="http://pi.math.cornell.edu/~lipa/mec/lesson6.html">Life.</a>

In this assignment, we will implement 2 different hash tables which differ in their conflict resolution strategy. We will use the hash table to implement Conway’s Game of Life.

Game of Life

<a href="https://en.wikipedia.org/wiki/Conway's_Game_of_Life">Conway’s Game of Life</a> is a simple simulation with surprisingly complex behavior. We start with a simple 2D grid of cells. Each cell can be either alive or dead. The rules are:

<ul>

 <li>A live cell stays alive if it has two or three live neighbors.</li>

 <li>A dead cell becomes alive if it has exactly three live neighbors.</li>

</ul>

We start with a certain set of cell states and then iterate, applying the rules to every cell at each iteration. Despite their simplicity, these rules can produce amazingly complicated behavior.

— <a href="https://www.refsmmat.com/posts/2016-01-25-conway-game-of-life.html">A flexible implementation of Conway’s Game of Life</a>

The rules above are presented differently from their original formulation but they are nonetheless correct. This formulation is presented because it is more amenable to our eventual implementation.

<h3>     1.1      Initial Configurations</h3>

The game begins with an initial configuration of live cells. As the rules of the game are deterministic, the initial configuration completely determines all subsequent states of the game. Some initial configurations lead to interesting behavior and have led to the identification of certain classes of patterns.

<strong>Still Life </strong>These patterns are not affected by further iterations of the game and stay unchanged as the game proceeds.

<strong>Oscillators </strong>These patterns recur after a fixed number of iterations which are called the <em>period </em>of the oscillator.

<strong>Spaceships </strong>These are oscillators that change position or <em>glide </em>across the grid.

Figure 2: Evolution of the game from some initial states. From <a href="http://pi.math.cornell.edu/~lipa/mec/lesson6.html">Chaos and Fractals: Conway’s Game of Life.</a>

<h3>     1.2     Computation</h3>

It’s possible even, to create patterns which emulate logic gates (and, not, or, etc.) and counters. Building up from these, it was proved that the Game of Life is <a href="https://simple.wikipedia.org/wiki/Turing_complete">Turing Complete,</a> which means that with a suitable initial pattern, one can do any computation that can be done on any computer. Later, Paul Rendell actually constructed a simple Turing Machine as a proof of concept, which can be found <a href="https://www.ics.uci.edu/~welling/teaching/271fall09/Turing-Machine-Life.pdf">here.</a>

— <a href="http://pi.math.cornell.edu/~lipa/mec/lesson6.html">Chaos and Fractals: Conway’s Game of Life</a>

Some links in the above excerpt that are now dead have been updated.

<h3>     1.3     Visualization</h3>

As the Game of Life is a dynamic system, i.e. its stage changes with each iteration, it is best viewed as an animation which this document is unable to present. See the <a href="https://en.wikipedia.org/wiki/Conway's_Game_of_Life">Wikipedia page</a> or any of the other pages linked in this document for helpful animations. Here is a <a href="https://www.youtube.com/watch?v=C2vgICfQawE">YouTube video.</a>

<h2>     2       Implementation Details</h2>

An implementation of Conway’s Game of Life is provided in the classes Life and Game in the accompanying file game.py. The code is in the accompanying file and in the Appendix in this document. Life takes its initial configuration on creation and relies on 2 structures.

<strong>Live Cells </strong>A hash table containing (<em>x,y</em>) coordinates of live cells.

<strong>Neighbor Count </strong>A hash table containing key-value pairs. Each key is an (<em>x,y</em>) coordinate of a cell with live neighbors and the value is the number of its live neighbors.

In each iteration, the live cells are used to populate neighbor count which in turn is used to update the live cells.

Do not modify the implementation of this class.

Game runs a Life instance according to provided configurations with an option for animation. In the animation system used, the origin, (0<em>,</em>0), is at the top left of the window. This class is provided for your testing. You may modify it as per your needs.

<h2>     3      Task</h2>

Your task is to implement the structures in Life in 2 different ways.

<strong>Chaining </strong>The hash tables use chaining for conflict resolution.

<strong>Linear Probing </strong>The hash tables use linear probing for conflict resolution.

The hash table to use is indicated through a parameter passed to Life at the time of initialization.

<strong>Part II</strong>

<h1>Skiplists</h1>

The solutions to the following problems are to be entered inline below. Remove all other parts and sections from this document. Enter your team name for the date in the document’s title.

<h2>1. Redundant Comparisons</h2>

<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> The find(x) method in a SkiplistSet sometimes performs redundant comparisons; these occur when x is compared to the same value more than once. They can occur when, for some node, u, u.next[r] = u.next[r-1].

<ul>

 <li>What causes these redundant comparisons to happen?</li>

</ul>

<strong>Solution:</strong>

<ul>

 <li>Modify find(x) so that redundant comparisons are avoided.</li>

</ul>

<strong>Solution:</strong>

<h2>2. A Ranked Set</h2>

<a href="#_ftn2" name="_ftnref2"><sup>[2]</sup></a> Design, i.e. provide the necessary pseudo code for, a version of a skiplist that implements the SSet interface, but also allows fast access to elements by <em>rank</em>. That is, it also supports the function get(i), which returns the element whose rank is i in <em>O</em>(log<em>n</em>) expected time. (The rank of an element x in an SSet is the number of elements in the SSet that are less than x.)

<strong>Solution:</strong>

<h2>3. Finger Search</h2>

<a href="#_ftn3" name="_ftnref3"><sup>[3]</sup></a> A <em>finger </em>in a skiplist is an array that stores the sequence of nodes on a search path at which the search path goes down. (The variable stack in the add(x) code on page 87 is a finger; the shaded nodes in Figure 4.3 show the contents of the finger.) One can think of a finger as pointing out the path to a node in the lowest list, <em>L</em><sub>0</sub>.

A <em>finger search </em>implements the find(x) operation using a finger, walking up the list using the finger until reaching a node u such that u.x &lt; x and u.next = nil or u.next.x &gt; x and then performing a normal search for x starting from u. It is possible to prove that the expected number of steps required for a finger search is <em>O</em>(1 + log<em>r</em>), where <em>r </em>is the number values in <em>L</em><sub>0 </sub>between x and the value pointed to by the finger.

Design, i.e. provide the necessary pseudo code for, a version of a skiplist that implements find(x) operations using an internal finger. This subclass stores a finger, which is then used so that every find(x) operation is implemented as a finger search. During each find(x) operation the finger is updated so that each find(x) operation uses, as a starting point, a finger that points to the result of the previous find(x) operation.

<strong>Solution:</strong>

<h2>4. BONUS: Text Search</h2>

<a href="#_ftn4" name="_ftnref4"><sup>[4]</sup></a> Using an SSet as your underlying structure, design <em>and implement </em>an application that reads a (large) text file and allows you to search, interactively, for any substring contained in the text. As the user types their query, a matching part of the text (if any) should appear as a result.

<strong>Hint 1 </strong>Every substring is a prefix of some suffix, so it suffices to store all suffixes of the text file.

<strong>Hint 2 </strong>Any suffix can be represented compactly as a single integer indicating where the suffix begins in the text.

Test your application on some large texts, such as some of the books available at <a href="https://www.gutenberg.org/">Project Gutenberg. </a>If done correctly, your application will be very responsive; there should be no noticeable lag between typing keystrokes and seeing the results.

Submit your solution as textsearch.py. It is your responsibility to design and implement the necessary interface. Your program should remotely fetch the text to operate on, e.g using the urllib module from Homework 1. Any special instructions regarding running and using the program should be indicated clearly in the file.

<strong>Part III</strong>

<h1>Closing</h1>

<h2>Credits</h2>

The Game of Life homework is adapted from <a href="https://www.refsmmat.com/posts/2016-01-25-conway-game-of-life.html">A flexible implementation of Conway’s Game of Life</a> due to <a href="https://www.facebook.com/abdullah.zafar.547389">Abdullah Zafar</a> who identified it and adapted the implementation from <a href="https://racket-lang.org/">Racket.</a>

<h3>A Life</h3>

The listing below js based on line numbers from the accompanying file, game.py. Modifying the file will change the listing.

<table width="633">

 <tbody>

  <tr>

   <td width="633">for i in self.t:if len(i) != 0:yield idef clear(self): self.randomInt = random.randrange(1, 101, 2) self.w = 1 self.d = 0 self.q = 0 self.t = [()] * 2**self.wdef resize(self): self.w = int(math.log2(3*self.d)) self.w += 1 t = self.t self.t = [()] * 2**self.w self.q = self.d for coord in t:if coord != “” and coord != ():hashIndex = self.hashFunction( self.randomInt, coord[0], self.w)while self.t[hashIndex] != (): hashIndex = (hashIndex + 1) % 2**self.w self.t[hashIndex] = coordclass LinearSet:def __init__(self, state):self.randomInt = random.randrange(1, 101, 2) self.w = 1 self.d = 0 self.q = 0 self.t = [None] * 2**self.w for i in state: self.add(i)def hashFunction(self, randomInt, coord, d):return ((randomInt*hash(coord)) % 2**(32)) &gt;&gt; (32 – d)def add(self, coord):if self.find(coord) != None: return Falseif 2 * (self.q + 1) &gt; 2**self.w:self.resize()hashIndex = self.hashFunction(self.randomInt, coord, self.w) while self.t[hashIndex] != None and self.t[hashIndex] != “”:hashIndex = (hashIndex + 1) % 2**self.wif self.t[hashIndex] == None:</td>

  </tr>

 </tbody>

</table>




<table width="633">

 <tbody>

  <tr>

   <td width="59"> </td>

   <td width="573">self.q += 1self.d += 1 self.t[hashIndex] = coord return True</td>

  </tr>

  <tr>

   <td width="59">def</td>

   <td width="573">find(self, coord):hashIndex = self.hashFunction(self.randomInt, coord, self.w) while self.t[hashIndex] != None:if self.t[hashIndex] != “” and coord == self.t[hashIndex]:return self.t[hashIndex] hashIndex = (hashIndex + 1) % 2**self.w</td>

  </tr>

  <tr>

   <td width="59">def</td>

   <td width="573">discard(self, coord):hashIndex = self.hashFunction(self.randomInt, coord, self.w) while self.t[hashIndex] != None: y = self.t[hashIndex] if y != “” and coord == y: self.t[hashIndex] = “” self.d -= 1 if 8 * self.d &lt; 2**self.w:self.resize()return yhashIndex = (hashIndex + 1) % 2**self.wreturn None</td>

  </tr>

 </tbody>

</table>

<h3>B Game</h3>

The listing below js based on line numbers from the accompanying file, game.py. Modifying the file will change the listing.

<table width="633">

 <tbody>

  <tr>

   <td width="633">if i != None and i != “”: yield idef resize(self): self.w = int(math.log2(3*self.d)) self.w += 1 t = self.t self.t = [None] * 2**self.w self.q = self.d for coord in t:if coord != “” and coord != None:hashIndex = self.hashFunction( self.randomInt, coord, self.w)while self.t[hashIndex] != None:hashIndex = (hashIndex + 1) % 2**self.w self.t[hashIndex] = coord“””A Set implementation that uses hashing with chaining”””class ChainedSet():def __init__(self, state, iterable=[]): self.d = 1 self.t = self._alloc_table((1 &lt;&lt; self.d)) self.z = self._random_odd_int() self.n = 0 for i in state: self.add(i)def _random_odd_int(self): return random.randrange(1 &lt;&lt; w) | 1 def _alloc_table(self, s):</td>

  </tr>

 </tbody>

</table>




<table width="633">

 <tbody>

  <tr>

   <td width="59"> </td>

   <td width="573">return [[] for _ in range(s)]</td>

  </tr>

  <tr>

   <td width="59">def</td>

   <td width="573">_resize(self): temp = copy.copy(self.t) self.t = [] self.q = self.n if self.n &gt; 0:self.size = int(math.log2(3*self.n)) if self.size &lt; 2:</td>

  </tr>

 </tbody>

</table>




<a href="#_ftnref1" name="_ftn1">[1]</a> Adapted from Exercise 4.8 from the textbook.

<a href="#_ftnref2" name="_ftn2">[2]</a> Adapted from Exercise 4.9 from the textbook.

<a href="#_ftnref3" name="_ftn3">[3]</a> Adapted from Exercise 4.10 from the textbook.

<a href="#_ftnref4" name="_ftn4">[4]</a> Adapted from Exercise 4.14 from the textbook.