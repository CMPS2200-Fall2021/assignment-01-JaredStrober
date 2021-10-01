

# CMPS 2200 Assignment 1

**Name:**
Group: Jared, Bharat, Rosey


In this assignment, you will learn more about asymptotic notation, parallelism, functional languages, and algorithmic cost models. As in the recitation, some of your answer will go here and some will go in `main.py`. You are welcome to edit this `assignment-01.md` file directly, or print and fill in by hand. If you do the latter, please scan to a file `assignment-01.pdf` and push to your github repository. 
  
  

1. **Asymptotic notation**

  - 1a. Is $2^{n+1} \in O(2^n)$? Why or why not? 
.  
    Yes, the constant in the $2^{n+1}$, 1, does not affect the growth rate of the equation. If you graph both the functions, you can see easily that $2^{n+1}$ is far within
    $O(2^n)$. If you took the limit of $g(n)/F(n)$ you would arrive at $2*2^n/n^2$ <= C which simplifies to 2 <= C. 
.  
.  
. 
  - 1b. Is $2^{2^n} \in O(2^n)$? Why or why not?     
.  
    No, as the limit approaches inf. with $g(n)/F(n)$ being $2^2^n/2^n$ it simplifies to $(ln 2)(2^2^n)$ != C.
.  
.  
.  
  - 1c. Is $n^{1.01} \in O(\mathrm{log}^2 n)$?    
.  
    No, when graphing both functions, you can clearly see that $n^{1.01}$ is not within $O(\mathrm{log}^2 n)$. Furthermore, iif you work out the math 
    using L'Hosptials rule, the limit is inf. To see this derivative of $g'(n)/f'(n)$, you end up with $1.01^2*n/2 = 1.01^2/2$ * x = inf
.  
.  

  - 1d. Is $n^{1.01} \in \Omega(\mathrm{log}^2 n)$?  
.  
Yes, using that the logic above means that $n^{1.01} \in O(\mathrm{log}^2 n)$ is False as the limit is inf.
    $n^{1.01} \in \Omega(\mathrm{log}^2 n)$ would be true as the opposite of 1c. 
.  
.  
  - 1e. Is $\sqrt{n} \in O((\mathrm{log} n)^3)$?  
.  

No, because the limit is inf. If you plug in $\sqrt{n} for g(n) and O((\mathrm{log} n)^3)$ for f(n), and you use L'Hosptials rule it results in 2 * n/$\sqrt{n} and finally to $\sqrt{n} = inf. 
.  
  - 1f. Is $\sqrt{n} \in \Omega((\mathrm{log} n)^3)$?  
.  
Yes, because 1e is False, by the definition of $\Omega$ and 'big O, $\sqrt{n}$ is not $\in \Omega((\mathrm{log} n)^3)$.
.  
.  

  - 1g. Consider the definition of "Little o" notation:
  
$g(n) \in o(f(n))$ means that for **every** positive constant $c$, there exists a constant $n_0$ such that $g(n) \le c \cdot f(n)$ for all $n \ge n_0$. There is an analogous definition for "little omega" $\omega(f(n))$. The distinction between $o(f(n))$ and $O(f(n))$ is that the former requires the condition to be met for **every** $c$, not just for some $c$. For example, $10x \in o(x^2)$, but $10x^2 \notin o(x^2)$.  

.  

**Prove** that $o(g(n)) \cap \omega(g(n))$ is the empty set.  

Let f(n) be in $o(g(n))$ and f(n) be in $\omega(g(n))$.
Thus F(n) < c * g(n) and F(n) > c * g(n) for every constant c

So f(n) < g(n) and f(n) < g(n)
The above is not true for every constant because when c = 1, the above is false and $o(g(n)) \cap \omega(g(n))$ is an empty set.



2. **SPARC to Python**

Consider the following SPARC code:  
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

  - 2a. Translate this to Python code -- fill in the `def foo` method in `main.py`  

  - 2b. What does this function do, in your own words?  

It is the fibonacci sequence. The fibonacci sequence is that is the sum of the previous two numbers. 
The only complex about this version of the fib function is that rather then returning foo(x-1) + foo(x-2),
the function assigns them to two values ra, rb, and then returns the sum of the two numbers. 
  


3. **Parallelism and recursion**

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
 
  - 3a. First, implement an iterative, sequential version of `longest_run` in `main.py`.  

  - 3b. What is the Work and Span of this implementation?  

The work is O(n) and the span is O(N). ~~This is because the function iterates over 
each item in the list, and then saves the count to memory.~~ 


  - 3c. Next, implement a `longest_run_recursive`, a recursive, divide and conquer implementation. This is analogous to our implementation of `sum_list_recursive`. To do so, you will need to think about how to combine partial solutions from each recursive call. Make use of the provided class `Result`.   

  - 3d. What is the Work and Span of this sequential algorithm?  

The work is O(n) and the span is O(n log n)

  - 3e. Assume that we parallelize in a similar way we did with `sum_list_recursive`. That is, each recursive call spawns a new thread. What is the Work and Span of this algorithm?  

    Work = O(N)
    Span = O(log n)