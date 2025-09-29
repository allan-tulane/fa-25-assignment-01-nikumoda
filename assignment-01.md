# CMPS 2200 Assignment 1

**Name:** Nikhil Modayur

In this assignment, you will learn more about asymptotic notation, parallelism, functional languages, and algorithmic cost models. As in the recitation, some of your answer will go here and some will go in `main.py`. You are welcome to edit this `assignment-01.md` file directly, or print and fill in by hand. If you do the latter, please scan to a file `assignment-01.pdf` and push to your github repository. 
  
  

1. (2 pts ea) **Asymptotic notation** (12 pts)

  - 1a. Is $2^{n+1} \in O(2^n)$? Why or why not?

Yes, because $2^{n+1} = 2 \cdot 2^n$, so for $c=2$, $c \cdot 2^n \geq 2^{n+1}$ for all $n \geq 1$. Thus, $2^{n+1}$ grows at the same rate as $2^n$ up to a constant factor.

  - 1b. Is $2^{2^n} \in O(2^n)$? Why or why not?     
No, because $2^{2^n}$ grows much faster than $2^n$. There is no constant $c$ such that $c \cdot 2^n \geq 2^{2^n}$ for all large $n$. Taking logarithms, $n + \log_2 c < 2^n$ for large $n$, which is not true.

  - 1c. Is $n^{1.01} \in O(\mathrm{log}^2 n)$?    
No, $n^{1.01}$ grows much faster than $(\log n)^2$ for large $n$. There is no constant $c$ such that $n^{1.01} \leq c \cdot (\log n)^2$ for all large $n$.

  - 1d. Is $n^{1.01} \in \Omega(\mathrm{log}^2 n)$?
Yes, because $n^{1.01}$ grows polynomially while $(\log n)^2$ grows much slower. For large $n$, $n^{1.01}$ will always eventually be greater than $c \cdot (\log n)^2$ for any constant $c$.

  - 1e. Is $\sqrt{n} \in O((\mathrm{log} n)^3)$?  
No, $\sqrt{n}$ grows faster than $(\log n)^3$ for large $n$. The limit $\lim_{n \to \infty} \frac{\sqrt{n}}{(\log n)^3} = \infty$, so $\sqrt{n}$ is not in $O((\log n)^3)$.

  - 1f. Is $\sqrt{n} \in \Omega((\mathrm{log} n)^3)$?  
Yes, for large $n$, $\sqrt{n}$ grows faster than $(\log n)^3$, so $\sqrt{n}$ is in $\Omega((\log n)^3)$.


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

This function computes the $x$th Fibonacci number recursively. If $x$ is 0 or 1, it returns $x$. Otherwise, it returns the sum of the Fibonacci numbers for $x-1$ and $x-2$.

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

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

The work is $O(n)$ because every element in the list is checked once. The span is also $O(n)$ since the algorithm is sequential and each step depends on the previous one.

  
  
  
  
  
  
  
  
  
  
  
  

  - 3c. (7 pts) Next, implement a `longest_run_recursive`, a recursive, divide and conquer implementation. This is analogous to our implementation of `sum_list_recursive`. To do so, you will need to think about how to combine partial solutions from each recursive call. Make use of the provided class `Result`.   

  - 3d. (4 pts) What is the Work and Span of this sequential algorithm?  

The work is $O(n)$, as each element is processed. The span is $O(\log n)$, since the recursive calls divide the problem in half at each step.

  
  
  
  
  
  
  
  
  
  
  
  

  - 3e. (4 pts) Assume that we parallelize in a similar way we did with `sum_list_recursive`. That is, each recursive call spawns a new thread. What is the Work and Span of this algorithm?  

If each recursive call is parallelized, the work remains $O(n)$, but the span becomes $O(\log n)$, as the recursive calls can be executed in parallel, reducing the longest dependency chain.

  
  