Download Link: https://assignmentchef.com/product/solved-stats507-homework-3-files-and-objects
<br>
<h1>1         Counting Word Bigrams</h1>

In your previous homework, you wrote a function for counting character bigrams. Now, let’s write a function for counting word bigrams. That is, for each pair of words, say, cat and dog, we want to count how many times the word “cat” occurred immediately before the word “dog”. We will represent this bigram by a tuple, (’cat’, ’dog’). For our purposes, we will ignore all spaces, newlines, punctuation and capitalization in our counting. So, as an example, the fragment of poem,

Half a league, half a league,

Half a league onward,

All in the valley of Death Rode the six hundred.

includes the bigrams (’half’, ’a’) and (’a’, ’league’) both three times, the bigram (’league’, ’half’) appears twice,while the bigram (’in’, ’the’) appears only once.

<ol>

 <li>Write a function count_bigrams_in_file that takes a filename as its only argument. Your function should read from the given file, and return a dictionary whose keys are bigrams (given in the tuple form above), and values are the counts for those bigrams. Again, your function should ignore punctuation, spaces, newlines and capitalization. The strings in your key tuples should be lower-case. Your function should use a try-catch statement to raise an error with an appropriate message to alert the user in the event that the given file cannot be opened, and a different error in the event that the provided argument isn’t a string at all. <strong>Hint: </strong>you will find the Python function strip(), along with the string constants defined in the string documentation (<a href="https://docs.python.org/3/library/string.html">https://docs.python.org/3/library/string.html</a><a href="https://docs.python.org/3/library/string.html">)</a>, useful in removing punctuation. <strong>Hint: </strong>be careful to check that your function handles newlines correctly. For example, in the poem above, one of the (’league’, ’half’) bigrams spans a newline, but should be counted nonetheless. <strong>Note: </strong>be careful that your function does not accidentally count the empty string as a word (this is a common bug if you aren’t careful about splitting the input text). Solutions that merely delete “bad” keys from the dictionary at the end will not receive full credit, as all edge cases can handled by correctly splitting the input.</li>

 <li>Download the file txt from the course webpage: This is an ASCII copy of all of Tolstoi’s novel <em>War and Peace</em>. Run your function on this file, and pickle the resulting dictionary in a file called mb.bigrams.pickle. Please include this file in your submission, along with WandP.txt, so that we can run your notebook directly from your submission.</li>

 <li>We say that word <em>A </em>is <em>collocated </em>with word <em>B </em>in a text if words <em>A </em>and <em>B </em>occur immediately one after another (in either order). That is, words <em>A </em>and <em>B </em>are collocated if and only if either of the tuples (A, B) or (B, A) are present in the text. Write a function collocations that takes a filename as its only argument and returns a dictionary. Your function should read from the given file (raising an appropriate error if the file cannot be opened or if the argument isn’t a string at all) and return a dictionary whose keys are all the strings appearing in the file (again ignoring case and stripping away all spaces, newlines and punctuation) and the value of word <em>A </em>is a Python set containing all the words collocated with <em>A</em>. Again using the poem fragment above</li>

</ol>

as an example, the string ’league’ should appear as a key, and should have as its value the set {’a’, ’half’, ’onward’}, while the string ’in’ should have the set {’all’, ’the’} as its value. <strong>Hint: </strong>we didn’t discuss Python sets in lecture, because they are essentially just dictionaries without values. See the documentation at <a href="https://docs.python.org/3/tutorial/datastructures.html#sets">https://docs.python.org/3/tutorial/datastructures.html#sets</a> for more information.

<ol start="4">

 <li>Run your function on the file txt and pickle the resulting dictionary in a file called mb.colloc.pickle. Please include this file in your submission.</li>

</ol>

<h1>2         More Fun with Vectors</h1>

In this exercise, we’ll encounter our old friend the vector yet again, this time taking an object-oriented approach.

<ol>

 <li>Define a class Vector. Every vector should have a dimension (a non-negative integer) and a list or tuple of its entries. The initializer for your class should take the dimension as its first argument and a list or tuple of numbers (ints or floats), representing the vector’s entries, as its second argument. Choose sensible default behavior for the case where the user applies only a dimension and no entries. The initializer should raise a sensible error in the case where the dimension is invalid (i.e., wrong type or a negative number), and should also raise an error in the event that the dimension and the number of supplied entries disagree.</li>

 <li>Did you choose to make the vector’s entries a tuple or a list (there is no wronganswer here, although I would say one is better than the other in this context)? Defend your choice.</li>

 <li>Are the dimension and entries class attributes or instance attributes? Why is thisthe right design choice?</li>

 <li>Implement the necessary operator(s) to support comparison (equality, less than, lessor equal to, greater than, etc) of Vector We will say that two Vector objects are equivalent if they have the same coordinates. Otherwise, comparison should be analogous to tuples in Python, so that comparison is done on the first coordinate first, then the second coordinate, then the third, and so on. So, for example, the two-dimensional vector (2<em>,</em>4) is ordered before (less than) (2<em>,</em>5). Attempting to compare two vectors of different dimensions should result in an error.</li>

 <li>Implement a method dot that takes a single Vector as its argument and returns the inner product of the caller with the given Vector object. Your method should raise an appropriate error in the event that the argument is not of the correct type or in the event that the dimensions of the two vectors do not agree.</li>

 <li>We would also like our Vector class to support scalar multiplication. Left- or rightmultiplication by a scalar, e.g., 2*v or v*2, where v is a Vector object, should result in a new Vector object with its entries all scaled by the given scalar. We will also follow R and numpy (which you will learn in a few weeks), and use * to denote entrywise vector-vector multiplication, so that for Vector objects v and w, v*w results in a new Vector object, with the <em>i</em>-th entry of v*w equal to the <em>i</em>-th entry of v multiplied by the <em>i</em>-th entry of w. Implement the appropriate operators to support this multiplication operation. Many languages have a convention for dealing with multiplication of vectors that differ in their dimension, but we will punt on this matter. Your method should raise an appropriate error in the event that v and w disagree in their dimensions.</li>

 <li>For a real number 0 ≤ <em>p </em>≤ ∞, and a vector <em>v </em>∈ R<em><sup>d</sup></em>, the <em>p</em>-norm of <em>v</em>, written k<em>v</em>k<em><sub>p</sub></em>, is given by if <em>p </em>= 0  if 0 <em>&lt; p &lt; </em>∞<em>, .</em></li>

</ol>

max<em>i</em>=1<em>,</em>2<em>,…,d </em>|<em>v</em><em>i</em>|        if <em>p </em>= ∞

Strictly speaking, this is only a norm for <em>p </em>≥ 1, but that’s beside the point. Implement a method Vector.norm that takes a single int or float p as an argument and returns the p-norm of the calling Vector object. Your method should work whether p is an integer or float. Your method should raise a sensible error in the event that <em>p </em>is negative. <strong>Hint: </strong>see <a href="https://docs.python.org/3/library/functions.html#float">https://docs.python.org/3/library/functions.html# </a><a href="https://docs.python.org/3/library/functions.html#float">float</a> for documentation on representing positive infinity in Python.