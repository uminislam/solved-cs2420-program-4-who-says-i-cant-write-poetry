Download Link: https://assignmentchef.com/product/solved-cs2420-program-4-who-says-i-cant-write-poetry
<br>
<strong>Part 1: Becoming familiar with the code</strong>

HashTable code has been given to you.  No testing program has been provided.  To become familiar with how the code works, try reading in a small input file and make sure you can create a hash table of those entries.

<strong>Testing:</strong> Make sure the following works:

<ol>

 <li>Insert values</li>

 <li>Delete values</li>

 <li>Find values</li>

 <li>Printing the contents of the hash table.</li>

 <li>Control the size of the hash table.</li>

</ol>

What happens if you attempt to delete an item that isn’t there?

What if you add more things than can fit into the hash table?

<strong>Modification: </strong>You have been given the hash table code from your text for doing quadratic probing.  Modify the code so it takes the key and the associated object as two separate parameters.

Please retain the generic structure of the hash table.  Be careful not to add anything to the hash table that only makes sense for this specific problem.

Part 1 is for your benefit.  The code you turn in does not need to show the results of this experimentation.




Part 2 <strong>Using the code to solve a bigger problem</strong>

This assignment is designed to give you experience with hash tables.  In this assignment, you will randomly create a new verse of poetry (based on the pattern seen in the existing poem).

You will fit a bi-word language model to English and then use it to generate a poem.  A uni-word model of English consists of a single probability distribution <strong><em>P</em></strong><em>(W)</em> over the set of all words.

A bi-word model of English consists of two probability distributions: <strong><em>P</em></strong><em>(W)</em> and <strong><em>P</em></strong><em>(W<sub>i+1</sub> | W<sub>i</sub>)</em>. The first distribution is just the probability a word in a document. The second distribution is the probability of seeing word <em>W<sub>i+1</sub></em> given that the previous word was <em>W<sub>i</sub></em>.

Given a set of documents (in our case, various poems), your job in this assignment is to generate a poem from a given word.  The method is simple. You just need to decide which word should follow a given word.  The word selected is based on the probability in which it occurs (in the file) after the last word used.  So for example, in the text below, if I ask, “What should follow ‘sam’”?, you pick ‘I’ most of the time  (7 out of 8 times) and ‘sam’ the rest of the time.  No other word follows ‘sam’.

I am Sam. I am Sam. Sam I Am.

That Sam I Am! That Sam I Am! I do not like that Sam I Am!

Do you like green eggs and ham?

I do not like them, Sam I Am.

I do not like green eggs and ham.

Would you like them here or there?

I would not like them here or there.

I would not like them anywhere.

I do not like green eggs and ham.

I do not like them, Sam I Am.

Thus you need to keep track of the number of times that each word follows every other word  (so you can figure probabilities).

Keep track of all words (and their probabilities) using a hash table in which you hash on word W.   For the input above, partial contents of the hash table are shown below.  Thus, “do” occurs 6 times in the file.  Five times “do” is followed by “not” and one time it is followed by “you”

Similarly, for the input file, when you see the word “sam”, seven times out of 8 “i” is the next word.  One time out of 8, “sam” is the next work.

Given the information in this data structure, we can compute the conditional probability that “i” occurs once you are looking at word “sam” <em>P(i|sam)</em> as 7/8. Similarly, we can compute the probability <em>P(ham|and)</em> as 3/3 = 1.  When I ask what should follow “sam”, you will pick the next word given the probabilities seen.  In other words,  87.5% of the time you will want ‘i’ to come next (after sam).

Given a specific input file,  you are to generate a poem of a given length from a specific starting word.  So for example, poem(“sam”, 20) is to generate a poem of 20 words that begins with the word sam.    Your poem might look like: “sam I am sam I am I am I would not like them here or there I am do not like” or “sam I would you like green eggs and ham I am do you like them sam I am I am I”

<strong>Specifics</strong>

For the data, remove all special characters and punctuation and change everything to lower case.

<strong>Output</strong>

There are several data files associated with the test.    You will generate poems from the following specification:

<table>

 <tbody>

  <tr>

   <td width="186"><strong>File</strong></td>

   <td width="189"><strong>Beginning word</strong></td>

   <td width="181"><strong>Length of Poem</strong></td>

   <td width="163"><strong>Print Hash Table?</strong></td>

  </tr>

  <tr>

   <td width="186">green.txt</td>

   <td width="189">sam</td>

   <td width="181">20</td>

   <td width="163">Yes</td>

  </tr>

  <tr>

   <td width="186">test.txt</td>

   <td width="189">that</td>

   <td width="181">20</td>

   <td width="163">Yes</td>

  </tr>

  <tr>

   <td width="186">clown.txt</td>

   <td width="189">go</td>

   <td width="181">20</td>

   <td width="163">Yes</td>

  </tr>

  <tr>

   <td width="186">inch.txt</td>

   <td width="189">computer</td>

   <td width="181">50</td>

   <td width="163">no</td>

  </tr>

  <tr>

   <td width="186">Poe.txt</td>

   <td width="189">nevermore</td>

   <td width="181">50</td>

   <td width="163">no</td>

  </tr>

  <tr>

   <td width="186">Seuss.txt</td>

   <td width="189">mordecai</td>

   <td width="181">50</td>

   <td width="163">no</td>

  </tr>

 </tbody>

</table>

For grading purposes, you are asked to print the contents of the hash table for some of the test cases. This will be a huge benefit to you in debugging.   Because the next word is generated via a random number generator,  you should not expect your output to match that of others.

<strong>Hints</strong>

In order to generate which word follows word WORD with the correct probability, I used the following strategy.  I kept track of how many times WORD occurred (call it occurCt) and how many times each word followed WORD (followCt).   I generated a random number between 0 and occurCt.  Then I considered each word which followed WORD in order.  I added up the followCts of each following word until the sum of the followCts passed the random number.  When the sum passed the random number, that is the word I selected to be the next word in the poem.




<strong>What to Turn In</strong>

Turn in your complete project file. In a readMe file, please write a one-paragraph analysis of the generated texts addressing the following points:

<ul>

 <li>What knowledge do human beings have that is NOT captured by this language model and that therefore causes the model to generate nonsense. Write down at least three facts that, if the computer could somehow know them, would allow it to generate more sensible language.</li>

 <li>Compare the different poems. If your experience is like mine, some will be more coherent than others. Speculate about why this is true.</li>

</ul>


