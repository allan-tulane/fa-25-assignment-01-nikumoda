

# CMPS 2200 Assignment 1

**Name:** Nikhil Modayur

In this assignment, you will learn more about asymptotic notation, parallelism, functional languages, and algorithmic cost models. As in the recitation, some of your answer will go here and some will go in `main.py`. You are welcome to edit this `assignment-01.md` file directly, or print and fill in by hand. If you do the latter, please scan to a file `assignment-01.pdf` and push to your github repository. 
  
  

1. (2 pts ea) **Asymptotic notation** (12 pts)

  - 1a. Is $2^{n+1} \in O(2^n)$? Why or why not?

Yes, because there exists some value of c such that c*2^n >= 2^(n+1) for all n>1
.  c*2^n = 2^(c+n) 
.  when c=2
.  2^n+2 >= 2^(n+1)
. 
  - 1b. Is $2^{2^n} \in O(2^n)$? Why or why not?     
.  no it is not since there is no value of c such that  c*2^n > 2^(2^n) for all n
.  2^(n+c) > 2^(2^n) then take log2 of both sides
.  n+c > 2^n is not true so n+c < 2^n 
.  
.  
  - 1c. Is $n^{1.01} \in O(\mathrm{log}^2 n)$?    
.  It is not since there is no value of c such that n^(1.01)<= c*log^2(n) for all n 
.  n^1 = n<n^1.01
.  n < clog^2(n) 
. n increases as a polynomial and log increases less than that so n will always increase faster when n is big enough no matter the c value

  - 1d. Is $n^{1.01} \in \Omega(\mathrm{log}^2 n)$?
It is since lim n->infinity of n^1.01/log(n)^3 = infinity
. this is because n^1.01 grows like a polynomial and log(n)^3 grows logarithmically 
.  regardless of the c value for all n eventually n^1.01 will be greater than log^2(n)
.  
  - 1e. Is $\sqrt{n} \in O((\mathrm{log} n)^3)$?  
.  It is not since lim n->infinity of root(n)/log(n)^3 = infinity
.  this is because root(n) grows like a polynomial and log(n)^3 grows logarithmically 
.  
.  
  - 1f. Is $\sqrt{n} \in \Omega((\mathrm{log} n)^3)$?  
.  It is since lim n->infinity of root(n)/log(n)^3 = infinity
. this is because root(n) grows like a polynomial and log(n)^3 grows logarithmically 


2. **SPARC to Python** (12 pts)

Consider the following SPARC code of the Fibonacci sequence, which is the series of numbers where each number is the sum of the two preceding numbers. For example, 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610 ... 
$$
\begin{array}{l}
\mathit{foo}~x =   \\
~~~~\texttt{if}{}~~x \le 1~~\texttt{then}{}\\
~~~~~~~~x\\   
~~~~\texttt{else}\\
~~~~~~~~\texttt{let}{}~~(ra, rb) = (\mathit{foo}~(x-1))~~,~~(\mathit{foo}~(x-2))~~\texttt{in}{}\\  
~~~~~~~~~~~~ra + rb\\  
~~~~~~~~\texttt{end}{}.\\
\end{array}
$$ 

  - 2a. (6 pts) Translate this to Python code -- fill in the `def foo` method in `main.py`  

  - 2b. (6 pts) What does this function do, in your own words?  

.  This function return the fibonnaci sequence for an input x greater than 0
.  The function has two bases cases when x==1 return one and when x==0 return 0
.  It uses the recursive algorithm x = x-1 +x-2 ...1 until the base case is reached and then the recrusive calls 
.  
.  
.  
.  
.  
  

3. **Parallelism and recursion** (26 pts)

Consider the following function:  

```python
def longest_run(myarray, key)
   """
    Input:
      `myarray`: a list of ints
      `key`: an int
    Return:
      the longest continuous sequence of `key` in `myarray`
   """
```
E.g., `longest_run([2,12,12,8,12,12,12,0,12,1], 12) == 3`  
 
  - 3a. (7 pts) First, implement an iterative, sequential version of `longest_run` in `main.py`.  

  - 3b. (4 pts) What is the Work and Span of this implementation?  

.  the work is O(n) since the entire list is iterated through so n elements are oparted on
.  the span is O(n) since the list is iterated through so element 1 is iterated then element 2 all the way until n 
.  
.  
.  
.  
.  
.  
.  


  - 3c. (7 pts) Next, implement a `longest_run_recursive`, a recursive, divide and conquer implementation. This is analogous to our implementation of `sum_list_recursive`. To do so, you will need to think about how to combine partial solutions from each recursive call. Make use of the provided class `Result`.   

  - 3d. (4 pts) What is the Work and Span of this sequential algorithm?  
.  The work is W(n) = 2w(n/2) + O(1)
.  so the work is O(n) 
.  S(n) = S(n/2) + O(1)
.  so the span is O(logn)
.  
.  
.  
.  
.  
.  
.  


  - 3e. (4 pts) Assume that we parallelize in a similar way we did with `sum_list_recursive`. That is, each recursive call spawns a new thread. What is the Work and Span of this algorithm?  

.  If we parallelize using contraction in the same way we did 'sum_list_recursive' in class
.  the new work is W(n) = W(n/2) + O(n)
.  this work is O(lg(n)n
.  the span is the same so O(lg(n))
.  
.  
.  
.  

