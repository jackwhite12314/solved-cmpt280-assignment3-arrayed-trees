Download Link: https://assignmentchef.com/product/solved-cmpt280-assignment3-arrayed-trees
<br>
<h2>1.1    Arrayed Trees</h2>

Question 1 is about a bounded binary tree implementation. You should remember binary trees from CMPT 145 (or similar course) – they are trees in which each node has at most two children. What you probably didn’t know is that binary trees can be stored using an array, rather than a linked structure. In such an array, the contents of the root node are stored in offset 1 of the array (offset 0 is unused). The contents of the children of the node whose contents are stored at offset <em>i </em>are stored at offset 2<em>i </em>and 2<em>i </em>+ 1, respectively. Thus, the left child of the root is at offset 2 × 1 = 2, the right child of the root is at offset 2 × 1 + 1 = 3, the left child of the left child of the root is at offset 2 × 2 = 4, and so on. The parent of the node whose contents are at offset <em>i</em>, is at offset <em>i</em>/2 (integer division). Thus, the parent of node at offset 7 is at offset 3.

<strong>Example 1</strong>

<em>Here is the array representation of a tree storing the elements 1 through 10, in no particular order. The array</em>

<table width="259">

 <tbody>

  <tr>

   <td width="21">–</td>

   <td width="23">7</td>

   <td width="23">1</td>

   <td width="23">4</td>

   <td width="23">3</td>

   <td width="23">9</td>

   <td width="30">10</td>

   <td width="23">2</td>

   <td width="23">8</td>

   <td width="23">5</td>

   <td width="23">6</td>

  </tr>

 </tbody>

</table>

<em>is a representation of the tree:</em>

Note that we do not allow any unused entries in the array between used ones. All the data items in the array are stored contiguously. This means that we can represent only a particular subset of binary trees with this representation. Namely, it is the set of trees where all levels except possibly the last level are complete (full) and the nodes in the bottom level are all as far to the left as possible. You might be thinking that this is too restrictive and not very useful because we can’t represent <strong>all </strong>binary trees with this data structure. However, as we will see on future assignments, this array-based tree data structure is highly useful and efficient as a basis for implementing certain other important data structures.

Also note that if we read off the items from left to right in each level of the tree, starting from the top level, we get the items in the same order as they appear in the array.

<h2>1.2     <em>m</em>-ary Trees</h2>

An <em>m</em>-ary tree is one in which a node may have up to <em>m </em>children. Your lib280-asn3 library has a class called BasicMAryTree280&lt;I&gt; which implements an <em>m</em>-ary tree. It has some similarities with LinkedSimpleTree280&lt;I&gt; in that, like LinkedSimpleTree280&lt;I&gt;, you have to build up larger trees from smaller trees, rather than inserting individual elements, because since <em>m</em>-ary trees have no defined structure in general and thus there is no obvious algorithm for automatically deciding where a new element should go. You will use this class in Question 2. More details and some examples on how to use this class are/were provided in Tutorial 3.

<h1>2      Your Tasks</h1>

<strong>Question 1:</strong>

Your task is to write a Java class called ArrayedBinaryTreeWithCursors280&lt;I&gt; which extends and implements the abstract class ArrayedBinaryTree280<em>&lt;</em>I<em>&gt; </em>(provided in the lib280-asn3.tree package as part of lib280-asn3). This week’s lab will also talk more about array-based trees.

<strong>Methods to be Implemented</strong>

Some of the work of implementing ArrayedBinaryTreeWithCursors280&lt;I&gt; has already been done, but there is more to do.

Firstly, there are several methods in ArrayedBinaryTreeWithCursors280&lt;I&gt; which are defined but not implemented. You must implement these methods. These methods can be easily identified by their “TODO” comments.

Secondly, since ArrayedBinaryTreeWithCursors280&lt;I&gt; implements some other interfaces, there are several methods required by these interfaces that also need to be implemented but have not yet been finished. The method headers for these methods have already been generated but the method bodies are empty. The definitions of these methods in their respective interfaces document what these methods are supposed to do. These methods can be identified by their “TODO” commands as well as the @Override directive above the method headers. Many of these methods are defined by LinearIterator280, which is inherited through Dict280&lt;I&gt;. These are the same linear iterator methods that you wrote for LinkedList280&lt;I&gt; on assignment 1. The rest of these methods are defined by Cursor280&lt;I&gt;.

There is already a regression test included in ArrayedBinaryTreeWithCursors280&lt;I&gt;. Your completed implementation of the arrayed binary tree must pass the given regression test. If all the regression tests are successful, the only output should be: Regression test complete.

<strong>You may not modify any of the existing code in the provided </strong>ArrayedBinaryTreeWithCursors280.java <strong>file </strong>(including the regression test) but you can add to it. <strong>You may also not modify any other files within </strong>lib280-asn3.

<strong>Implementation Hints</strong>

<ul>

 <li>You don’t need to declare an array instance variable in ArrayedBinaryTreeWithCursors280&lt;I&gt; to hold the data items. There is already one inherited from ArrayedBinaryTree280&lt;I&gt;. You should look at the other inherited instance variables too!</li>

 <li>One of your first tasks will be to start implementing the insert method and decide where the new element should be inserted. If you think about it, there’s really only one place it can go…</li>

 <li>The algorithm for deleting an element is to replace the element to be deleted by the right-most element in the bottom level of the tree, then delete the right-most element in the bottom level of the tree.</li>

 <li>Not sure how a linear iterator works on a tree? If you think about it, there is only one reasonable way to define a linear ordering on the elements of an array-based binary tree.</li>

 <li>Reminder: the items array (defined in the abstract class ArrayedBinaryTree280<em>&lt;</em>I<em>&gt; </em>) represents the nodes of the tree. You are storing the <strong>contents </strong>of nodes in the array. There is no node class. It is very important that the contents of the root are stored in offset 1 and we don’t use offset 0 of the array, otherwise the given formulae for finding the child or parent of a node at offset <em>i </em>will not work correctly.</li>

</ul>

<strong>Question 2 :</strong>

In video games, especially those in the roleplaying genre, it is common that characters in the game are advanced in power through the use of a <em>skill tree</em>. Generally, a skill tree defines the prerequisite for the various skills that your character in the game might acquire. For example, in a hypothetical game, if the <em>Shield Bash</em>, <em>Defensive Stance</em>, and <em>Shield Ally </em>skills all require that your character first have the skill <em>Shield Proficiency</em>, then this might be represented by the following skill tree:

More formally, a skill in the skill tree can only be gained if the character first gains all of the skills which are ancestors of that skill in the tree.<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a>

Your task in this question is to write a class called SkillTree which extends BasicMAryTree280&lt;Skill&gt; (an <em>m</em>-ary tree of Skill objects; a complete Skill.java is provided). A template for the SkillTree class is provided. It contains a constructor and a couple of useful methods. You will add additional methods to this class in the following steps, which you should complete in order:

<ul>

 <li>Write a main() method in the SkillTree class in which you construct your own skill tree for your own hypothetical video game. Your tree must contain at least 10 skills. However, for the sanity of everyone involved, try to keep it under 15 skills. Be creative! There is no reason why any two students should hand in exactly the same (or even very similar) skill trees, nor should you just duplicate the skill tree shown in the sample output. Print your tree to the console using the toStringByLevel() method inherited from BasicMAryTree280.</li>

 <li>Write a method in the SkillTree class called skillDependencies which takes a skill name as input and returns an instance of LinkedList280&lt;Skill&gt; which contains all the of the skills which are prerequisites for obtaining the input skill (including the input skill itself!). A RuntimeException exception should be thrown if the tree does not contain the given skill. A good implementation approach for this method is to use a recursive traversal of the tree to find the named skill, and then add skills to the output list as the recursion unwinds. Tutorial 3 includes some discussion of recursive traversal of <em>m</em>-ary trees. Add to your main() program a few tests of this method, and print out the lists that is returned (you can use the list’s toString() method for this). Be sure to test the case where the named skill does not exist in the tree.</li>

 <li>Write a method in the SkillTree class called skillTotalCost which takes a skill name as input and returns the total number of skill points that a player must invest to obtain the given skill. If the named skill is not in the skill tree, then the skillTotalCost method should throw a RuntimeException exception. <em>Hint: this method is quite easy to implement if you make use of the previously implemented </em>skillDependencies</li>

</ul>

For example, in the above skill tree, if a character wants the <em>Shield Ally </em>skill they would need to spend 1 skill point to get <em>Shield Proficiency</em>, and then spend 3 skill points to get <em>Shield Ally </em>for an overall investment of 1 + 3 = 4 points, so for the above tree, skillTotalCost(“Shield Ally”) should return 4. Note that the Skill object contains the cost of the skill.

Add to your main() program a few tests of skillTotalCost, and print out the total costs returned. Be sure to test the case where the named skill does not exist in the tree.

<ul>

 <li>Run your main() program. Cut and paste the console output to a text file and submit it with your assignment. See the sample output on the next page.</li>

</ul>

<h2>2.1     Sample Output</h2>

Here is an example of what the output of your program might look like. Remember, you are expected to be creative in designing your skill tree, and your submission should not attempt to duplicate what you see here aside from the general formatting (the formatting can be the same, but the data should be different!). Note that the formatting of output of the skill tree contents is done by the toStringByLevel() method of BasicMAryTree280.

<table width="601">

 <tbody>

  <tr>

   <td width="601">My Skill Tree:1: Slash, Cost: 12: Mighty Blow, Cost: 22: Shield Bash, Cost: 13: Shield Charge, Cost: 23: Parry, Cost: 24: Shield Wall, Cost: 44: –4: –4: –3: –3: –2: Cleave, Cost: 23: Whirlwind, Cost: 34: Berzerk, Cost: 54: –4: –4: –3: –3: –3: –2: Mobility, Cost: 1Dependencies for Shield Wall:Slash, Cost: 1, Shield Bash, Cost: 1, Parry, Cost: 2, Shield Wall, Cost: 4, Dependencies for Mobility: Slash, Cost: 1, Mobility, Cost: 1, Dependencies for Slash:Slash, Cost: 1,Dependencies for FakeSkill:FakeSkill not found.To get Whirlwind you must invest 6 points.To get Mighty Blow you must invest 3 points.To get Slash you must invest 1 points.FakeSkill not found.</td>

  </tr>

 </tbody>

</table>

<h1>3      Files Provided</h1>

<strong>lib280-asn3: </strong>A copy of lib280 which includes the ArrayedBinaryTree280 class needed for Question 1, a partially complete ArrayedBinaryTreeWithCursors280 for Question 1, and the BasicMAryTree280 class which is needed for Question 2.

<strong>Skill.java </strong>: A complete implementation of the Skill class needed for Question 2.

<strong>SkillTree.java </strong>: A template for your implementation of the SkillTree class in Question 2

<a href="#_ftnref1" name="_ftn1">[1]</a> In the video game world, the term “skill tree” sometimes refers to things that actually aren’t trees; a noteworthy example is the skill tree in the ARPG <a href="https://www.pathofexile.com/passive-skill-tree">Path Of Exile</a><a href="https://www.pathofexile.com/passive-skill-tree">,</a> which, if you click the link, can see is clearly <strong>not </strong>a tree, even though they call it that. <strong>Here in question 2, we used the term “skill trees” to mean skill trees that are, in fact, actual trees.</strong>