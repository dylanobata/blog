---
title: "Analysis of Algorithms"
date: 2021-05-23T16:44:00-07:00 
draft: false
---

The goal of analyzing an algorithm is to provide a *general* baseline for its efficiency, as measured by the time and space needed to finish its execution. To do this, we first need to specify an appropriate model of computation. We want our hypothetical model to be general enough so that our analysis remains true regardless of the device it is being executed on, and easy enough to reason with. The [Random-Access Machine (RAM)](https://en.wikipedia.org/wiki/Random-access_machine) model satisfies these requirements. The RAM model of computation behaves similarly to the common notion of an actual computer. We will make three assumptions about the behavior of our RAM model: 
1. Simple instructions take **one** time step to execute. 

2. Loops, functions, and other complex instructions take one or more time steps to execute. 

3. Memory access takes **one** time step and there is an infinite amount of memory.

With this, we can begin to think about time and space complexity.

## Time and Space Complexity

We can classify an algorithm's performance by its best-case, average-case, and worst-case time and space requirements. Performance is measured as a mathematical function on the length of the input. Instead of trying to precisely measure the  performance with an exact function, we instead try to provide general upper and lower bounds which limit the end behavior of the function. This allows us to drop constant multipliers and consider only the fastest growing term in the expression. For example, suppose we find out an algorithm takes exactly \\(3n^2 + 2n + 1\\) steps to execute. Instead of considering the entire expression, it is enough to say that this function grows quadratically with respect to the input size \\(n\\), or that it has a growth rate of \\(n^2\\).

 By providing bounds instead of an exact function, we simplify our analysis while still benefiting from useful estimates on the performance of the algorithm. It is common to plan for the worst-case scenario when analyzing an algorithm because it provides us with the strongest guarantee on performance and it is the easiest case to consider. The worst-case, best-case, and average-case complexities are denoted by \\(O(f(n)), \Omega (f(n))\\) and \\(\Theta(f(n))\\) respectively.

**Definition (Big O)**
: Let \\(f\\) and \\(g\\) be functions from the positive integers to the positive real numbers. We say \\( f(n) = O(g(n)) \\) if and only if there exists positive integers \\(c > 0 \\) and \\( n_0 > 0 \\) such that 
$$ f(n) \leq c \cdot g(n) \quad \text{ for all } n \geq n_0$$

That is to say for some input \\(n_0\\), any input after \\(n_0\\) makes the function \\(f(n)\\) smaller than \\(c \cdot g(n)\\). Therefore \\( f(n) \\) is **bounded above** by \\(c \cdot g(n)\\) and \\( f(n) \\) has O of \\( g(n)\\) complexity.

**Definition (Big \\(\Omega\\))**
: Let \\(f\\) and \\(g\\) be functions from the positive integers to the positive real numbers. We say \\( f(n) = \Omega(g(n)) \\) if and only if there exists positive integers \\(c > 0 \\) and \\( n_0 > 0 \\) such that 
$$ f(n) \geq c \cdot g(n) \quad \text{ for all } n \geq n_0$$

This definition is almost exactly the same as Big O except we flip the inequality sign. This means that \\( f(n) \\) is **bounded below** by \\( c \cdot g(n)\\) and we say \\(f(n) \\) has Omega of \\(g(n)\\) complexity.

**Definition (Big \\(\Theta\\))**
: Let \\(f\\) and \\(g\\) be functions from the positive integers to the positive real numbers. We say \\( f(n) = \Theta(g(n)) \\) if and only if there exists positive integers \\(c_1, c_2 > 0 \\) and \\( n_0 > 0 \\) such that 
$$ c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n) \quad \text{ for all } n \geq n_0$$

Here we note that \\(f(n)\\) is bounded above and below by the same function \\(g(n)\\) but with different constants \\(c_1\\) and \\(c_2\\). 

As mentioned above, we usually consider the worst-case scenario and as such, will only consider Big O analysis on the example we look at. 

**A quick remark on notation**

It is customary to use the symbol \\("="\\) to say that a function "is" a class of functions, i.e. \\(f(n)=O(f(n))\\), however the \\("="\\) symbol does not express equality. It is probably appropriate to think in terms of the notation \\(f(n) \in O(f(n))\\), read \\(f(n)\\) is an element of \\(O(f(n))\\). We use \\("="\\) instead of \\("\in" \\) largely for convenience. For example, the statement \\(n^3 + O(n) = O(n^3)\\) can be written using the \\("="\\) notation to express that \\(n^3\\) plus any equation from the class of \\(O(n)\\) will still be \\(O(n^3)\\). Equivallently, we would have to say \\( \\{n^3 + f(n) \mid f(n) \in O(n)\\} \subseteq O(n^3) \\) if we were to use the \\("\in" \\) notation, which is far more inconvenient.

## Properties of Big O
Big O notation has some useful properties we can work with. The main ones being addition, multiplication, and transitivity. 

### Additive Property
The additive property is a little different than the typical addition property we are used to working with. When using the additive property with Big O, we take the max of either class of functions. 

Let \\(f\\) and \\(g\\) be functions such that \\( f(n) = O(f(n))\\) and \\(g(n) = O(g(n))\\). Then

 $$ f(n) + g(n) = max(O(f(n)), O(g(n)))$$

Proof.
: Without loss of generality, suppose \\(f(n) \leq c_1 \cdot g(n)\\) for all \\(n \geq n_1\\) where \\(c_1\\) and \\(n_1\\) are positive integers . Then by definition, \\( f(n) = O(g(n))\\). Now \\( g(n) = O(g(n)) \\) means there exists positive integers \\(c_2, n_2\\) such that \\(g(n) \leq c_2\cdot g(n) \\) for all \\( n \geq n_2 \\). Choose \\(c_0 = 2 \cdot max\\{c_1,c_2\\}\\) and \\(n_0 = max\\{n_1,n_2\\}\\) so that 
$$
f(n) + g(n) \leq max\\{c_1,c_2\\} \cdot g(n) + max\\{c_1,c_2\\} \cdot g(n) =  2 \cdot max\\{c_1,c_2\\} \cdot g(n) = c_0 \cdot g(n)
$$ 
for all \\(n \geq n_0 \\). Thus, \\(f(n) + g(n) = max(O(f(n), O(g(n))\\).

### Multiplicative Property

**Multiplying Constants**

$$ O(c \cdot f(n)) = O(f(n)) \quad \text{ for } c>0$$

Proof.
: We need to find positive integers \\(c_0, n_0\\) so that \\(c \cdot f(n) \leq c_0 \cdot f(n)\\) for all \\(n \geq n_0\\). To do this, simply let \\(c_0 = c\\) and \\(n_0 = 1\\) so that \\(c \cdot f(n) = c_0 \cdot f(n)\\) for all \\(n \geq n_0\\), thereby satisfying the inequality \\(c \cdot f(n) \leq c_0 \cdot f(n)\\) for all \\(n \geq n_0\\). Thus, \\(O(c \cdot f(n)) = O(f(n)) \text{ for } c>0\\).

**Multiplying Functions**

$$ O(f(n)) \cdot O(g(n)) = O(f(n) \cdot g(n)) $$

Proof.
: By definition, there exists positive integers \\(n_1, n_2, c_1, c_2\\) such that \\(f(n) \leq c_1 \cdot f(n)\\) for all \\(n \geq n_1\\) and \\(g(n) \leq c_2 \cdot g(n)\\) for all \\(n \geq n_2\\). Since \\(c_1 \text{ and } c_2\\) are positive integers, the following inequality holds if we let \\(c_0 = c_1c_2\\) and \\(n_0 = n_1 \cdot n_2\\).

$$ f(n) \cdot g(n) \leq (c_1c_2) \cdot f(n) \cdot g(n) \quad \text{ for all }n \geq n_0$$ 

: Thus, \\( f(n) \cdot g(n) = O(f(n) \cdot g(n))\\).

### Transitive Property
 $$ \text{If } f(n) = O(g(n)) \text{ and } g(n) = O(h(n)) \text{ then } f(n) = O(h(n)) $$

Proof. 
: By definition, there exists positive integers \\(c_1, c_2, n_1,n_2\\) such that \\( f(n) \leq c_1 \cdot g(n) \\) for all \\( n \geq n_1\\) and \\( g(n) \leq c_2 \cdot h(n)\\) for all \\(n \geq n_2 \\). Choose \\(c_0 = max\\{c_1, c_2\\}\\) and \\(n_0 = max\\{n_1,n_2\\}\\) so that 

$$f(n) \leq c_1 \cdot g(n) \leq c_0 \cdot h(n) \quad \text{ for all } n \geq n_0$$

: Thus, \\(f(n) = O(h(n))\\) and transitivity holds.

## Dominance Relations and Little-o
When analyzing algorithms we encounter a few common classes of functions. These different classes are separated by their relative growth rates and can be seen below. The symbol \\(\ll\\) means "much less than" and in our context we say that \\(f(n) \ll g(n) \\) if \\( \lim_ {n \to \infty} \frac{f(n)}{g(n)} = 0  \\). This happens to be the exact definition for Little-o notation as well.

**Definition (Little-o)**
: Let \\(f\\) and \\(g\\) be functions from the positive integers to the positive real numbers. We say \\( f(n) = o(g(n)) \\) if and only if \\(\lim _{n \to \infty} \frac{f(n)}{g(n)} = 0\\).

**Theorem**
: Let \\( c, \lg n, n,  n \cdot \lg n, n^2, 2^n,\\) and \\(n!\\) be sequences from the positive integers to the nonnegative real numbers. Then
$$ c \ll \lg n \ll n \ll n \lg n \ll n^2 \ll 2^n \ll n!$$

: Where c is a constant greater than 0 and \\(\lg n\\) is defined to be \\( \log _2 n\\).

Proof.
: We need to show that \\( \frac{c}{\lg n}, \frac{\lg n}{n}, \frac{n}{n \lg n}, \frac{n \lg n}{n^2}, \frac{n^2}{2^n}\\) and \\( \frac{2^n}{n!}\\) all go to 0 as n approaches infinity. 

: For \\(\lim _{n \to \infty} \frac{c}{\lg n}\\) we can simply evaluate it to get 0.

$$\lim _{n \to \infty} \frac{c}{\lg n} = 0 $$

: For \\(\lim _{n \to \infty} \frac{\lg n}{n}\\) we can apply [LHospitals Rule](https://en.wikipedia.org/wiki/L%27Hôpital%27s_rule) since evaluating it would result in the indeterminate form \\(\frac{\infty}{\infty}\\). Applying L'Hospital's gives us:

$$ \lim _ {n \to \infty} \frac{n}{\lg n} = \frac{\infty}{\infty} \implies \lim_{n \to \infty} \frac{\frac{1}{n\ln (2)}}{1} = \frac{0}{1} = 0 $$ 

: For \\( \lim_{n \to \infty} \frac{n}{n \lg n}\\) we simplify with algebra first before evaluating:
    
$$\lim_{n \to \infty} \frac{n}{n \lg n} = \lim_{n \to \infty} \frac{1}{\lg n} = 0 $$

: For \\( \lim_{n \to \infty} \frac{n \lg n}{n^2}\\) we can simplify with algebra again, giving us our first relation again which we found to be 0:

$$ \lim_{n \to \infty} \frac{n \lg n}{n^2} = \lim_{n \to \infty} \frac{\lg n}{n} = 0  $$

: For \\( \lim_{n \to \infty} \frac{n^2}{2^n}\\) we apply L'Hospital's twice:

$$ \lim_{n \to \infty} \frac{n^2}{2^n} = \frac{\infty}{\infty} \implies \lim_{n \to \infty} \frac{2n}{2^n \ln(2)} = \frac{\infty}{\infty} \implies \lim_{n \to \infty} \frac{2}{2^n \ln^2(2)} = 0 $$


: Finally, to show \\(\lim_{n \to \infty} \frac{2^n}{n!} = 0 \\) requires a few observations. First, define the sequence \\( s_n = \frac{2^n}{n!} \\). Then the \\( (n+1)st \\) term is given by \\( s_{n+1} = \frac{2^{n+1}}{(n+1)!} = \frac{2 \cdot 2^n}{(n+1)n!} = \frac{2}{n+1}s_n \\). As \\(n\\) gets larger, \\(\frac{2}{n+1}\\) gets smaller, thus making \\(\frac{2}{n+1}s_n\\) smaller. So we have \\(s_n > s_{n+1}\\) for all positive integers \\(n\\). This is the definition of a montonically decreasing sequence. Furthermore, we know that the sequence \\(s_n\\) is bounded below by 0. Then by the [monotone convergence theorem](https://en.wikipedia.org/wiki/Monotone_convergence_theorem) we know there exists a limit \\(L\\) for the sequence \\(s_n\\). Combining this, we get 

$$ L = \lim _{n \to \infty} s _{n+1} = \lim _{n \to \infty} \frac{2}{n+1} \cdot \lim _{n \to \infty} s_n = 0 \cdot L = 0$$

: Thus the limit \\(L\\) is equal to 0 and we have shown that \\(\lim_{n \to \infty} \frac{2^n}{n!} = 0 \\).

As a baseline, algorithms should not exceed \\(O(n^2)\\) unless \\(n\\) is small.

## Analyzing Insertion Sort

[Insertion Sort](https://en.wikipedia.org/wiki/Insertion_sort) is a sorting algorithm that orders the elements of an array (this could be sorting an array of numbers from least to greatest, or sorting an array of strings in alphabetical order).

To illustrate insertion sort, suppose we have a hand of five playing cards, and we'd like to order the cards from least to greatest. Let's say the cards in our hand from left to right are: **3, 2, Ace, King**, and **Queen**. 

To start insertion sort, we look at the second leftmost card, in our case the **2** card. Now we check if its neighbor to the left is bigger; if it is we swap them. In our case it is (since \\(3 > 2\\)), so we swap them. Since there are no more neighbors to the left to compare the **2** card with, we proceed to the next step. Our new ordering is **2, 3, Ace, King, Queen**. 

Next we look at the third leftmost card, which is the **Ace** card. Again, we compare it to its neighbor to its left. Since **Ace** is smaller than **3**, we swap them. Now we compare the **Ace** to its neighbor to the left again, the **2** card. Again, since **Ace** is smaller than **2**, we swap them. Now that there are no neighbors to the left to compare it to, we arrive at the new ordering **Ace, 2, 3, King, Queen**. 

We now look at the fourth leftmost card, the **King**. We compare it to its neighbor to the left, and we see that the **King** is bigger than the **3** card. Since **King** is bigger than **3** and everything to the left of the **King** is sorted, we leave the **King** in place and continue to the next step of the algorithm. Our ordering remains **Ace, 2, 3, King, Queen**.

Now we look at the fifth leftmost card, the **Queen**. Again we compare it to its neighbor to the left, which is the **King**. Since the **King** is bigger than the **Queen**, we swap the cards. Now we compare the **Queen** to its neighbor to the left again, which is the **3**, and since the **Queen** is bigger, we keep it in place and stop comparing since the cards to the left of it are sorted. Our new ordering is **Ace, 2, 3, Queen, King**.

Finally, we check to see if there are anymore cards to sort and since there are none left, insertion sort is completed.

Here's what the code for the process just described looks like written in Python.

```python
def insertionSort(Array):
    i = 1
    while i < len(Array):
        j = i
        while j > 0 and Array[j-1] > Array[j]:
            Array[j], Array[j-1] = Array[j-1], Array[j]
            j -= 1
        i += 1
```

To begin our worst-case analysis we should identify what the worst case is. If we are sorting an array from least to greatest, then the worst case is if the elements are ordered from greatest to least.

The inner `while` loop can execute, in worst case, *j* times, since in a reverse ordered array, we will have to move the *jth* element, *j* times to get it to the front of the array. Since each of the operations in the inner `while` loop are simple, they will take \\(O(1)\\) time, and so the inner `while` loop will have a runtime of \\(O(j)\\). For simplicity, we will say the inner loop has a runtime of \\(O(n)\\), assuming *n* is the length of the array. We can do this since \\(j < n\\) so \\(j = O(n)\\).

The outer `while` loop will execute \\(n-1\\) times since we start at 1 and end at \\(n-1\\). We will round this number up to *n*. For each iteration \\(1, 2, \ldots , n\\) of the outer `while` loop, the inner `while` loop will execute *j* times, which we rounded up to *n* as well. Thus, we have *n* iterations each taking *n* steps to complete, so we get a worst case runtime of \\(O(n^2)\\).

Regarding the space complexity of the algorithm, the assignments `i=1` and `j=1` are \\(O(1)\\), and since we sorted the array in-place, insertion sort has an \\(O(1)\\) space complexity.

