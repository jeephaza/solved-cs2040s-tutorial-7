Download Link: https://assignmentchef.com/product/solved-cs2040s-tutorial-7
<br>
<h2>Problem 1.            Quadratic Probing</h2>

Quadratic probing is another open-addressing scheme very similar to linear probing. Recall that a linear probing implementation searches the next bucket on a collision.

We can also express linear probing with the following pseudocode (on insertion of element <em>x</em>):

for i in 0..m:

if buckets[hash(x) + i % m] is empty:

insert x into this bucket break

Quadratic probing follows a very similar idea. We can express it as follows:

for i in 0..m:

// increment by squares instead if buckets[hash(x) + i * i % m] is empty:

insert x into this bucket break

<ul>

 <li>Consider a hash table with size 7 with hash function h(x) = x % 7. We insert the following elements in the order given: 5, 12, 19, 26, 2. What does the final hash table look like?</li>

 <li>Continuing from the above question, we now delete the following elements in the order given: 12, 5. What does the final hash table look like?</li>

 <li>Can you construct a case where quadratic probing fails to insert an element despite the table not being full?</li>

</ul>

<h2>Problem 2.           Table Resizing</h2>

Suppose we follow these rules for an implementation of an open-addressing hash table, where <em>n </em>is the number of items in the hash table and <em>m </em>is the size of the hash table.

<ul>

 <li>If <em>n </em>= <em>m</em>, then the table is <em>doubled </em>(resize <em>m </em>to 2<em>m</em>)</li>

 <li>If <em>n &lt; m/</em>4, then the table is <em>shrunk </em>(resize <em>m </em>to <em>m/</em>2)</li>

</ul>

What is the minimum number of insertions between 2 resize events? What about deletions?

<h2>Problem 3.           Necessary Evils</h2>

We discussed that when using a Bloom filter, we can choose which elements to place in order to tolerate false positives or false negative. For example, we would rather tolerate false negatives for displaying online friends (i.e., having an online person appearing as offline rather than an offline person appearing as online) – and as such we would put the set of offline friends into our bloom filter. How would you use a Bloom filter in the following situations?

<ul>

 <li>New article filter – you want to use a Bloom filter so only unread articles are shown to users.</li>

 <li>Search engines – you want to use Bloom filters to help users look for relevant documents based on search terms</li>

 <li>IP filter – you want to use a Bloom filter to prevent attackers on your web server (e.g. to prevent DDoS)</li>

</ul>

<h2>Problem 4.             Implementing Union/Intersection of Sets</h2>

Consider the following implementations of sets. How would intersect and union be implemented for each of them?

<ul>

 <li>Hash table with open addressing</li>

 <li>Hash table with chaining</li>

 <li>Fingerprint hash table/Bloom filters</li>

</ul>

<h2>Problem 5.            Removing Fingerprints</h2>

In this question, we will implement a delete function for our Bloom Filter/Fingerprint Hash Table (FHT).

<ul>

 <li>One way is by keeping count of items which hash to each fingerprint. How would you use this to implement the delete function? What are the tradeoffs and potential issues with this implementation?</li>

 <li>Another way is by using another FHT to keep track of deleted entries. How would you implement this? What are some issues with this implementation?</li>

</ul>

<h1>1         Scapegoat Trees</h1>

<strong>Problem 6. </strong>Consider the Scapegoat Tree data structure that we have implemented in Problem Sets 4-5. We assume that only insertions are performed on our Scapegoat Tree. In this question, we will use amortized analysis to reason about the performance of inserts on Scapegoat Trees.

<ul>

 <li>Suppose we are about to perform the rebuild operation on a node <em>v</em>. Show that the amount of entries that <em>must </em>have been inserted into node <em>v </em>since it was <strong>last rebuilt </strong>is Ω(<em>size</em>(<em>v</em>)).</li>

 <li>Show that the <em>depth </em>of any insertion is <em>O</em>(log<em>n</em>)</li>

 <li>Now use the previous two parts to show that the amortized cost of an insertion in a Scapegoat Tree is <em>O</em>(log<em>n</em>). <em>Hint: </em>Suppose an a constant amount is ”deposited” at every node traversed on an insertion.</li>

</ul>

<h1>2         Hashing</h1>

<strong>Problem 7.</strong>

<h2>(Tabulation Hashing.)</h2>

Suppose we are creating a hash function keys <em>N </em>= log<em>n </em>bits long, mapped to buckets indexed by <em>M </em>= log<em>m</em>. So, the hash function maps an <em>N </em>bit key to an <em>M </em>bit identifier for a bucket. To do this, we construct a 2D-array <em>T</em>[2<em>,N</em>] and fill each entry in the table with a random <em>M </em>bit value. Now to hash a key, we just XOR the key and the table:

hash = 0 for (j = 1 to N) hash = hash XOR T[key[j], j]

<strong>Problem 7.a. </strong>Show that for a given key <em>k </em>and bucket <em>b</em>, Pr[<em>h</em>(<em>k</em>) = <em>b</em>] = 1<em>/m</em>, and that for two keys <em>k</em><sub>1 </sub>6= <em>k</em><sub>2</sub>, Pr[<em>h</em>(<em>k</em>1) = <em>h</em>(<em>k</em>2)] ≤ 1<em>/m</em>

<strong>Problem 7.b.           </strong>How much space does this table require?

Now let’s generalize the function. Choose some integer <em>R </em>that divides <em>N</em>. (In the previous example, <em>R </em>= 1.) Now generate a 2d table of size [2<em><sup>R</sup>,N/R</em>]. As before, fill each entry with a random M bit value. As before, take the hash by breaking the key into R bit chunks, look up each chunk in the table, and perform XOR:

hash = 0 for (j = 1 to N/R) hash = hash XOR T[key[(j-1)R .. jR]][j]

Notice now the table needs one entry for each of the 2<em><sup>R </sup></em>possible chunks of the key.

<strong>Problem 7.c.           </strong>What is the size of the table?

<strong>Problem 7.d.           </strong><em>Bonus </em>Here’s another simple hashing scheme:

Construct a 2D binary array <em>A</em>[<em>M,N</em>], where each entry is a random 0 or 1. For key <em>k</em>, let <em>h </em>= <em>Ak </em>(think of it as matrix multiplication, where <em>k </em>is a column vector, <em>A </em>is a matrix, and the result is an <em>m</em>-bit column vector).

Is this the same as tabulation hashing?