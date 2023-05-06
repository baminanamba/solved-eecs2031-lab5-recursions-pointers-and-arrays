Download Link: https://assignmentchef.com/product/solved-eecs2031-lab5-recursions-pointers-and-arrays
<br>
This lab focuses mainly on pointers. Following the recent and near future lectures on pointers, this lab contains four major parts:  Part I: Pointers and passing address of scalar variables. Part II:

Pointer arithmetic. Part III: Pointers and passing char arrays (strings) to functions; Part IV:

Pointers and passing general arrays to functions.

Before delving into pointers, let’s start with exercises on rand() library function and simple recursions, which we covered recently. We also look at system() library function as an preparation of the Unix materials that will be covered soon in class.

<strong>0 system() library function </strong>

Download file lab5randSys.c, compile and run it.  Observe that,

<ul>

 <li>the program calls function rand() to generate random numbers. Randomization is a fundamental technique in algorithm design. Function rand(), declared in &lt;stdlib.h&gt;, returns a random integer in the range 0 to RAND_MAX every time it is called.</li>

</ul>

RAND_MAX is a constant whose default value may vary between implementations but it is granted to be at least 32767. On machines using the GNU C library RAND_MAX is equal to INT_MAX.

<ul>

 <li>to generate a random number in a certain range, e.g., [1, 6] to represent dice rolls, a typical approach is to use modules operation and then shift by adding the lower bound. Try to understand the mathematic trick.</li>

 <li>note that rand() is a <strong>pseudorandom number generator</strong>: the sequence of values it returns is predictable. Run the program several times and you will notice the same sequence of random number.</li>

 <li>if you want to get different sequences, you need to <strong>seed</strong> the random number generator using srand(). A typical use might be: strand(time(0)). Here time(0) returns the number of seconds since the epoch (00:00:00 UTC, January 1, 1970, for POSIX systems). As you observed above, If random numbers are generated with rand() without first calling srand(), your program will create the same sequence of numbers each time it runs. Now uncomment the first line, compile and run the program again for several times, and you will observe different sequence of numbers. (Note that this still might give repeated values if you run it fast – e.g., twice in the same second).  Explore other approaches if you are interested.  Also explore how to generate random number in Java.</li>

</ul>




Next, uncomment the commented block in the second half of the program.

The code block calls a standard library function system(), whose prototype is                        int system(char *command)  as given in stdlib.h. Taking as input a string command, which is a valid Unix command,  system() executes  a  Unix shell command specified in command, much as if you enter the command in terminal.   Compile and run it. Observe that,  •        current location is displayed, with pwd command.

<ul>

 <li>the current directory is listed, and new directories xxxDir were created in the current directory, and the current directory is listed again.  These are performed using ls, mkdir</li>

</ul>




Issue commands ls -l in the terminal to verify that directory xxxDir was generated.

Remove the directory each time before you run the program again. (Can you do that in terminal using commands? Try issue command <strong>rmdir xxxDir</strong> but don’t spend too much time if you cannot make it. We will learn how to do this in terminal when we cover unix commands later in the course.) <strong>  </strong>

No submission for this question. <strong> lab3D0</strong>

<strong> </strong>

<ol>

 <li><strong> A Math Library functions, simple recursions (5pt) </strong></li>

</ol>

<strong>Specification </strong>

Write an ANSI-C program that reads input from the standard input, which contains one double and one integer representing a base <em>b</em> and exponent (i.e., power) <em>n</em>, and then calculates <em>b<sup>n</sup></em>.   After reading base and exponent from the user, the program first calls the math library function pow(), and then call function my_pow(), which is a <strong>recursive</strong> function that you are going to implement here.

The program keeps on prompting user and terminates when user enters -1000 for base

(followed by any number for exponent).

<strong> </strong>

<strong>Implementation </strong>

Download file lab5pow.c and start from there.   Note that to read a double using scanf, we need to use %lf.  (%f is use for float).

<ul>

 <li>Your function my_pow(double, double) should be RECURSIVE, not ITERATIVE. That is, the function should be implemented using RECURSION, not loops. In a recursive solution, the function calls itself with different (usually smaller) inputs, until the input becomes small enough so that we can solve the case directly. This case is called a <em>base case</em>.</li>

 <li>Note that although the function’s parameters are of type double, the actual argument for exponent is assumed to be an integer literal (i.e. the power will not be 3.5). However, the power can be negative. Your functions should handle this.</li>

</ul>

<strong> </strong>

<strong>Sample Inputs/Outputs  </strong> <strong> </strong>red 117% a.out

<h1>Enter base and power: <strong>10 2 </strong></h1>

pow:    100.0000 my_pow: 100.0000




Enter base and power: <strong>10 4</strong> pow:    10000.0000 my_pow: 10000.0000




Enter base and power: <strong>2 3</strong> pow:    8.0000 my_pow: 8.0000




Enter base and power: <strong>2.3 5</strong> pow:    64.3634 my_pow: 64.3634




<h1>Enter base and power: <strong>-2 4 </strong></h1>

pow:    16.0000 my_pow: 16.0000




<h1>Enter base and power: <strong>-2.75 5</strong></h1>

pow:    -157.2764 my_pow: -157.2764




Enter base and power: <strong>2 -3</strong> pow:    0.1250 my_pow: 0.1250




Enter base and power: <strong>2 -5</strong> pow:    0.0312 my_pow: 0.0312




Enter base and power: <strong>2.7 -3</strong> pow:    0.0508 my_pow: 0.0508




Enter base and power: <strong>-2 -6</strong> pow:    0.0156 my_pow: 0.0156




Enter base and power: <strong>-2.75 -3</strong> pow:    -0.0481 my_pow: -0.0481




Enter base and power: <strong>-1000 4</strong>

<h1>red 118%</h1>

Submit your program using    <strong>submit 2031A lab5 lab5pow.c</strong><strong>   </strong>

<strong> </strong>

<strong>Part I</strong><sub>  </sub><strong>Pointers and passing address of scalar variables 1. Problem A  (5pt) </strong>

<strong>Subject       </strong>

Experiencing “modifying scalar arguments by passing addresses/pointers”.

<strong> </strong>

<strong>Specification </strong>

Write an ANSI-C program that reads three integers line by line, and modify the input values.




<strong>Implementation    </strong>Download file lab5swap.c to start off.

<ul>

 <li>The program reads user inputs from stdin line by line. Each line of input contains 3 integers separated by blanks. A line that has the first number being -1 indicates the end of input.</li>

 <li>Store the 3 input integers into variable a, b and c;</li>

 <li>Function swapIncre() is called in main() with an aim to change the values of a, b and c in such a way that, after function swapIncre returns, b’s value is doubled, a stores c’s original value incremented by 100, and c stores the original value of a. As an example, suppose a is 1, b is 2 and c is 3, then after function returns, a has value 103, b has value 4 and c has value 1.</li>

 <li>Compile and run the program and observe unsurprisingly that the values of a, b and c are not changed at all (why?).</li>

 <li>Modify the program so that it works correctly, as shown in the sample inputs/outputs below. You should only modify function swapIncre and the statement in main that calls this function.</li>

</ul>

No global variables should be used.

<strong>Sample Inputs/Outputs: </strong>

red 309 % <strong>a.out</strong>

<ul>

 <li><strong>8 9 </strong></li>

</ul>

Original inputs:   a:4     b:8     c:9

Rearranged inputs: a:109   b:16    c:4




<ul>

 <li><strong>12 7 </strong></li>

</ul>

Original inputs:   a:5     b:12    c:7

Rearranged inputs: a:107   b:24    c:5

<strong> </strong>

<strong>12 20 -3 </strong>

Original inputs:   a:12    b:20    c:-3

Rearranged inputs: a:97    b:40    c:12

<strong> </strong>

<strong>12 -3 30 </strong>

Original inputs:   a:12    b:-3    c:30

Rearranged inputs: a:130   b:-6    c:12

<strong> -1 2 3</strong>

red 309 % <strong>cat inputA.txt</strong>

3 5 6

2 67 -1

-12 45 66

66 55 1404

22 3 412

-2 44 6 -1 55 605

red 310 % <strong>a.out &lt; inputA.txt</strong> Original inputs:   a:3     b:5     c:6

Rearranged inputs: a:106   b:10    c:3




Original inputs:   a:2     b:67    c:-1

Rearranged inputs: a:99    b:134   c:2




Original inputs:   a:-12   b:45    c:66

Rearranged inputs: a:166   b:90    c:-12




Original inputs:   a:66    b:55    c:1404

Rearranged inputs: a:1504  b:110   c:66




Original inputs:   a:22    b:3     c:412

Rearranged inputs: a:512   b:6     c:22




Original inputs:   a:-2    b:44    c:6

Rearranged inputs: a:106   b:88    c:-2

red 311%

Submit using  <strong> submit 2031A lab5 lab5swap.c</strong>

<strong> </strong>

<ol start="2">

 <li><strong>Problem A2 (10 pt) </strong></li>

</ol>

Modify program lab5swap.c, by defining a new function void swap(int *, int *) which swaps the values of a and c.  This function should be called in function swapIncre().

Specifically, swapIncre()only increases the value of parameters, and delegates the swapping task to swap().

You should not change the code of main, and the parameter list of swapIncre given in your lab5swap.c.

Again, no global variables should be used.

<strong> </strong>

<strong>Sample Inputs/Outputs: </strong>Same as above.




Name the new program lab5swap2.c and submit using  <strong>  </strong>

<strong>                         </strong><strong>submit 2031A lab5 lab5swap2.c </strong>

<ol start="3">

 <li><strong>Problem A3 (10pt) </strong></li>

</ol>

Modify the above program, by defining a new function void swap(int **, int **) which swaps the values of a and c.  This function should be called in function swapIncre().

Specifically, swapIncre()only increases the value of parameters, and delegates the swapping task to swap().

You should not change the code of main, and the parameter list of swapIncre given in your lab5swap.c. Again, no global variables should be used.

<strong> </strong>

<strong>Sample Inputs/Outputs: </strong>Same as above.




Name the new program lab5swap3.c and submit using  <strong>  </strong>

<strong>                         </strong><strong>submit 2031A lab5 lab5swap3.c</strong>

<strong> </strong>

<table width="64">

 <tbody>

  <tr>

   <td width="64"><em>fact </em>1</td>

  </tr>

 </tbody>

</table>

<strong>Part II</strong><sub>   </sub><strong>Pointer/address arithmetic </strong>

C supports some arithmetic operations on pointers. For expression p ± n, where p is a pointer and n is an integer, the result is another address (pointer).

Download program lab5pArithmetic.c and study the code. Then compile and run it several times. You will get different values each time, but you should always observe the following:

<ul>

 <li>For pChar which is a pointer to char, expression pChar+1 results in an address (pointer) whose value is the value of pchar plus 1. For pShort which is a pointer to short, expression pShort+1 results in an address whose value is the value of pShort plus 2. For integer pointer pInt,  expression pInt+1 results in an address whose value is the value of pInt plus 4. For Double pointer pDouble, expression pDouble+1 results in an address whose value is the value of pDouble plus Likewise, these pointers + 2 result in addresses whose values are the original values plus 2, 4, 8 and 16 respectively.  Why was C designed this way?</li>

 <li>As discussed in class, the rule here is that for a pointer p, arithmetic expression p ± n results in an address (pointer) whose value is the value of p ± n × s  where s is the size of the type of p’s pointee, in bytes. That is, the result is “scaled” by the size of the pointee type. Thus, for an integer pointer pInt, expression pInt + n results in an address whose value is the value of pInt + n×4, assuming size of int is 4 bytes. (Because of this, pointer arithmetic in C is sometimes colloquially termed “<strong>p+1 is p+4</strong>”.)</li>

 <li>This rule is further verified by the outputs for p++, which assign the pointers to resulting addresses, jumping the pointers by 1, 2, 4 and 8 bytes respectively, and the outputs for p += 4, which jump the pointers by 4×1, 4×2, 4×4 and 4×8 bytes respectively.</li>

</ul>

<strong> </strong>

<ul>

 <li>For an array arr, its elements are stored continuously in memory, with arr[0] occupying the lowest address. For an integer array like arr, each element occupies 4 bytes in memory. So the address of arr[i+1] is 4 bytes higher than the address of arr[i]. For a double array, as another example, address of arr[i+1] is 8 bytes higher than the address of arr[i].</li>

</ul>




<ul>

 <li>If we have a pointer ptr0 that points the first element of the array, i.e., ptr0=&amp;arr[0]¸ then according to the pointer arithmetic rule above (<em>fact 1</em>), ptr0+i results in an address of value ptr0+i×4, which, due to the fact that array elements are stored continuously in memory (<em>fact 2</em>), is the address of element i of arr. That is, if ptr0==&amp;arr[0], then ptr0+i == &amp;arr[i], which in turn implies that *(ptr0+i) == arr[i].</li>

</ul>




<ul>

 <li>Array name arr contains the address of its first element, that is, arr and &amp;arr[0] contain the same address. So array name can be treated as a pointer (to its first element). Following pointer arithmetic, arr+i results in an address of value arr+i×4, which is the address of element i of arr. That is, arr+i == &amp;arr[i], and  *(arr +i) == arr[i];</li>

 <li>Since array name arr is a pointer, assignment operation ptr = &amp;arr[0] can be rewritten as ptr = arr, which assigns ptr the address of the first element of the array, making ptr point to arr[0]. Consequently, ptr0, ptr, arr and &amp;arr[0] contain the same value. Hence, we have the rule that if ptr == arr (i.e., ptr points to arr[0]), then ptr+i == arr+i == &amp;arr[i], and *(ptr+i) == *(arr+i) == arr[i].</li>

</ul>

<table width="64">

 <tbody>

  <tr>

   <td width="64"><em>fact </em>2</td>

  </tr>

 </tbody>

</table>

<table width="64">

 <tbody>

  <tr>

   <td width="64"><em>fact </em>3</td>

  </tr>

 </tbody>

</table>

<table width="64">

 <tbody>

  <tr>

   <td width="64"><em>fact </em>4</td>

  </tr>

 </tbody>

</table>

<table width="64">

 <tbody>

  <tr>

   <td width="64"><em>fact </em>5</td>

  </tr>

 </tbody>

</table>




Based on the above observations, complete the program so that arr[i] can also be accessed in two other ways which involve pointer arithmetic, generating the following outputs

arr[i]          *(arr+i)      *(ptr0+i)         *(ptr+i) ==========================================================================

Element[0]:     -100            -100          -100              -100

Element[1]:     100             100           100               100

Element[2]:     200             200           200               200

Element[3]:     300             300           300               300

Element[4]:     400             400           400               400

Element[5]:     500             500           500               500

Element[6]:     600             600           600               600

Element[7]:     700             700           700               700

Element[8]:     800             800           800               800

Element[9]:     900             900           900               900




<ul>

 <li>observe how a pointer to pointer is declared, initialized, and dereferenced. Understand the results. For example, why the two (**pp)– statements result in different values?</li>

</ul>




<ul>

 <li>Finally, since array name can be used as a pointer, is there any difference between array name and other pointers such as <sub>ptr</sub>? Uncomment the last line and compile again. What did you get?  Observe that ptr and pp can be changed as they are pointer <u>variables</u>. Array name arr, on the other hand, is a pointer <u>constant</u> so cannot be changed.</li>

</ul>




Why does C have pointer arithmetic and why is the result scaled based on the type? Why array name contains the address of its first element?

It turns out that all the above rules were designed with an aim to facilitate <u>passing array to</u> <u>functions</u>, which is the subject of Part III and Part IV below.




No submission for this question.

<strong> </strong>

<strong>Part III</strong> <strong>Pointers and passing char arrays to functions </strong>

<strong>Motivation </strong>

In C when an array is passed as an argument to a function, it is ‘decayed’ into a single value which is the (starting) memory address of the array, contained in the array name that is passed to the function. That is, the function only receives a single address value, rather than the whole array —<strong> whether the pointee at this address is a single variable or it is the first element of an array, or something else, it is the same form of information that is passed to the function.</strong> Thus, a function that expects an integer array as argument can specify its parameter (formal argument) either as int[] or int *.   Likewise, a function that expects a char array (string) as argument can specify its parameter (formal argument) either as char[] or char *.  (See prototype of functions in string.h). In calling the function, you can pass as the actual argument either the array name (which contains the address of its first element), or a pointer to an element of the array.  Either way, <strong>passing array by address allows the invoked function to not only access the argument array but also modify it, even it is called-by-value</strong>.

<strong> </strong>

<strong>Problem C0   </strong>

Passing char array as argument, and pointer notation in place of array index notation [].




Download the program lab5strlen.c, which shows more than 10 ways to implement strlen(). Read the code and run it, and observe the following:

<ul>

 <li>Firstly, since the array name contains the address of the first element (fact 4), in addition to array name as we did so far, we can also pass the address &amp;arr[0] explicitly into this functions. If we have a pointer that points to the start of the string, then we can also pass the pointer to the functions.</li>

 <li>Functions expecting a char array can specify the parameter (formal argument) either as char [], or, char *.</li>

 <li>Functions expecting a char array can be called by passing either the array name or a pointer to an array element as its actual argument.</li>

 <li>Even a function’s formal argument is declared as char[], you can always use pointer notations to manipulate the argument in the function.</li>

 <li>Even a function’s formal argument is declared as char *, you can always use array notation [] to manipulate the argument in the function</li>

 <li>Address/pointer arithmetic can be exploited strategically to calculate the string length</li>

 <li>Because of ‘decaying’, sub-arrays can be passed to a function easily. Note the 3 ways to pass sub-arrays of msg.</li>

 <li>By passing sub-arrays, recursion can be exploited to solve the problem.</li>

 <li>Based on the fact that array elements are stored continuously in memory, and assuming the array is fully populated, the length of an array can be calculated using sizeof <strong>operator</strong>, with sizeof(arr)/sizeof(char) or sizeof(arr)/sizeof(arr[i]). o In case of char array, we subtract 1 to exclude the ‘ ’.</li>

</ul>

Note that this approach does not work when used on a pointer variable that points to the array: sizeof ptr gives the memory size of the pointer variable ptr itself, which is usually 8 bytes.  Note, sizeof is an operator, not a function.  (As shown later in this lab (lab5E0), in a function that receives a array argument,  using sizeof on parameter also does not work.)




No submission for this problem.

<strong> </strong>

<strong>4.1 Problem C  (20+10pt)</strong>

<strong>Subject   </strong>Passing char array as argument, <strong><u>accessing argument array</u></strong>. Pointer notion in place of array index notation.

<strong> </strong>

<strong>Specification </strong>

Write an ANSI-C program that reads inputs line by line, and determines whether each line of input forms a palindrome.  A palindrome is a word, phrase, or sequence that reads the same backward as forward, e.g., “madam”, “dad”.         The program terminates when quit is read in.

<strong> </strong>

<strong>Implementation </strong>

Download file lab5palin.c to start with.

<ul>

 <li>Assume that each line of input contains at most 30 characters but it may contain blanks.</li>

 <li>Use fgets to read line by line o note that the line that is read in using fgets will contain a new line character ‘
’, right before ‘ ’. Then you either need to exclude it when processing the array, or, remove the trailing new line character before processing the array. As discussed in class, one common approach for the latter is replacing the ‘
’ with ‘ ’.</li>

 <li>Define a function void printReverse (char *) which prints the argument array reversely.

  <ul>

   <li>Do not use array indexing [] throughout your implementation. Instead, use pointers and pointer arithmetic to manipulate the array.</li>

   <li>Do not create extra arrays. Manipulate the original array only.</li>

  </ul></li>

</ul>




<ul>

 <li>Define a function int isPalindrome (char *) which determines whether the argument array (string) is a palindrome.   <strong> </strong>o Do not use array indexing [] throughout your implementation. Instead, use pointers and pointer arithmetic to manipulate the array.</li>

</ul>

o Do not create extra arrays. Manipulate the original array only.

<ul>

 <li>Do not use global variables.</li>

</ul>

<strong> </strong>

<ul>

 <li>[<strong>Bonus</strong>] Define another function int isPalindromeR (char *) which determines whether the argument array (string) is a palindrome, using <strong>recursion</strong>.  <strong> </strong>

  <ul>

   <li>Do not use array indexing [] throughout your implementation. Instead, use pointers and pointer arithmetic to manipulate the array.</li>

   <li>Do not create extra arrays. Manipulate the original array only.</li>

   <li>isPalindromeR(char*) itself is not necessarily a recursive function. You may want to create a recursive helper function, which is called by isPalindromeR(char *).</li>

  </ul></li>

</ul>

Hint: the reason for a helper function is that the recursive function needs more argument than isPanlidromR(char*)

<strong> </strong>

<strong>Sample Inputs/Outputs: </strong>

red 339 % <strong>a.out hello </strong>olleh Not a palindrome

<strong>lisaxxasil </strong>lisaxxasil Is a palindrome.




<strong>that is a SI taht </strong>that IS a si taht Not a palindrome.




<strong>that is a si taht </strong>that is a si taht

Is a palindrome.

<strong> quit </strong>red 340 %

red 340 % <strong>a.out &lt; inputPalin.txt</strong>

olleh

Not a palindrome.

doogsisiht Not a palindrome.

dad

Is a palindrome.

daD

Not a palindrome.




LI Saxxas il Not a palindrome.




123454321 Is a palindrome.

madam

Is a palindrome.




qwerty uiopoiu ytrewq

Is a palindrome.

33

Is a palindrome.




A

Is a palindrome.

lisaxxtsil

Is a palindrome.

that si a si taht Not a palindrome.




that is a si taht

Is a palindrome.

abCdyfxDCBA

Not a palindrome.

abcdefedcba Is a palindrome.

red 342 %

Submit using   <strong>submit 2031A lab5 lab5palin.c</strong>

<strong> </strong>

<strong> </strong>

<strong>4.2 Problem D   (20pt)</strong>

<strong> </strong>

<strong>Subject  </strong>

Array name contains address. Thus when an array is passed to a function as argument, the function is able to not only access the array, but also <strong>modify argument array.</strong>  Pointer notion in place of array index notation.

<strong> </strong>

<strong>Specification </strong>

Complete program lab5sort.c, which reads inputs line by line, and then for each line, sorts it alphabetically, according to the indexes of the characters in ASCII table, in ascending order, using two approaches. That is, the letter that appears earlier in the ASCII table should appear earlier in the sorted array. The program terminates when quit is read in.

<strong> </strong>

<strong>Implementation </strong>

<ul>

 <li>Assume that each line of input contains at most 50 characters and may contain blanks.</li>

 <li>Use fgets to read line by line</li>

 <li>Define a function void sortArray (char *) which sorts characters in the argument array according to the index in the ASCII table.</li>

</ul>

o Don’t use extra arrays. The function should sort and modify the argument array directly.

<ul>

 <li>Define a function void sortArray2 (char *) which sorts characters in the argument array according to the index in the ASCII table, using another approach. o Do not use extra arrays. The function should sort and modify the argument array directly.</li>

 <li>Do not use array indexing [] throughout the program, except for array declarations in main.</li>

</ul>

Instead, use pointers and pointer arithmetic to manipulate arrays.

<ul>

 <li>Do not use global variables.</li>

 <li>People have been investigating sorting problems for centuries and there exist various sorting algorithms, so don’t try to invent a new one. Also, don’t call library function such as <em>qSort</em> to do the sorting. Instead, you can implement any one of the existing famous sorting algorithms, e.g., Bubble Sort, Insertion Sort, Selection Sort, Quick Sort, Merge Sort. (Compared against recursive algorithms such as Quick Sort, Merge Sort which has <em>O(nlgn)</em> complexity, the first three algorithms are simpler but slower – <em>O(n<sup>2</sup>) </em>complexity). Pseudo-</li>

</ul>

code for Bubble Sort and Selection Sort are given below for you. You can implement these algorithms or some others.  Don’t use [] in your implementation.

<strong> </strong>

<strong>BUBBLE-SORT(A)  </strong>

<ol>

 <li>n ← number of elements in A</li>

 <li>for i ← 0 to n-2 //   ≤ n-2</li>

 <li>for j ← n-1 to i+1 // right to left</li>

 <li>if A[j]  &lt;  A[j-1]</li>

 <li>swap A[j] &#x2194; A[ j – 1 ]</li>

</ol>

<strong> </strong>

<strong>SELECTION-SORT(A) </strong>

<ol>

 <li>n ← number of elements in A</li>

 <li>for i ← 0 to n-2 //   ≤ n-2</li>

 <li>smallest ← i // smallest: index of current smallest, initially i</li>

 <li>for j ← i + 1 to n-1</li>

 <li>if A[ j ] appears earlier than A[ smallest ] in ASCII table</li>

 <li>smallest ← j  // update smallest</li>

 <li>swap A[ i ] &#x2194; A[ smallest ]    // move smallest element to index i</li>

</ol>

<strong> </strong>

<strong>Sample Inputs/Outputs: </strong>

red 340 % <strong>a.out hello </strong>ehllo ehllo

<strong>7356890 </strong>

0356789

0356789




<strong>DBECHAGIF </strong>

ABCDEFGHI

ABCDEFGHI <strong> hello world  </strong>dehllloorw  dehllloorw<strong>  </strong>

<strong>2031ON 2021W </strong>

<strong> </strong>00112223NOW

00112223NOW

<strong> quit  </strong>

red 341 % <strong>a.out &lt; inputSort.txt </strong>

02eehortt

02eehortt




023456ERbbdggjnnos

023456ERbbdggjnnos

agghhrrtvy agghhrrtvy

024667uy

024667uy




000001112239ABCEF

000001112239ABCEF




0123456789opqrstuvwxy

0123456789opqrstuvwxy




abcdefghijklmnopqrstuvwxyz abcdefghijklmnopqrstuvwxyz

red 342 %

Submit your program with   <strong>submit 2031A lab5 lab5sort.c</strong>

<strong> </strong>

<strong>Part IV</strong> <strong>Pointers and passing <u>general</u> arrays to functions </strong>

In C when an array is passed into a function, it is ‘decayed’ into a single memory address. That is, the function only receives a single address value, rather than the whole array structure itself. Without a view of the whole structure, the function does not “know” if the pointee at this address is a single variable or it is the first element of an array. No array length information is passed to the function automatically, thus the caller should provide the function with the information about where the array ends. In the case of a character array (string), the special sentinel character ‘ ’ is used to mark the end of array. For other type of arrays such as int [], double [], however, the caller needs to provide the function with the length information explicitly. In this section you will explore different approaches to providing the length info of an argument array.




<strong>5.0. Problem E0  </strong>

<strong>Subject    </strong>

Exploiting array memory size. (Not working).

Some people think that the function does not necessarily need a terminator token or an extra argument of length information. The seemingly plausible trick is to use sizeof on parameter. As implemented in lab5E0.c,  one attempt is to get the array length by exploiting the memory size of the array. Specifically, assuming the array is fully populated, then the number of elements can be derived with operation sizeof(array)/sizeof(int).




Compile and run lab5E0.c. Observer that,

<ul>

 <li>For an array, both the functions receive the correct starting address of the argument array.</li>

 <li>sizeof(arrName)/sizeof(type) works in main.</li>

 <li>in both the functions, however, sizeof(formal argument) / sizeof(type) does not give the correct length of the actual argument array, even when the formal argument is declared as int [] or char[].</li>

</ul>




Think about why this happens.

Hint：1) array passed to a function is “decayed” to an address. Thus argument c, even if defined as int c[],  is converted to int *c by the compiler;  2) sizeof is an operator, not a function. (strlen is a function, so it works inside the function). 3) some compiler will give you warning message about this.

<strong>No submissions for this problem. </strong>

<strong> </strong>

<strong>5.1. Problem E. Using terminator token  (10pt) </strong>

<strong>Subject  </strong>

Explore putting a special sentinel token at the end of array, like the case of string.  Use scanf to detect end of file.

“<em>My data are in my lockers. I occupy several (consecutive) lockers, starting at locker #10, and the last locker contains a bunny teddy bear in it</em>” – so given starting locker number #10, the function knows that the locker with a bunny bear is the end.

<strong>  </strong>

<strong>Specification </strong>

Write an ANSI-C program that reads a list of <u>non-negative</u> integer values (including 0), until EOF is read in, and then outputs the largest value among in the input integers.

Assume there are no more than 20 integers.   All inputs are non-negative integer literals.




<strong>Implementation </strong>

Download lab5E.c to start with.

<ul>

 <li>Keep on reading integers using scanf and a loop, and put the integers into an array, until EOF is read.</li>

</ul>

In earlier labs we have experienced how getchar detects end of file (end of input file or Ctrl+D). We have used  scanf to read input and we have ignored the fact that scanf also has a return value, which is an integer indicating the number of characters read in, and, same as getchar, function scanf also returns EOF if end of file is reached.  You can issue  <strong>man 3 scanf | grep return</strong>  or  <strong>man 3 scanf | grep EOF</strong>          in the terminal to see details.

<ul>

 <li>Note that several input integers can appear on the same line. So far we have used scanf to read a line of input a time (which contains no spaces). Here you can observe that scanf with a loop can read inputs that appear on the same line, as well as on multiple lines.</li>

</ul>




<ul>

 <li>In main, index notation [] should only be used in declaring the array. For the rest of code in main, you should use pointer indirection and address arithmetic to access and update the array. No array index [] should be used.</li>

</ul>

<strong> </strong>

<ul>

 <li>Define a function void display(int *), which, given an integer array, prints the array elements. <strong> </strong></li>

</ul>

Note that this function takes just one argument, which is the starting address of array.  How could the caller let the function know where the end of the array is? (Hint: could the caller add a bunny bear in the array before passing the array to the function?)

In this function, use pointer indirection and address arithmetic to access and traverse the array. No array index [] should be used in the function.<strong>   </strong>

<ul>

 <li>Define a function int largest(int *), which, given an integer array, returns the largest integer in the array.</li>

</ul>

Note that this function also takes just one argument, which is the starting address of array.   In this function, use pointer indirection and address arithmetic to access and traverse the array. No array index [] should be used in the function.

<ul>

 <li>Do not use global variables.</li>

</ul>

<strong> </strong>

<strong>Sample Inputs/Outputs: </strong>

red 330 % <strong>a.out  </strong>

<strong>1 2 0 33  </strong>

<strong>445  </strong>

<strong>23  </strong>

<strong>^D </strong>

Inputs: 1 2 0 33 445 23

Largest value: 445

red 331 % <strong>a.out &lt; inputE.txt </strong>

Inputs: 7 5 3 6 9 18 33 44 5 12 9 0 34 534 128 78

Largest value: 534




Submit using   <strong>submit 2031A lab5 lab5E.c </strong>

<strong> </strong>

<strong>5.2   Problem E2  Length info as argument  (10 pt) </strong>

<strong>Subject </strong>

Passing length info explicitly.   Use scanf to detect end of file.

The above approach provides the length info about argument array by putting a special sentinel terminator token at the end of the array, like the case of string. This is possible because the inputs are assumed to be non-negative integer literals. But putting a terminator might not always be possible.

A more general approach, which is more common for general arrays, is to pass the length info explicitly to the function (as an additional argument).




“<em>My data are in my lockers. I occupy several (consecutive) lockers, starting at lock #10, and I occupy eight lockers</em>” – so given starting locker number #10, the function knows that locker #17 is the end.




<strong>Specification </strong>

Same problem and requirement as above, but this time suppose the input numbers can be both positive and negative (so we could not store a special terminator token in the array).

<strong> </strong>

<strong>Implementation </strong>

<ul>

 <li>Implement function int largest(int *, int) and void display(int *, int).</li>

</ul>

Same as before, no array index [] should be used in main, except the array declaration.  No array index [] should be used in largest and display at all.

<ul>

 <li>Do not use global variables.</li>

</ul>

<strong> </strong>

<strong> </strong>

<strong>Sample Inputs/Outputs: </strong>red 340 % <strong>a.out  </strong>

<strong>1 2 0 33  </strong>

<strong>-445  </strong>

<strong>23  </strong>

<strong>^D </strong>

Inputs: 1 2 0 33 -445 23

Largest value: 33

red 341 % <strong>a.out &lt; inputE2.txt </strong>

Inputs: 7 5 3 6 9 18 -33 44 5 -12 0 9 -34 534 128 78

Largest value: 534

<strong> </strong>

Name your program lab5E2.c, and submit using    <strong>submit 2031A lab5 lab5E2.c </strong>

<strong> </strong>

<strong>5.3   Problem E2-void   (10 pt) </strong>

Rewrite lab5E2.c such that function largest is void  and has one more parameters. That is,  void largest(int *, int, ?) where ? is a type that you decide. Call the function properly in main so it has the same input and output as problem E2. Note that function largest should not print anything. Generate output in main as before.




Name your program lab2E2void.c and submit using

<strong>submit 2031A lab5 lab5E2void.c </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong>In summary, for this lab you should submit the following files  </strong><strong>lab5pow.c  </strong>

<strong>lab5swap.c lab5swap2.c  lab5swap3.c lab5palin.c lab5sort.c  </strong>

<strong>lab5E.c lab5E2.c lab5E2void.c </strong>




You can issue <strong>submit -l 2031A lab5</strong> in the terminal, or go to  <a href="https://webapp.eecs.yorku.ca/submit">web submit</a> to view the list of files that you have submitted.

<strong> </strong>

<strong> </strong>

<strong>Common Notes </strong>

All submitted files should contain the following header:

/***************************************

<ul>

 <li>EECS2031A – Lab5 *</li>

 <li>Author: Last name, first name *</li>

 <li>Email: Your email address *</li>

 <li>eecs_num: Your eecs login username *</li>

 <li>Yorku #: Your York student number</li>

</ul>

****************************************/





