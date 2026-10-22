# Sets and Functions: From First Principles to Expert Reasoning

> A rigorous, intuition-first guide to sets, functions, their properties, real-world applications, counterexamples, and proof-based challenges.

## Learning objectives

By the end, you should be able to:

- Define sets and functions precisely, including their domains and codomains.
- Work confidently with set operations, Cartesian products, and power sets.
- Distinguish injective, surjective, and bijective functions.
- Explain why function properties depend on the domain and codomain.
- Connect the theory to databases, AI, and robotic process automation (RPA).
- Construct counterexamples and write short mathematical proofs.

## 1. Sets: The mathematics of membership

A **set** is a well-defined collection of distinct elements.

$$A=\{2,4,6,8\}$$

We write $4\in A$ and $5\notin A$. Order and repetition do not matter:

$$\{2,4,6\}=\{6,2,4,4\}.$$

**Mental model:** A set is a *membership rule*, not a storage container. The important question is whether an object belongs, not how often it appears.

### Fundamental operations

Let $A=\{1,2,3\}$ and $B=\{3,4,5\}$.

| Operation | Notation | Meaning | Result |
|---|---|---|---|
| Union | $A\cup B$ | In A or B | $\{1,2,3,4,5\}$ |
| Intersection | $A\cap B$ | In both | $\{3\}$ |
| Difference | $A\setminus B$ | In A but not B | $\{1,2\}$ |
| Symmetric difference | $A\triangle B$ | In exactly one | $\{1,2,4,5\}$ |
| Subset | $A\subseteq C$ | Every A element is in C | Depends on C |
| Complement | $A^c$ | Outside A within universe U | $U\setminus A$ |

These operations parallel Boolean logic: union is OR, intersection is AND, and complement is NOT.

### The empty set and subtle counterexamples

- $\varnothing\subseteq A$ for every set $A$ (vacuous truth).
- $\varnothing\neq\{\varnothing\}$: the first has zero elements; the second has one.
- $x\in A$ and $x\subseteq A$ express different relationships.
- Sets may contain strings, people, other sets, or abstract objects—not only numbers.

### Power sets

The **power set** $\mathcal P(A)$ is the set of all subsets of $A$.

For $A=\{a,b,c\}$:

$$\mathcal P(A)=\{\varnothing,\{a\},\{b\},\{c\},\{a,b\},\{a,c\},\{b,c\},\{a,b,c\}\}.$$

Each element can be included or excluded, giving:

$$|\mathcal P(A)|=2^{|A|}.$$

**Application:** Ten independent on/off configuration switches create $2^{10}=1024$ configurations. Exhaustive testing can therefore become expensive.

### Cartesian products

$$A\times B=\{(a,b)\mid a\in A,\ b\in B\}.$$

For $A=\{1,2\}$ and $B=\{x,y\}$:

$$A\times B=\{(1,x),(1,y),(2,x),(2,y)\}.$$

Order matters in ordered pairs: $(1,x)$ is not generally $(x,1)$.

## 2. Functions: The mathematics of mapping

A function $f:A\to B$ assigns **exactly one** output in $B$ to **every** input in $A$.

- **Domain:** $A$, the permitted inputs.
- **Codomain:** $B$, the declared target set.
- **Image/range:** $f(A)=\{f(a):a\in A\}$, the outputs actually reached.

A function can be understood as a relation (a subset of $A\times B$) with exactly one ordered pair for each first coordinate in $A$.

**Valid:** $\{(1,x),(2,x)\}$ defines a function $\{1,2\}\to\{x,y\}$.

**Invalid:** $\{(1,x),(1,y),(2,x)\}$ does not define a function because input 1 has two outputs.

> A function need not give different outputs to different inputs. It must only give one output per input.

### Injective: No collisions

$f$ is **injective** if:

$$f(a)=f(b)\implies a=b.$$

Distinct inputs cannot collapse into the same output. Think of a unique employee ID assigned to each employee.

### Surjective: Complete coverage

$f:A\to B$ is **surjective** if:

$$\forall b\in B,\ \exists a\in A:\ f(a)=b.$$

Every codomain element is reached. Think of ensuring every support team has at least one assigned employee.

### Bijective: One-to-one correspondence

A function is **bijective** if it is both injective and surjective. A bijection has an inverse function $f^{-1}:B\to A$.

| Property | No collisions? | Every codomain output reached? | Inverse function on all B? |
|---|---|---|---|
| Injective | Yes | Not necessarily | Not necessarily |
| Surjective | Not necessarily | Yes | Not necessarily |
| Bijective | Yes | Yes | Yes |

### Why the domain and codomain matter

Consider the same formula $f(x)=x^2$.

1. $f:\mathbb R\to\mathbb R$ is **neither** injective nor surjective: $f(-2)=f(2)$, and no negative real is reached.
2. $f:[0,\infty)\to[0,\infty)$ is **bijective**: every nonnegative output has exactly one nonnegative square root.

**Key insight:** A formula alone does not completely specify a function; the domain and codomain are essential.

## 3. Multiple perspectives

### Logic perspective

Set union, intersection, and complement correspond to OR, AND, and NOT. A set can be represented by its characteristic function:

$$\mathbf 1_A(x)=\begin{cases}1 & x\in A\\0 & x\notin A.\end{cases}$$

Then intersection becomes multiplication of 0/1 membership values:

$$\mathbf 1_{A\cap B}(x)=\mathbf 1_A(x)\mathbf 1_B(x).$$

### Information perspective

Injective functions preserve distinctions between inputs. For example, $f(x)=|x|$ loses the sign: $f(-5)=f(5)=5$. Knowing the output does not reveal which input was used.

### Pipeline perspective

If $f:A\to B$ and $g:B\to C$, their composition is:

$$(g\circ f)(x)=g(f(x)).$$

This is the formal structure of an ETL or RPA processing pipeline.

**Important theorem:** If $g\circ f$ is injective, then $f$ must be injective. But $g$ need not be injective on all of $B$.

### Infinite-set perspective

The natural numbers $\mathbb N=\{1,2,3,\dots\}$ and the positive even numbers $E=\{2,4,6,\dots\}$ have the same cardinality because $f(n)=2n$ is a bijection $\mathbb N\to E$—even though $E$ is a proper subset of $\mathbb N$.

## 4. Applications in software engineering

### RPA and queue processing

Let $Q$ be a set of queue items and $S$ a set of statuses. At a fixed instant $t$:

$$status_t:Q\to S.$$

Every queue item has one current status. A transition function can model processing:

$$T:S\times E\to S,$$

where $E$ is a set of events (success, failure, retry, timeout). Real systems may require additional state to make the transition deterministic.

**Practical question:** Does your retry logic produce a valid transition for every supported state/event combination?

### Databases

A primary key can define a function from unique keys to records. Duplicate conflicting records violate uniqueness. SQL `UNION`, `INTERSECT`, and `EXCEPT` resemble set operations, but SQL queries often use *bag semantics* and may preserve duplicates.

### Machine learning

A classifier can be modeled as:

$$f:\text{Feature Vectors}\to\text{Predicted Labels}.$$

Different inputs often map to the same class, so classification functions are typically not injective. A class may never be predicted, so surjectivity is not guaranteed either.

## 5. Counterexample toolkit

Before accepting a mathematical statement, ask whether you can break it with the smallest possible example.

| Claim | Counterexample / correction |
|---|---|
| Every function is injective | $f:\{1,2\}\to\{a\}$ with both inputs mapped to $a$ |
| Every injective function is surjective | $f:\{1\}\to\{a,b\}$, $f(1)=a$ |
| Every surjective function is injective | $f:\{1,2\}\to\{a\}$ |
| $f(x)=x^2$ is always non-injective | Restrict domain to $[0,\infty)$ |
| Every proper subset has smaller cardinality | Positive even integers versus positive integers |

## 6. Expert-level assessment

Try these without looking at the answers.

1. If $|A|=3$ and $|B|=2$, how many functions $A\to B$ exist?
2. Is $f:\mathbb R\to\mathbb R$, $f(x)=x^3$, injective, surjective, bijective, or neither?
3. Which is always true: $\varnothing\in A$ or $\varnothing\subseteq A$?
4. If $g\circ f$ is injective, what must be true of $f$?
5. If $|A|=5$ and $|B|=3$, can a function $A\to B$ be injective? Surjective?
6. If $|A|=4$, how many binary relations on $A$ exist?

<details>
<summary>Reveal answers and explanations</summary>

1. $2^3=8$. Each domain element independently selects one of two outputs.
2. Bijective: $x^3$ is strictly increasing and every real number has a real cube root.
3. $\varnothing\subseteq A$. The empty set need not be an element of $A$.
4. $f$ must be injective. If $f(a)=f(b)$, then $g(f(a))=g(f(b))$, and injectivity of $g\circ f$ forces $a=b$.
5. Not injective (pigeonhole principle); surjective is possible.
6. $2^{16}=65,536$. There are $4\times4=16$ possible ordered pairs; each relation is a subset of them.

</details>

## 7. Proof challenges

### Challenge A: Inverse identities

Given $f:A\to B$ and $g:B\to A$ such that

$$g\circ f=id_A,\qquad f\circ g=id_B,$$

prove that $f$ and $g$ are bijections and inverses.

### Challenge B: Count surjections

If $|A|=4$ and $|B|=3$, how many surjective functions $A\to B$ exist?

*Hint:* Apply inclusion–exclusion to $3^4$ total functions.

### Challenge C: Preimages

Suppose for every $X\subseteq A$,

$$f^{-1}(f(X))=X.$$

Prove $f$ is injective. Here $f^{-1}(Y)$ denotes a **preimage**, which is defined even when $f$ is not bijective.

<details>
<summary>Proof sketches</summary>

- **A:** $g\circ f=id_A$ implies $f$ is injective and $g$ is surjective. $f\circ g=id_B$ implies $f$ is surjective and $g$ is injective. Thus both are bijections and inverse to one another.
- **B:** $3^4-\binom31 2^4+\binom32 1^4=81-48+3=36$.
- **C:** If $f(a)=f(b)$, let $X=\{a\}$. Then $b\in f^{-1}(f(X))=X$, so $b=a$. Thus $f$ is injective.

</details>

## 8. Mental model to remember

> **Sets** specify which objects are possible. **Functions** map objects between sets. **Properties** tell us whether mappings preserve distinctions, cover the target, or permit reversal.

The mathematician's habit is to ask:

1. What exactly is defined?
2. What follows logically from the definition?
3. What is the smallest counterexample to a tempting claim?
4. Does changing the domain or codomain change the conclusion?

---

### Suggested next topics

- Relations and equivalence classes
- Partial orders and lattices
- Mathematical induction and proof techniques
- Countability and cardinality
- Function composition, inverses, and transformations
- Discrete mathematics for computer science and automation
