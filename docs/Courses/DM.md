# Discrete Mathematics 离散数学及其应用

## 1 The Foundations: Logic and Proofs

### 1.1 Propositional Logic

具有确切真值的陈述句称为命题（proposition）

<img src="../images/1680357094712-889beccc-1e70-48a7-a8fd-6cd61a404720.png" style="zoom:50%;" /><img src="./../images/1680357191227-9ffc1cbd-9e1d-4fe7-be01-484107f95010.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680357221008-1a4777d3-7ac7-4e8e-a56b-24b189b9846b.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680357561481-a2a67ed9-e645-4c80-954e-ccc705a2b230.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680357576719-7f6ad027-2e38-4e22-816b-12e6905c500f.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680357258142-1099e51a-f8b9-411a-b0c3-3ff399ddb585.png" alt="image.png" style="zoom:50%;" />

- 复合命题有组成，则有2的n次方行

- n个命题变量可以构造 $2^{2^n}$ 不同 (非等价) 命题propositions

<img src="../images/1680357682282-04a2d989-fc7f-4481-bea4-4ab1b0138e67.png" alt="image.png" style="zoom: 50%;" /><img src="../images/1680357699174-bdd037f0-53d1-4f3a-9f0c-43cc09993052.png" alt="image.png" style="zoom: 50%;" /><br />**_p ∨ q (disjunction of p and q_): **the proposition “_p or q_,” which is true if and only if at least one of p and q is true 

**p ∧ q (conjunction of p and q): ** the proposition “_p and q_,” which is true if and only if both p and q are true

**p ⊕ q (exclusive or of p and q): ** the proposition “_p XOR q_,” which is true when exactly one of p and q is true

**_p → q (_p _implies q_): **the proposition “if _p_, then _q_,” which is false if and only if p is true and q is false

### 1.2 Applications of Propositional Logic

对偶复合命题

The dual compound proposition that contains only the logical operator: $∧,∨,﹁$, the proposition obtained by replacing each ∨ by ∧ , each by ∨ ∧, each T by F, and each F by T. The dual of S is denoted by S*.

### 1.3 Propositional Equivalences
<img src="../images/1680357836154-29943e22-f369-430a-a639-f2c88424a2ef.png" alt="永真式和矛盾式的例子" title="永真式和矛盾式的例子" style="zoom: 50%;" /><img src="../images/1680358054610-00a1876a-5c97-440e-b9f7-985bff5ced41.png" alt="image.png" style="zoom: 50%;" /><img src="../images/1680357992903-4a0d26ae-5277-4e5d-ad52-7ab7338d37aa.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680358037830-26565d28-123c-44c1-b926-9a9295cdc57f.png" alt="image.png" style="zoom:50%;" /><br />A **minterm** is a conjunctive of literals in which each variable is *represented exactly once*. For example, If a formula has the variables p, q, r, then p∧¬q∧ r is a minterm, but p∧¬q and p∧¬p∧r are not.

Disjunctive normal form 析取范式：取各命题变量或其否定的合取式 ∧ 的析取式∨，其中每一组合取试对应一组真值组合，从而使该复合命题为真。 eg, (a∧b)∨(c∧d)∨(e∧f). 

If a formula is expressed as a disjunction of minterms, it is said to be in **full disjunctive normal form** 全析取范式.<br />For example, <img src="../images/1709888768963-32c02aab-a33a-496d-8cb7-84e8e53ef44b.png" alt="image.png" style="zoom:40%;" />，括号间用析取∨连接。**Every compound proposition is logically equivalent to a full DNF**

- Disjunctive析取范式（）外由析取∨连接，（）内由合取∧连接
- Conjunctive合取范式（）外由合取∧连接，（）内由析取∨连接

Any formula A is tautologically equivalent to a formula in full disjunctive normal form<img src="../images/1709888820747-0ea6f319-01c2-4209-9c96-4084c33ff606.png" alt="image.png" style="zoom:40%;" />

其他逻辑运算符<img src="../images/1709889206692-c69d2e2d-d9e3-4506-81df-9de37a0c83cd.png" alt="image.png" style="zoom:33%;" />

给定一个联结词集合，如果所有命题公式都能用其中的联结词等价表示出来，则称该联结词集合为全功能联结词集合，或称该联结词集合为功能完备的 functionally complete 。

例如，{ ¬ , ∨ , ∧ } 、、{ ¬ , ∨ } 、{ ¬ , ∧ }  都是全功能联结词集合，还有 { ¬ , → } 、{ ↑ }、{ ↓ }  也是。

### 1.4 Predicates and Quantifiers
∃：existential quantifier<br />∃∀ 有最高级优先权

<img src="../images/1680358129991-0d5244b5-4cfd-49c6-bcaf-6176277ec62b.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680358254369-939000f9-f547-4bb0-b645-aa7ebecef2ee.png" alt="image.png" style="zoom:50%;" />

Uniqueness<br />**∃!x, P(x)** == **one and only one x** in the universe of the discourse

#### More logical equivalences
<img src="../images/1710662872231-c1401929-fc0e-4509-a772-9e28e5052beb.png" alt="image.png" style="zoom:33%;" /><br /><img src="../images/1710662991109-e33f6958-be09-469b-a5f6-1d1d139be119.png" alt="image.png" style="zoom:33%;" /><img src="../images/1710662951958-8669be9e-8316-43d6-80db-e0480b28caad.png" alt="image.png" style="zoom:33%;" />

#### Example

1. "Every student in this class has taken a course in Java."

   Solution 1: If U is all students in this class, define a propositional function J(x) denoting "x has taken a course in Java" and translate as **∀x J(x)**.

   Solution 2: But if U is all people, also define a propositional function S(x) denoting "x is a student in this class" and translate as **∀x (S(x)→J(x))**

! note：

**∀x (S(x)∧J(x))** is not correct 它的意思是所有人都在这个班级中且上了Java课程

2. "Some student in this class has taken a course in Java."

   Solution 1: If U is all students in this class, translate as **∃x J(x)**

   Solution 2: But if U is all people, then translate as **∃x (S(x)∧J(x)**)

!note:

**∃x (S(x) -> J(x))** is not correct 它包括了那些不在这个班级上的人也上了Java课程，与题意不符

### 1.5 Nested Quantifiers
<img src="../images/1680358357297-00d64bba-5d71-43b9-9469-5e08c206c6ab.png" alt="image.png" style="zoom:50%;" />

#### Prenex normal form 前束范式
How to obtain prenex normal form?<br />1. Eliminate all occurrences of → and ↔ from the formula in question.<br />2. Move all negations inward such that, in the end, negation only appear as part of literals.<br />3. Standardize the variables a part (when necessary).<br />4. The prenex normal form can now be obtained by moving all quantifiers to the front of the formula.
##### Example
<img src="../images/1710663120448-5261fd4a-8a97-4f82-99f1-53beb03a5cd5.png" alt="image.png" style="zoom:33%;" /><br /><img src="../images/1710663203310-fa39b626-3ddd-44eb-874f-692528a01651.png" alt="lQLPJwkSsoM9RinNBBbNB3SwRC7cruSXu-0F44WZXc4xAA_1908_1046.png" style="zoom: 33%;" /><br /> 第二个任意y可以不用换成任意u，直接把任意y提到前边就OK 

### 1.6 Rules of Inference
<img src="../images/1680358553359-ddf4a635-8686-4430-8dbd-bde3045924dd.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680785925500-25992037-1c49-4da0-9d48-5f1e7d28813a.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680358608298-0c38565e-e945-4302-a7b7-31ba046053c0.png" alt="image.png" style="zoom: 50%;" />

##### Example
Show that the premises “A student in this class has not read the book,” and “Everyone in this class passed the first exam” imply the conclusion “Someone who passed the first exam has not read the book.

Solution: Let C(x) be “x is in this class,” B(x) be “x has read the book,” and P(x) be “x passed the first exam.” The premises are ∃x(C(x) ∧ ¬B(x)) and ∀x(C(x) → P(x)). The conclusion is ∃x(P(x) ∧ ¬B(x)). These steps can be used to establish the conclusion from the premises.

Step Reason:

1. ∃x(C(x) ∧ ¬B(x)) 	Premise
2. C(a) ∧ ¬B(a) 		Existential instantiation from (1)
3. C(a) 				Simplification from (2)
4. ∀x(C(x) → P(x)) 	Premise
5. C(a) → P(a) 		Universal instantiation from (4)
6. P(a) 				Modus ponens from (3) and (5)
7. ¬B(a) 			Simplification from (2)
8. P(a) ∧ ¬B(a) 		Conjunction from (6) and (7)
9. ∃x(P(x) ∧ ¬B(x)) 	Existential generalization from (8)

Fallacy 谬论

Universal modus ponens广泛假言推理：

∀x(P(x) → Q(x)) 
P(a), a 是域中的一个特定值
=> Q(a)

∀x(P(x) → Q(x)) 
¬Q(a), a 是域中的一个特定值
=> ¬P(a)

### 1.7 Introduction to Proofs
定理(theorem):可以证明为真的数学断言。
猜想(conjecture):真值未知的数学断言。
证明(proof):对定理为真的展示过程。
公理(axiom):假设为真的并可作为基础用来证明定理的命题。
引理(lemma):用来证明其他定理的定理。
推论(corollary):可以被证明是刚刚证明的一个定理的结论的命题。

### 1.8 Proof Methods and Strategy

**proof by contraposition 反证法: **a proof that p → q is true that proceeds by showing that p must be false when q is false <br />**proof by contradiction 归谬法: **a proof that p is true based on the truth of the conditional statement ¬_p → q_, where q is a contradiction <br />**exhaustive proof 穷举法: **a proof that establishes a result by checking a list of all possible cases <br />**proof by cases: **a proof broken into separate cases, where these cases cover all possibilities
**Mathematical induction** 数学归纳法：详见 [5](#5 Induction and Recursion)

**counterexample** 反例



## 2 Basic Structures: Sets, Functions, Sequences, Sums, and Matrices
### 2.1 Sets
**N **= {0_, 1_, _2_, _3_, _…}_, the set of all **natural numbers **自然数集<br />**Z **= {… _,_−2_,_−1, _0_, 1, 2, …}, the set of all **integers **整数集<br />**Z**+ = {1, 2, _3_, _…}_, the set of all **positive integers **正整数集<br />**Q **= {p/q ∣ p ∈ **Z**, q ∈ **Z**, and q ≠ 0}, the set of all **rational numbers **有理数集
**R**, the set of all **real numbers** 实数集<br />**R**+, the set of all **positive real numbers ** 正实数集<br />**C**, the set of all **complex numbers** 复数集

【Definition】A set is an unordered collection of objects

---

_**A ⊆ B**：_∀_x_(_x ∈ A  →  x ∈  B_)

For every set _S_,  ∅ ⊆ _S_

**S = T (set equality): **  S and T have the same elements（集合中的元素顺序或者重复元素不影响结果）

**S ⊆ T (S is a subset子集 of T): **every element of  S  is also an element of T

_**S ⊂ T** (_S is a **proper subset真子集** of T): S is a subset of T and S ≠ T 

**finite set** 有限集: a set with n elements, where n is a nonnegative integer

**infinite set** 无限集: a set that is not finite 

**|S| (the cardinality/size of _S_)**: the number of elements in _S_ 有限集的大小 

**Power set Ρ(S)：S的所有子集**

<img src="../images/1680431044245-d8c4a998-ae7d-4b5f-a660-8b7b95ae99b5.png" alt="image.png" style="zoom:50%;" /><img src="../images//1680431069800-3ea298b3-5254-4441-9e47-eae1334e582d.png" alt="image.png" style="zoom:50%;" />

<img src="../images/image-20240412081951612.png" alt="image-20240412081951612" style="zoom:30%;" /><img src="../images/image-20240412082029980.png" alt="image-20240412082029980" style="zoom:33%;" /><img src="../images/image-20240412082102865.png" alt="image-20240412082102865" style="zoom:33%;" />正确

<img src="../images/1680431283158-797bd060-a567-4eb8-b33a-8459a4cc6efd.png" alt="image.png" style="zoom:50%;" />

##### Example 1
What is the _**Cartesian product **_**笛卡尔积** of _A = {1_, _2} and B = {_a, b, c_}? <br />_Solution: _The Cartesian product  A × B  is <br />	A × B = {(1_, a_)_, _(1_, b_)_, _(1_, c_)_, _(2_, a_)_, _(2_, b_)_, _(2_, c_)}. <br />But the Cartesian product B × A  is <br />	B × A = {(_a, _1)_, _(_a, _2)_, _(_b, _1)_, _(_b, _2)_, _(_c, _1)_, _(_c, _2)}. This is not equal to A × B._
##### Example 2
What is the Cartesian product _A × B × C_, where _A = {0_, _1}, B = {1_, _2}, and C = {0_, _1_, _2}? <br />_Solution: _The Cartesian product A × B × C consists of all ordered triples (_a, b, c_), where a ∈ A_, <br />_b ∈ B_, and _c ∈ C_. <br />Hence, _A × B × C = {(0_, _1_, _0)_, _(0_, _1_, _1)_, _(0_, _1_, _2)_, _(0_, _2_, _0)_, _(0_, _2_, _1)_, _(0_, _2_, _2)_, _(1_, _1_, _0)_, _(1_, _1_, _1)_, _(1_, _1_, _2)_, _(1_, _2_, _0)_, _(1_, _2_, _1)_, _(1_, _2, 2_ )}.

---

Note that when _A_, _B_, and _C are sets, (_A _× B_) × C is not the same as A × B × C <br /><img src="../images/1680785334093-f45ae0ba-31e6-4619-aeee-05fcfab40917.png" alt="image.png" style="zoom:50%;" />
##### Example 3
Suppose that _A = {1_, _2}. <br />It follows that A2 = {(1_, _1)_, _(1_, _2)_, _(2_, _1)_, _(2_, _2)} <br />and A3= {(1_, _1_, _1)_, _(1_, _1_, _2)_, _(1_, _2_, _1)_, _(1_, _2_, _2)_, _(2_, _1_, _1)_, _(2_, _1_, _2)_, _(2_, _2_, _1)_, _(2_, _2_, 2)}.
### 2.2 Set Operations
容斥原理：|A ∪ B| = |A| + |B| − |A ∩ B| 

**Union**： A∪B
**Intersection**： A∩B
**Complement**： U-A

**Difference**：<img src="../images/1710950006586-e6cb4da1-3f59-4a4c-a6ae-9db8dffc8a27.png" alt="image.png" style="zoom:33%;" />A非B的部分

**Symmetric**：<img src="../images/1710950339536-b38c8729-79b2-4986-a438-01272f717a72.png" alt="image.png" style="zoom:33%;" />A和B中不重合的部分

<img src="../images/1680432516920-25bcc003-7e0e-4dd4-bbbb-b78f1b5c0464.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680780567854-c6bfe3a0-9069-41bd-843d-1a85cf337f47.png" alt="image.png" style="zoom:50%;" />

##### Example

Use set builder notation and logical equivalences to establish the first De Morgan law A∩B=A∪B. 

Solution: We can prove this identity with the following steps. 

<img src="../images/1680780868792-051fc1d2-e768-4af8-a839-630f65aac233.png" alt="image.png" style="zoom: 67%;" />

_Let A_, _B_, and C be sets. Show that A∪(B ∩ C ) = (C∪B) ∩ A. <br /><img src="../images/1680781063022-681185de-147f-4742-bb96-f5a13d909b75.png" alt="image.png" style="zoom: 67%;" />



<img src="../images/1680781119835-50db8693-33a5-41da-adc3-8ac207badcf0.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680781151900-6934889e-82c7-4b42-82db-9e6822b85f51.png" alt="image.png" style="zoom:50%;" />



### 2.3 Functions

Functions are sometimes also called **mappings **or **transformations**.<br /><img src="../images/1680434068104-92dc7fb7-357b-4b56-8ef9-6b336f8c75ae.png" alt="image.png" style="zoom:50%;" />

domain定义域；codomain值域

<img src="../images/1680434198310-5fc36c23-8c77-4115-b0ad-b1130803d7e1.png" alt="image.png" style="zoom:50%;" /><br /><img src="../images/1680781943617-8a6a128d-8406-42bd-87af-a3e68e8cd77a.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680434272330-fee41932-7eaf-4952-bda0-b1bd37acad89.png" alt="image.png" style="zoom:50%;" /><br />即 ∀a∀b ( f (a)=f (b) → a=b<br />**单射 injection/one-to-one**：对X中任意两个不同的x1、x2，f(x1)不等于f(x2)，集合x的元素数 < 集合y<br /><img src="../images/1680434447812-80240f95-0bfd-4819-813c-821eee6c893e.png" alt="image.png" style="zoom:50%;" /><br />即 ∀y ∃x (f(x)=y)<br />**满射 surjective/onto**：Y中的任何一个元素都是X中某元素的像<br /><img src="../images/1680435138240-c92aa61a-a1ee-4891-aa84-c0a9800dabee.png" alt="一一对应" title="一一对应" style="zoom:50%;" /><br />**双射bijection**：既单又满

<img src="../images/1680435277554-268117d9-7674-45ea-a9c3-a5edc390144c.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680435255341-1052741d-4ddb-4d53-8bb2-b6ecfb7e12a6.png" alt="image.png" style="zoom:50%;" />

inverse function逆函数 f^-1^(b)=a iff f(a)=b

只有当f是双射时才有逆函数

arbitrary means 任意<br /><img src="../images/1680435420975-c12f6a8e-d4b1-4078-8269-1a177258955e.png" alt="image.png" style="zoom:50%;" /><br /><img src="../images//1680436988925-2a786527-e50a-41d7-aaee-9009e20a1bcd.png" alt="image.png" style="zoom:50%;" />

### 2.4 Sequences and Summations
<img src="../images//1680437481345-de53f1ea-4cfa-4630-ac86-241dcc49203e.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680437545920-6fea6d99-da32-45c6-b58f-bd4d34c417e6.png" alt="image.png" style="zoom:50%;" />

<br /><img src="../images/1680439435775-854c0f59-cdae-4dbd-b6d5-b90f935c2cf8.png" alt="image.png" style="zoom:50%;" />

### 2.5 Cardinality of Sets

集合的基数

#### 2.5.1 Introduction

实数集的基数>有理数
不是所有无限集的基数是一样的

The sets A and B have the **same cardinality** (denoted by | A |= | B |) iff there exists a **one-to-one correspondence** (bijection) from A to B. 基数相同，当且仅当有一一对应关系。

如果B是A的子集，则|B|≤|A|;

#### 2.5.2 Countable sets

**Countable sets** 可数集：A set that is either finite or has the same cardinality as the set of positive integers 和正整数集的基数相同的集合是可数的

Let the cardinality of a countably infinite set S be $\aleph$. 
We write |S|=$\aleph_0$ and say that S has cardinality "alepha null".​

An infinite set is countable if and only if it is possible to list the elements of the set in a sequence (indexed by the positive integers) 无限集可数，当且仅当可以用序列列出集合的元素

##### Example 1

<img src="../images//image-20240329151709993.png" alt="image-20240329151709993" style="zoom: 33%;" />

##### Example 2

- The Positive Rational Numbers are Countable

<img src="../images//image-20240329151905707.png" alt="image-20240329151905707" style="zoom:33%;" />

- The set of all rational numbers Q, positive and negative, is countable infinite. 所有有理数集是无限可数集
- The set of rational numbers and the set of natural numbers have same cardinality，namely |Q| = |N| 有理数集和自然数集基数相同



<img src="../images/1680439116950-de768897-29af-46bf-b5ad-42765286ec7d.png" alt="image.png" style="zoom:50%;" />

#### 2.5.3 Uncountable sets

【Theorem】The set of real numbers (between 0 and 1) is **uncountable**. 实数集不可数

cantor diagonalization argument 对角线论证<img src="../images/1680439407872-1889f8ba-e927-4b0f-bf55-206e70075aca.png" alt="image.png" style="zoom:50%;" />

##### (Un)Computable

A function is **computable** 可计算 if there is a computer program in some programming language that **finds the values of this function**. If a function is not computable we say it is uncomputable.

##### Continuum Hypothesis 连续性假设

<img src="../images//image-20240329155817902.png" alt="image-20240329155817902" style="zoom:33%;" />

- 任意集合其所有子集的基数大于原来集合的基数
- 正整数集的所有子集和实数集有相同的基数

<img src="../images//image-20240329161017556.png" alt="image-20240329161017556" style="zoom:33%;" />
不存在一个无穷集合，它的势比自然数集($\aleph_0$)的势大，比实数集（连续统）势小

The set of all functions from $\mathbb{N}$ to $\mathbb{N}$ is uncountably infinite, with a cardinality of ${2^{\aleph_0}}$, the same as the cardinality of the continuum

#### Conclusion

<img src="../images//image-20240329152632606.png" alt="image-20240329152632606" style="zoom:33%;" />

## 3 Algorithms

### 3.1 Algorithms
<img src="../images/1686912008190-22fefa4d-5b35-4ee3-84f7-b3eba35e7a3a.png" alt="image.png" style="zoom:50%;" />

Searching Algorithms; Sorting; String Matching; Greedy Algorithms

Properties of Algorithms: input, output, definiteness, correctness, finiteness, effectiveness, generality

### 3.2 The Growth of Functions
**f(x) is O(g(x)) **: the fact that |f(x)| ≤ C|g(x)| for all x > k for some constants C and k<br />**f(x) is 𝛀(g(x)) : **the fact that |f(x)| ≥ C|g(_x_)| for all x > k for some positive constants C and k <br />**f(x) is 𝚯(g(x)) :**the fact that f(x) is both _O(g(x)) and Ω(g(x)) 

#### Big-O 
$log(n!) = O(nlog n)$ <br /><img src="../images/1683089406642-e0870e98-3850-43fb-94d3-7cc0376d6ece.png" alt="image.png" style="zoom: 50%;" /><img src="../images/1686910853248-b53ceff7-e3e0-4ccf-91ba-7e73f4593382.png" alt="image.png" style="zoom:50%;" /><br /><img src="../images/1686910869741-fc4bde2e-0bf8-49c3-874f-f2e1563e4d4b.png" alt="image.png" style="zoom:50%;" /><br /><img src="../images/1686910883883-8071e0ad-862c-4d3d-b821-c4a93ceb4b87.png" alt="image.png" style="zoom:50%;" /><img src="../images/1686910898734-6b97adfc-5a63-4715-8908-06978a2da440.png" alt="image.png" style="zoom:50%;" /><img src="../images/1686911126219-e7342094-526d-4fb6-898e-d73f1e3419e5.png" alt="image.png" style="zoom:50%;" />
#### Big-Omega and Big-Theta Notation

$\omega$：增率的下界

<img src="../images/1686910945560-c078bea0-2e17-4e3e-b617-9528f57c5c89.png" alt="image.png" style="zoom:50%;" />

f(x) is $\Omega(g(x))$ if and only if g(x) is O(f(x))

<img src="../images/1686910956528-d279ab9d-708f-43d0-8aa2-4136fd1752d4.png" alt="image.png" style="zoom:50%;" /><img src="../images/1686910972067-5421d72e-be55-43eb-b8fe-681367a1f85a.png" alt="image.png" style="zoom:50%;" />![image.png](../images/1686911058025-3923e0c1-5cdb-489e-b1d5-280a1302de97.png)<img src="../images/1686911093145-f06e5da8-63d1-4193-9c5d-48d664ca1fba.png" alt="image.png" style="zoom:50%;" />

---

##### example

<img src="../images/1680834340807-4656f5a9-1af8-4f43-95f1-18d9217e2725.png" alt="image.png" style="zoom:50%;" />

### 3.3 Complexity of Algorithms

<img src="../images/1680569919356-a1778b69-efee-443e-a94c-2d651cf7c524.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680571162745-f96cd297-1699-4479-8f3d-9cb846dc5ba1.png" alt="image.png" style="zoom:50%;" /><img src="../images/1680571479827-91f205bb-9bad-4f05-86ef-ffe97dd3e23c.png" alt="image.png" style="zoom:50%;" />

## 4 Number Theory and Cryptography
### 4.1 Divisibility and Modular Arithmetic
![image.png](../images/1683089897607-02b86153-9dce-428a-8987-a4d8a1ffeb6b.png)

**a∣b： **a divides b = b/a, b是大的被除数  

![image.png](../images/1683091128174-74c5d8fc-0b12-4c88-8b1c-407fbe25a56f.png)

![image.png](../images/1683091158165-62c9fce6-3acd-4ba0-bb00-72da9ebddb54.png)

![image.png](../images/1683091438033-d1ea8ed5-c914-47ba-a544-8d2dcb682730.png)

![image.png](../images/1683091450309-03116018-fd71-4cfc-9834-3ac7deb99ea8.png)

**a div d**: a 整除d为q

![image.png](../images/1683092286939-fbee442e-26d8-4d79-b0ae-e2de4e239681.png)同余定理 congruence

【**定理四**】 **a ≡ b (mod m)，则a=b+km**<br />![image.png](../images/1683094500224-39d859d8-a7d2-41ab-88b0-d49308fac24e.png)

![image.png](../images/1683096048763-4648ed7a-a957-4709-9162-b5c083bfe69f.png)

<img src="../images/1683096153734-0d60cad8-e4d9-4fb8-a9f3-53a16b87c438.png" alt="image.png" style="zoom: 50%;" />

模m算术：满足

![image.png](../images/1683096253201-e61b7405-c085-4dfe-a58c-7852970371b9.png)

### 4.2 Integer Representations and Algorithms
![image.png](../images/1683111653036-64886174-775d-4a73-9369-4683fb860c44.png)<br />n的b进制展开式<br />![image.png](../images/1683274493291-7bc141e9-a7ba-4b46-9b37-923e4e184fb3.png)
### 4.3 Primes and Greatest Common Divisors
**relatively prime互素**<br />**prime 素数**<br />**composite 合数**<br />**Mersenne prime 梅森素数: **a prime of the form 2p _− 1, where p is prime<br />**Trial Division 试除法**<br />![image.png](../images/1683278222524-c3baa742-9542-4702-8756-bacf7a71061f.png)

**The Sieve of Eratosthenes 埃拉托斯特尼筛法**

100内筛2、3、5、7整除的数<br />![image.png](../images/1683278927422-44075328-d99f-4a4e-a82c-f2f223722bf7.png)![image.png](../images/1683279269523-72382d7c-0d4c-4715-9f5d-98434a5a1cc1.png)

欧几里得定理：素数的无穷性
梅森素数 mersenne primes

【Prime number theorem 素数定理】：随机选取一个小于n的正整数是素数的概率为$\frac{1}{lnn}$

**gcd**(Greatest common divisor)：最大公约数

![image.png](../images/1683279350249-28242087-3c69-4fa7-bc37-30b5604a952c.png)

**lcm**(least common divisor)：最小公倍数

![image.png](../images/1683279385035-b4451418-8b68-4010-a714-6084ab6473be.png)

![image.png](../images/1683279666429-4abcf328-3145-47f8-8a43-21284c269947.png)

#### The Euclidean Algorithm 欧几里得算法

**贝祖定理**

![image.png](../images/1683279970055-eb01a711-7ae0-4f6c-b5be-a5269f88975f.png)

**Bezout coefficients of a and b: **sa + tb = gcd(a, b)

![image.png](../images/1683280988793-a873f9f3-12b3-4c60-8b7f-667aad080e3e.png)![image.png](../images/1683280477061-5b168edb-c59d-4068-92f3-4297b145f104.png)![image.png](../images/1683280903008-419dfad0-6437-411b-a4d3-d20578ff4969.png)**a ≡ b (mod m)** (a is congruent to b modulo m): a − b is divisible by m，即a-b能被m整除

##### Example

![image.png](../images/1683279885612-2ad3116d-445b-442a-8980-c5d229f6fbed.png)

### 4.4 Solving Congruences 求解同余方程
**sa **+ **tm **= 1 (mod m) → s是a mod m的逆，满足 sa≡1(mod m)

1. 用欧几里得算法算模的逆s
2. 左右两边同 ✖s
3. 等式右边即为x的解

![image.png](../images/1683282304561-a7e5f162-4ca6-4be1-a1d2-4e9207981237.png)

<img src="../images/image-20240504155256757.png" alt="image-20240504155256757" style="zoom:50%;" />

该解法a，m要求互素，即gcd(a,m)=1

#### Chinese remainder theorem 中国剩余定理

<img src="../images/1683282748408-951eaf10-267a-425b-866b-368a11099e40.png" alt="image.png" style="zoom:60%;" /><br />其中<img src="../images/1683283320100-2e1a22ca-3138-4acf-896a-1e975069f5ed.png" alt="image.png" style="zoom:67%;" />, <img src="../images/1683283337649-a4824cf5-4e39-4a2c-9d9c-ae411a8b0ba5.png" alt="image.png" style="zoom:67%;" />= 一个数(mod m)<br /><img src="../images/1683283380852-ed1bed0f-78b2-40e1-96b0-c850cbd59638.png" alt="image.png" style="zoom: 67%;" /><img src="../images/1683283401830-571798a9-6ff6-4e6a-b6a5-b16ff21afcec.png" alt="image.png" style="zoom:60%;" /><br />**Back substitution 反向替换 → 翻译成一个同余式**

同余方程重写为

<img src="../images/1683285941039-86f305ed-3fd4-43ff-981c-8231be73d10e.png" alt="image.png" style="zoom: 67%;" />

**pseudo prime to the base  b** 以b为基底的伪素数: a composite integer  n such that  $bn−1 ≡ 1 (\mod n)$ 

---

#### Fermat's little theorem 费马小定理

<img src="../images/1683285884113-73af85e1-cc47-4ef1-ab7d-a85696b05a76.png" alt="image.png" style="zoom: 50%;" /><br /><img src="../images/1683289312305-0230a955-5e9f-4ff7-bcfe-da6c6b057108.png" alt="image.png" style="zoom:50%;" /><br /><img src="../images/1683290223687-06967f9e-061b-42f2-839e-324a7a0e7b84.png" alt="image.png" style="zoom:67%;" />

**Carmichael 卡米切尔数**<img src="../images/1683341076481-85bd2c44-19c6-4a80-bb76-4819eb2414b0.png" alt="image.png" style="zoom: 50%;" />

## 5 Induction and Recursion
### 5.1 Mathematical Induction
**Mathematical Induction 数学归纳法**

(P(1)∧∀k(P(k)→P(k+1)))→∀n P(n)

<img src="../images/1683344448037-87deb769-5814-410a-b760-0705c84bf373.png" alt="image.png" style="zoom:67%;" /><br />**inductive hypothesis 归纳假设**<br /><img src="../images/1683345264018-808d6bbc-3d3d-43c9-8d77-f7e542d88cac.png" alt="image.png" style="zoom:67%;" /><img src="../images/1683346615888-58384556-66e1-4726-a622-6c5cb2289449.png" alt="image.png" style="zoom:67%;" />

### 5.2 Strong Induction and Well-Ordering 
**强归纳法（第二归纳法）和良序性**

(P($n_0$)∧∀k(k>=$n_0$∧P($n_0$)∧P($n_0$+1)∧···∧P(k)→P(k+1)))→∀n P(n)

<img src="../images/1683350021250-d1f486ab-6317-416f-956a-b52354e4d04e.png" alt="image.png" style="zoom: 67%;" />

良序性：Every *nonempty* set of *nonnegative* integers has the smallest element.
每个非空的自然数集都有最小的元素。

<img src="../images/image-20240419132551342.png" alt="image-20240419132551342" style="zoom:50%;" />

<img src="../images/1683350052807-a167d26a-4dd3-4f77-a156-58995fe9b444.png" alt="image.png" style="zoom:67%;" />

![image.png](../images/1683350320451-8700f07e-68a2-4547-bdfe-6db555017d4a.png)

数学归纳法和第二数学归纳法的有效性来自良序性原理。
实际上，数学归纳法、第二数学归纳法和良序性是等价的原理

### 5.3 Recursive Definitions and Structural Induction
**递归定义和结构归纳法**<br /><img src="../images/1683356282183-ff44a797-fafd-4b0f-90ba-ca536d381606.png" alt="image.png" style="zoom:67%;" />

记$f_n=n!$

<img src="../images/1683357282208-d6a6f888-ba1b-42e2-94dd-d0a65bce9973.png" alt="image.png" style="zoom:67%;" />

LAME'S Theorem

![image.png](../images/1683356297768-ed6c74fe-df0f-40f7-8309-2b763c37e920.png)![image.png](../images/1683356319921-cc093dac-e7a3-4c5b-b4b8-fb75d5a2209b.png)![image.png](../images/1683356771817-d3dad888-5be7-46ce-86ae-12a7b6651673.png)

**Well-formed formulae** for compound proposition:

The set of well-formed formulae in propositional logic involving T, F, propositional variables, and operators from the set {¬,∧,∨,→,↔}.
![image-20240621164900429](../images/image-20240621164900429.png)

<img src="../images/1683383323929-86e9430c-c752-45c6-9e1b-9ce45e38ed63.png" alt="image.png" style="zoom:67%;" /><img src="../images/1683383344132-c66ddd5f-b64f-4a70-8ff5-9b84cca5903d.png" alt="image.png" style="zoom:60%;" />

**Structural Induction 结构归纳**

![image.png](../images/1683384731456-d82ad01b-38e6-423d-99c1-e918956ee3d7.png)<br /><img src="../images/1683384745659-4e9e0fae-8f0b-4070-b678-e1f0f87d9f0b.png" alt="image.png" style="zoom:50%;" /><img src="../images/1683384939710-6ebf47fc-9827-419c-bb1e-1d93e07473f6.png" alt="image.png" style="zoom:67%;" /><br /><img src="../images/1683384993302-61ed4916-2f38-4151-b8d1-d9197c078dd6.png" alt="image.png" style="zoom:67%;" />![image.png](../images/1683385014577-265de3ad-f93c-4cd4-b86b-0cc4878b388c.png)![image.png](../images/1683385025876-b2b9347b-a39c-4199-be53-c0df20e380b0.png)<img src="../images/1683385211423-ed590858-4bda-47b3-ac45-6ad85ec62fb3.png" alt="image.png" style="zoom:67%;" />

**Generalized Induction 广义归纳法**

Generalized induction is used to prove results about **sets other than the integers** that have the **well-ordering property**.

![image.png](../images/1683385371105-7d245b6a-0412-410f-9467-b0f834afaf86.png)

**lexicographic ordering 字典序**

### 5.4 Recursive Algorithms
**递归算法**<br /><img src="../images/1683386095729-f9663592-0a0c-4cf3-9fe6-ea13d37a4168.png" alt="image.png" style="zoom:67%;" /><img src="../images/1683386058052-3ddd0499-bbe8-47e5-8a0e-6eb79534d1bf.png" alt="image.png" style="zoom:50%;" />

**geometric progression:几何数列（等比）**

**arithmetic progression:等差**

## 6 Counting
### 6.1 The Basics of Counting
<img src="../images/1683431306094-3b6e7064-9489-4833-b3c5-56153226f8a7.png" alt="image.png" style="zoom:67%;" />乘积原则

根据乘法原则，从m个元素的集合映射到n个元素的集合有n^m^个不同的函数；有n(n-1)……(n-m+1)个不同的单射函数（m≤n）；有
$$
n^m-C_n^1(n-1)^m+C_n^2(n-2)^m-...+(-1)^{n-1}C_n^{n-1}*1^m
$$
个不同的满射函数（n≤m）[详见8.6](#8.6 Applications of Inclusion–Exclusion)

<img src="../images/1683432132940-e37fc9db-eec3-40df-8d61-21aae0a94aff.png" alt="image.png" style="zoom:67%;" />

求和原则

<img src="../images/1683433433514-726851e0-bbc3-4bd9-be44-51cee83a6fa5.png" alt="image.png" style="zoom:67%;" />

The subtraction rule is also known as the **principle of inclusion–exclusion**

减法原则又称容斥原理

<img src="../images/1683434049030-b197c6df-a321-4b34-b8b6-3a55d01e2b37.png" alt="image.png" style="zoom:67%;" />

除法原则

<img src="../images/1683434070809-a0e8e0ad-4f8e-4ab8-a08a-9f5aa01c4646.png" alt="image.png" style="zoom:60%;" />

### 6.2 The Pigeonhole Principle
鸽巢/洞原理

![image.png](../images/1683434543824-e040bc49-5da6-4de2-9dea-9aafd49a6df9.png)

![image.png](../images/1683434713702-534d50a5-ef57-4183-996b-e488c0c78e76.png)

广义鸽洞原理：把N个物品放到k个箱子中，至少有一个箱子中包含至少$⌈N/k⌉$ 个物品（向上取整）

<img src="../images/1683435216848-54952471-38cd-4bf2-a09c-f1ca896d16fd.png" alt="image.png" style="zoom:60%;" />

<img src="../images/1683435252465-45ce35d4-6cc2-4341-a6aa-8654dc3167a6.png" alt="image.png" style="zoom:50%;" />![image.png](../images/1683435269162-8b59b243-1fc0-4a1e-92fb-5dc1c51c14c0.png)![image.png](../images/1683441412237-b44e6750-9e5a-491d-9372-8a297c47b286.png)

Example

在6个人的群体中，每两个人不是朋友就是敌人，那么有3个共同的朋友或者敌人

### 6.3 Permutations and Combinations
排序与组合<br />![image.png](../images/1683442789467-5dfbd124-bbb9-429a-af4e-86eab4014525.png)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/34417153/1683442828015-9f533ce5-0dc3-4927-bf79-616c886de7d6.png#averageHue=%23c7eef1&clientId=uef27861d-e585-4&from=paste&height=61&id=u61fa8d0f&originHeight=122&originWidth=1471&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=22391&status=done&style=none&taskId=u36f94624-ba18-4479-8a3c-8406aea2341&title=&width=736)![image.png](../images/1683442850905-f1797393-9696-4398-b158-42cb900c2254.png)

组合数$C(n,r)=C(n,n-r)$证明：重复计数方法或者双射方法

<img src="../images/1683443720173-695cd843-2f28-4100-8f7d-1b9b8e764dc2.png" alt="image.png" style="zoom:50%;" /><img src="../images/1683443703584-4a6877db-a7d4-4ffe-85e9-b022828ba9ae.png" alt="image.png" style="zoom:67%;" />

### 6.4 Binomial Coefficients
![image.png](../images/1683443767343-e1ecff18-153c-4362-a6d5-f99fd4d7c0e5.png)

**二项式定理**

![image.png](../images/1683444428161-b9f5c10f-5704-4aea-b9fc-05d8bc79715e.png)![image.png](../images/1683444531366-019e685a-242d-4ac5-a9c6-934443755b21.png)![image.png](../images/1683444563030-92396387-939a-43f2-8cf0-79427fa5f0cd.png)<br />**帕斯卡恒等式 pascal's identity**<br /><img src="../images/1683444710353-fe569caa-1dce-4370-9bdf-7391001a29d7.png" alt="image.png" style="zoom:67%;" /><br /><img src="../images/1683444879792-4b7e2860-741e-4a8e-9ba2-6e89599a90c9.png" alt="image.png" style="zoom:60%;" /><br /><img src="../images/1683444897691-8b685640-21dc-4733-ac61-38488cb95484.png" alt="image.png" style="zoom:60%;" />

**Vandermonde's Identity 范德蒙德恒等式**

<img src="../images/1683445001814-cd30c096-0fd8-41e1-b708-fd7bca5c0cb3.png" alt="image.png" style="zoom:60%;" />

<img src="../images/1683445071850-dbc52887-4ba4-4963-9624-0d436e5922ea.png" alt="image.png" style="zoom: 50%;" /><br /><img src="../images/1683445597419-ae629698-8976-4e16-8930-4e24a7be256f.png" alt="image.png" style="zoom:67%;" />

![image-20240513212738161](../images/image-20240513212738161.png)

证明：长度为n+1的位串里有r+1个1，最后一个1在第k位。那么前k-1位必须有r个1，即有C(k-1, r)种情况，同时对于最后一个1，k最小为r+1，最大为n+1，则把所有情况相加，<img src="../images/image-20240513213053004.png" alt="image-20240513213053004" style="zoom:25%;" />=左边

### 6.5 Generalized Permutations and Combinations

**permutation 排列**<br />![image.png](../images/1683450810367-91782734-a9ee-4f18-bdca-8acc1d6af62b.png)![image.png](../images/1683450822804-4e5fa3c3-263a-4510-96d6-14405603c3dc.png)

**Combination with repetition** n个元素集合中允许重复的r组合个数: $H_n^r=C_{n-1+r}^r=C_{n-1+r}^{n-1}$

<img src="../images/1683451060334-f09cb542-215a-4691-8fde-0f90a8195d54.png" alt="image.png" style="zoom:50%;" />

<img src="../images/image-20240513214312904.png" alt="image-20240513214312904" style="zoom: 33%;" />

1. **Distinguishable objects and distinguishable boxes**不同物品不同箱子

![image.png](../images/1683451280063-59ccf9f6-e90f-4f8d-909c-146d05112a26.png)

2. **Indistinguishable objects and distinguishable boxes**相同物品不同箱子

<img src="../images/1683452577849-014d984e-b1b6-48f9-9d4f-411875078880.png" alt="image.png" style="zoom:50%;" /><img src="../images/1683452591697-3745bb9c-829b-495b-ac95-d827043f1318.png" alt="image.png" style="zoom:50%;" />

3. **Distinguishable objects and indistinguishable boxes**不同物品相同箱子

<img src="../images/1683452792250-3c288428-7bd5-4d2b-96a1-7f897feede5e.png" alt="image.png" style="zoom:50%;" />：将n个不同的物品放进k个相同的箱子

$S(n,j)j!$​：将n个不同的物品放进j个相同的箱子（没有箱子是空的）

<img src="../images/image-20240504132545683.png" alt="image-20240504132545683" style="zoom: 33%;" />

![image-20240621194124965](../images/image-20240621194124965.png)

4. **Indistinguishable objects and indistinguishable boxes**相同物品相同箱子

   没有公式，手算

   Eg, 6本相同的书放到4个相同的盒子中，有{6}, {5,1}, {4,2}, {4,1,1}, {3,3}, {3,2,1}, {3,1,1,1}, {2,2,2}, {2,2,1,1}，共9种情况

## 8 Advanced Counting Techniques
### 8.1 Applications of Recurrence Relations
递推关系<br /><img src="../images/1683453702234-4eaeaae6-1e19-4daa-ad48-c9b98719c164.png" alt="image.png" style="zoom: 50%;" /><img src="../images/1683454046497-bc7f58aa-8181-42b9-a03b-f7188dd62d42.png" alt="image.png" style="zoom: 50%;" /><img src="../images/1683454833269-92d6f32c-603c-43f3-86f0-14bb734800d1.png" alt="image.png" style="zoom:67%;" /><br /><img src="../images/1683454774798-760a4df6-f0bc-4300-9868-c72d39a0b6ff.png" alt="image.png" style="zoom: 50%;" />
### 8.2 Solving Linear Recurrence Relations
求解线性递推关系

<img src="../images/1683456033593-7b4212be-27f9-41d0-a3d7-e5962c7f28e0.png" alt="image.png" style="zoom: 50%;" /><img src="../images/1683456142563-a6493322-40fe-49f1-bc94-5303e8e93311.png" alt="image.png" style="zoom:50%;" /><img src="../images/1683456155293-2913a008-8a7a-4c58-a7c0-258720d06bad.png" alt="image.png" style="zoom: 50%;" />

Fibonacci numbers:<img src="../images/1683456294197-0fd568ec-0ac7-4765-a2e0-a8135c675a8e.png" alt="image.png" style="zoom:50%;" />

**linear线性**：右边是$a_k$*c之和+F(n)

**homogeneous同类**：都是形如$s_j*s$的项

 **constant coefficients常系数**：对每个$a_k$​前的系数都是常数

**degree k**：左边$a_n$，右边最多追溯到前k项即$a_{n-k}$

<img src="../images/image-20240428134949103.png" alt="image-20240428134949103" style="zoom: 33%;" />

<img src="../images/1683456398171-15b70dfa-003e-4d10-9a48-fe70a90a8cf4.png" alt="image.png" style="zoom:50%;" /><br /><img src="../images/1683456383610-486e3ff4-a63c-4d95-b191-bb75307a8eb8.png" alt="image.png" style="zoom:67%;" /><br /><img src="https://cdn.nlark.com/yuque/0/2023/png/34417153/1683456518705-6006fa8a-403b-4806-a9bc-598a6d888d51.png#averageHue=%23cacaca&clientId=uef27861d-e585-4&from=paste&height=254&id=uc3a74bab&originHeight=381&originWidth=1447&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=618304&status=done&style=none&taskId=u8635da36-ccb4-4d15-9b88-0075af37c24&title=&width=964.6666666666666" alt="image.png" style="zoom:50%;" /><img src="../images/1683456754958-8900d3db-4e08-4d60-8eeb-75fd187a8d86.png" alt="image.png" style="zoom:50%;" /><br /><img src="../images/1683457265813-aecb3059-9b47-4143-a065-b90f0aa04105.png" alt="image.png" style="zoom: 50%;" />

<img src="../images/1683456720602-845128b9-8f7f-4ffa-9dee-bbab0a7204ff.png" alt="image.png" style="zoom: 50%;" />

<img src="https://cdn.nlark.com/yuque/0/2023/png/34417153/1683456794217-a5b04f1c-a550-4d27-9ee9-e1e50b1cbbe4.png#averageHue=%23c6c6c6&clientId=uef27861d-e585-4&from=paste&height=144&id=u0955efe6&originHeight=287&originWidth=1455&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=464801&status=done&style=none&taskId=u7f51476d-bf94-4e98-9c44-55332e007ea&title=&width=728" alt="image.png" style="zoom:50%;" /><img src="../images/1683457182726-bcc6c328-bc09-44d1-8cc5-9fddb1b452ef.png" alt="image.png" style="zoom: 50%;" /><img src="../images/1683457158018-2702526c-f1e1-4fc5-a400-7d35b1199bca.png" alt="image.png" style="zoom:50%;" />

定理6是特解的形式，和F(n)有关

<img src="../images/image-20240428132658089.png" alt="image-20240428132658089" style="zoom: 50%;" />

![image-20240622161009737](../images/image-20240622161009737.png)

最后$a_n$要把通解$a_n^{(h)}$和特解$a_n^{(p)}$相加

### 8.4 Generating Functions

生成函数

<img src="../images/1683458904842-5c8250dc-2e65-44a7-8f16-92844981f63e.png" alt="image.png" style="zoom: 50%;" /><img src="../images/1683460256567-1e4109a4-2ef1-411c-9143-11a9e672a374.png" alt="image.png" style="zoom:50%;" />

#### Extended Binomial Theorem 拓展二项式系数

<img src="../images/1683460273097-f827eb07-416c-4f39-90e8-730e47bada2e.png" alt="image.png" style="zoom:50%;" /><img src="../images/1683460515691-1533987e-2845-41d9-aa77-ba36b7fbeb22.png" alt="image.png" style="zoom: 67%;" /><img src="../images/1683857338104-1f77331b-f179-47eb-a163-8895f171b7df.png" alt="image.png" style="zoom: 33%;" />

利用公式<img src="../images/image-20240426084952319.png" alt="image-20240426084952319" style="zoom:40%;" />，其中$a_k=1$

<img src="../images/1683857418541-2f1280f6-830a-4e17-86eb-694e613f9a45.png" alt="image.png" style="zoom: 40%;" />

利用公式<img src="../images/image-20240426085214998.png" alt="image-20240426085214998" style="zoom:33%;" />，其中$c_k$全为1的生成函数为$\frac{1}{1-x}$

<img src="../images/image-20240426085404826.png" alt="image-20240426085404826" style="zoom: 33%;" /><img src="../images/image-20240426085657078.png" alt="image-20240426085657078" style="zoom: 33%;" />

#### Solve Recurrence Relations

<img src="../images/1683467868855-f4193700-23f8-4660-bbb8-59746796000d.png" alt="image.png" style="zoom:50%;" /><img src="../images/1683467889330-6abc29d7-ff2a-4901-8fc3-6150bdc4f60d.png" alt="image.png" style="zoom:50%;" />

<img src="../images/1683468321326-e458a1f3-7568-430a-8eb8-fa1f9af02b94.png" alt="image.png" style="zoom:50%;" /><img src="../images/1683468347985-6be67f29-d286-4d6e-a02a-17ea729ff8d4.png" alt="image.png" style="zoom: 50%;" /><img src="../images/1683468368673-b30e80c5-3194-4b12-a29c-c68e5b1d9955.png" alt="image.png" style="zoom: 50%;" />

[9.6: Using generating functions to solve recurrences - Mathematics LibreTexts](https://math.libretexts.org/Bookshelves/Combinatorics_and_Discrete_Mathematics/Applied_Combinatorics_(Keller_and_Trotter)/09%3A_Recurrence_Equations/9.06%3A_Using_generating_functions_to_solve_recurrences)这个写的更易于理解

#### Counting Problems

$$
G(x)=(1+x+x^2+x^3+...)^n=\frac{1}{(1-x)^n}
$$

<img src="../images/1683466184195-76be55a6-34ce-482f-8c57-b81a20c0e7b1.png" alt="image.png" style="zoom:50%;" />

#### Example

![image-20240622174658402](../images/image-20240622174658402.png)

### 8.5 Inclusion–Exclusion

**容斥原理**

<img src="../images/1683590740048-103f6ee0-f17e-4afc-9a03-29b2dd25a96f.png" alt="image.png" style="zoom: 50%;" />向下取整

<img src="../images/1683590826170-df9f0213-06f0-4b91-9423-015da236e1ba.png" alt="image.png" style="zoom: 50%;" />

### 8.6 Applications of Inclusion–Exclusion
<img src="../images/1683591388916-eda67e9c-5eb6-4ad0-b37b-190770059756.png" alt="image.png" style="zoom: 50%;" />

<img src="../images/1683591353297-3943544f-ee2a-4408-8ba7-b265a447856a.png" alt="image.png" style="zoom:50%;" />

m个东西分配给n个人，每个人至少有一件东西的方法总数：

![image.png](../images/1683591552002-7f759f72-0241-429d-a9f5-1f8c22e25b5b.png)

即映上函数onto/surgective function m →n（每个y至少有一个x与之对应）

**derangement 错排**

![image.png](../images/1683591797736-35d32cba-8d37-4d2d-a84a-553c2a0fa4be.png)

即 $≈ n!/e$最接近的整数

## 9 Relations

### 9.1 Relations and Their Properties
![image.png](../images/1683787250444-0c367ab2-596f-449e-ba11-504852bc1b6c.png)**binary relation from A to B **二元关系 ![image.png](../images/1684462904076-5ca47366-66e5-478e-b1e0-1bc70b590afa.png)![image.png](../images/1684463115762-10b96df1-ae61-4860-b896-7d3143896f5b.png)

- 二元关系是一个集合， R包含于A✖B
- n元关系就是A1✖A2✖···✖An的子集

![image.png](../images/1684463243674-eb51922f-b7d4-430e-9c23-bd0e457d79c1.png)

#### Properties of binary relations

**reflexive **自反性

![image.png](../images/1684463574066-f477a0d8-f602-479a-9076-63aed2f7ec54.png)

自反关系：矩阵主对角线都是1；有向图每个顶点都有环

**irreflexive **反自反性

反自反关系：矩阵主对角线都是0；存在既不是自反也不是反自反的关系

**symmetric & antisymmetric **对称性和反对称性

![image.png](../images/1684463630296-a4967f0a-9c9b-4990-a88d-ba1bfd417d97.png)

对称性：矩阵主对角线为对称轴

反对称性，主对角线随意，以主对角线为轴的一边如果是1，另一边必须是0

对称性和反对称性不是互斥的

**transitive **传递性![image.png](../images/1684464581017-83bfb5ca-1f9c-4697-9776-8e8158ad9859.png)![image.png](../images/1684495248536-474f9e6a-4a84-4926-815c-15c5cc53ce58.png)

<img src="../images/image-20240612150943842.png" alt="image-20240612150943842" style="zoom:33%;" />

R的n次幂

![image.png](../images/1684495223416-8ee29e80-969e-4279-970b-18b7c112dc3f.png)

![image.png](../images/1684502153754-ee048ac0-15d0-4195-9ca2-b55da4752af3.png)![image.png](../images/1684502128822-70fc36bb-8355-4a73-be78-dda42e84f573.png)![image.png](../images/1684502421496-cd0632f6-32e4-4dfa-8590-b59fdfb7deb9.png)![image.png](../images/1684502404403-b509d17e-33d8-4909-875a-39dcaf744d2a.png)

对于n个元素的集合，以下关系有多少种？

| reflexive 自反 | irreflexive 反自反 | symmetric and reflexive 对称+自反 |
| -------------- | ------------------ | --------------------------------- |
| $2^{n^2-n}$    | $2^{n^2-n}$        | $$ 2^{n(n-1)/2}$$                 |

| symmetric 对称                                  | antisymmetric 反对称       | asymmetric 非对称 |
| ----------------------------------------------- | -------------------------- | ----------------- |
| $2^n✖2^{\frac{n^2-n}{2}}= 2^{\frac{n(n+1)}{2}}$ | $2^n*3^{\frac{n(n-1)}{2}}$ | $3^{C(n, 2)}$     |

$$
C(n, 2)=n(n-1)/2
$$

![image.png](../images/1684464914179-410f7eda-a6e1-4e72-890e-0ec1592cecbe.png)

- n个元素的集合A上共有$2^{n^2}$​种二元关系

#### Example

正整数的整除关系是：reflexive, symmetric, transitive

从m个元素的集合到n个元素的集合的不同关系有$2^{mn}$个


### 9.3 Representing Relations
![image.png](../images/1684683924335-29350013-6226-48a1-93f9-763c381b6205.png)![image.png](https://cdn.nlark.com/yuque/0/2023/png/34417153/1684683957236-159a496d-5705-454f-a53c-5f5d14699ff2.png#averageHue=%23f6f6f6&clientId=ue0b39bfd-c88d-4&from=paste&height=161&id=u78124a74&originHeight=321&originWidth=1328&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=129124&status=done&style=none&taskId=u13ba0d3c-7ea3-41d5-b324-fd9aa274349&title=&width=664)<img src="../images/1684684225835-bd83a735-26f3-48bb-8596-d3560e26e15d.png" alt="image.png" style="zoom:40%;" /><img src="../images/1684684240684-19a5914d-c9ce-42d3-8e5d-09e8b7c0402e.png" alt="image.png" style="zoom:40%;" /><img src="../images/1684684286658-1df8f108-5aad-4a3b-9e9c-9cc767814634.png" alt="image.png" style="zoom:50%;" />

![image.png](../images/1685180708560-657b7250-eb62-46f1-9ae9-d9f2a92757a1.png)![image.png](../images/1685181034541-fc6ac8b0-a96e-45df-a0f0-037fd1ad6e87.png)

#### Combining relations

$R^{-1}$：R的逆，$R^{−1}=$​{(y,x)∣(x,y)∈R}

<img src="../images/image-20240612153224858.png" alt="image-20240612153224858" style="zoom:50%;" />

A⨀B，两个矩阵的布尔乘积<img src="../images/image-20240510145136465.png" alt="image-20240510145136465" style="zoom: 33%;" />

<img src="../images/image-20240510145050746.png" alt="image-20240510145050746" style="zoom:40%;" />

A⨁B：异或，不一样就出1

$M_{S∘R}= M_R ·M_S = M_R ⨀M_S$

$R^{n+1}=R^n∘R$​​ ——关系R的幂集

<img src="../images/image-20240612152327827.png" alt="image-20240612152327827" style="zoom: 33%;" />

- S∘R≠R∘S

[【集合论】关系幂运算 ( 关系幂运算 | 关系幂运算示例 | 关系幂运算性质 )_关系的幂运算-CSDN博客](https://blog.csdn.net/shulianghan/article/details/108956605)

![image.png](../images/1685193390373-0cbe1791-ed83-4914-abed-9c7324d717b4.png)![image.png](../images/1685193428049-800de16f-cba0-4288-993d-b4ed1f66c59e.png)<br />![image.png](../images/1685193702815-21ec6b5b-1a73-4ffc-b0d0-27b95a10a239.png)

### 9.4 Closures of Relations
![image.png](../images/1685193836328-b3e40e0b-e10b-4a27-a214-d66117db416d.png)![image.png](../images/1685193855861-654e4201-ae7e-47f3-8b99-ef9f92804200.png)

![image.png](../images/1685194132186-35829b3b-acc3-424a-8ed0-c11fbce87382.png)![image.png](../images/1685194148570-230800f6-9065-4bbf-b976-5fdf496b2901.png)

**Reflective Closures 自反闭包** $r(R)$​

【 Corollary 】$R = R ∩ I_A$  ⇔ R is a reflexive relation 

<img src="../images/1685194169967-3899233d-769c-4965-a0c3-39b6e6e05b80.png" alt="image.png" style="zoom:50%;" />![image.png](../images/1685194194181-a6231d6e-14a0-4c0b-b9d7-d5d91ede10b5.png)

**Symmetric Closures** 对称闭包 $s(R)$​

【 Corollary 】$R = R ∪ R^{-1}$​ ⇔ R is a symmetric relation 

![image.png](../images/1685193761622-bea750aa-7cd3-4adb-aa88-eb0d8d5b3aaf.png)

**Transitive Closures** 传递闭包 

![image.png](../images/1685194250693-e81133be-e452-4c8c-9878-c0c12ab79b40.png)<br />![image.png](../images/1685194309933-1c2fa53c-1c89-4b45-bce4-94a9b64c93dd.png)<br />![image.png](../images/1686650308808-ed311fce-af71-47b3-84df-13462419d3a3.png)![image.png](../images/1686650334062-e07e0d78-0ecd-42cb-9c1e-fc0cd30fa917.png)

**R^∗^ (connectivity relation 连通性关系)**: the relation consisting of those ordered pairs (_a, b_) such that there is a path from _a to b_

![image.png](../images/1686650406530-b44cf10c-a77d-44a9-8f45-551020517ddc.png)

**传递闭包等于连通性关系**  t(R)=R^*^![image.png](../images/1686651949385-f4aa5682-7d86-49a2-94fe-724de2fa853d.png)<br />![image.png](../images/1686651935443-474dadcd-b378-4318-8a40-58b10d94fb77.png)

![image-20240612183342537](../images/image-20240612183342537.png)

传递闭包的0-1矩阵（矩阵并

![image.png](../images/1686651964848-c07555af-7eb4-47fe-9eac-29b93026f7ce.png)

![image.png](../images/1686651994343-4894d620-89e5-41b2-ad1f-b7c77d7aee8d.png)![image.png](../images/1686651982081-6b3c15f8-469c-4096-b142-cf80c99bf0fc.png)![image.png](../images/1686652125567-efd682c6-a328-4177-a3b9-d8ad234cf70b.png)![image.png](../images/1686652188371-6348306e-fd54-47e2-9821-731635eb3603.png)

#### Warshall's algorithm 沃舍尔算法

use the concept of the **interior vertices **of a path  用到了一条路径内部顶点的概念

内部顶点：一条路径去掉起点和终点，如acdafbj的内部顶点cdafb

<img src="../images/1686799325622-e8f1113f-0236-45cb-9aa5-6bf5fbfe590b.png" alt="image.png" style="zoom: 50%;" /><img src="../images/1686799349750-ddba2965-1c9b-4d88-bbdc-0384c8c135ef.png" alt="image.png" style="zoom: 40%;" /><矩阵中$$a_{ij}={0,1}$$表示有从i到j的路径

![image.png](../images/1686799612588-7306a6d7-fc30-4ba2-af08-c11b15904bf4.png)<br />![image.png](../images/1686805395164-be53b6c7-4eb6-45a1-a8d2-63b33f0d5059.png)![image.png](../images/1686805540833-45835268-d627-4936-9efe-a890f63e480d.png)

k确定的情况下，原先矩阵是1的还是1，只要检查第k列是1的行中的0有没有变化

total number of bit operations（时间复杂度![image.png](../images/1686805488442-897742a2-c393-4e92-9769-20072ccc827c.png)

### 9.5 Equivalence Relations

#### Equivalence Relations 等价关系

**equivalent 等价: **if R is an equivalence relation, a is equivalent to b  if `aRb`![image.png](../images/1686805614220-15993860-af73-4d17-9e79-c40c97e0fe99.png)

**等价关系：自反+对称+传递**

![image.png](../images/1686805627180-ea3a211a-9b65-44b2-9808-c3b9dc82c22d.png)<br />![image.png](../images/1686805799270-68905a5b-412b-4618-a41f-1a5601812e7a.png)

- 模m同余是等价关系 R={(a,b) | a≡b(mod m), a,b∈Z}

![image.png](../images/1686805911068-81581a93-752d-46a7-ba43-1dd7d5caf1de.png)

#### Equivalence Classes 等价类

![image.png](../images/1686806254995-016d3164-2ba8-4ce1-983c-6a25f2db7e11.png)<br />**representative**代表元<br />**$[a]_R$ (equivalence class of a with respect to R ) **等价类**: **the set of all elements of A that are equivalent to a

![image.png](../images/1686806734341-8022326e-ba39-4fb9-875d-b23ae9f931f7.png)<br />**[a]m (congruence class modulo m)**模m的同余类<br />![image.png](../images/1686806928721-0db80c4d-9392-41ce-855b-a89fda08af4a.png)<br />![image.png](../images/1686807360810-3768f4df-6d37-40ef-bcc3-6639da4b5626.png)![image.png](../images/1686807377676-09c9b8f5-fe60-4200-bfac-2953b9d5efde.png)

等价关系的数量：partition of a set 有一个分化就有一个等价关系

![image.png](../images/1687310644986-ddf47786-c479-45ff-ad47-721148ccf0cb.png)

> 5个（3个元素集合的等价关系有5个）

![image-20240612191920628](../images/image-20240612191920628.png)![image-20240612191937612](../images/image-20240612191937612.png)![image-20240612192004316](../images/image-20240612192004316.png)

#### Questions

1 R={(a,b) | a≡b(mod m), a,b∈Z},  $pr(Z)={[0]_m,[1]_m,····,[m-1]_m}$​

2 If |A|=n, the p(n)=? 
p(n): the number of different equivalence relations on a set with n elements

> $p(n)=B_n=\sum_{k=0}^{n}C(n,k)$

### 9.6 Partial Orderings

#### Partial Orderings

**poset (S, R)偏序集: **a set S and a partial ordering R on this set<br />![image.png](../images/1686807496537-d71883f0-3735-4d71-89d7-a8bb3b1e566b.png)

**偏序**：自反+**反对称**+传递<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/34417153/1686808725504-601d4c1e-29a2-40bd-a538-03d970ff7855.png#averageHue=%23efefef&clientId=udc947211-f064-4&from=paste&height=146&id=u1842be85&originHeight=219&originWidth=1479&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=168323&status=done&style=none&taskId=u0a41d7e5-18f9-4b58-9ffb-55eb1869a5b&title=&width=986)![image.png](../images/1686809045687-55a9b4e2-bd0b-4397-8f00-6eae1824182c.png)

Example: <img src="../images/image-20240612193005475.png" alt="image-20240612193005475" style="zoom:33%;" />

![image.png](../images/1686808748915-095b9099-0fba-4b66-9701-280ab4ceae9e.png)![image.png](../images/1686808760790-61647510-0a0f-42b6-8ac3-85e2fe820581.png)

 ≤: less than or equal to

![image.png](../images/1686808785788-bed392b4-4772-4618-8123-e747d86d9936.png)

**totally (or linearly) ordered set **全序（线序）集：一个偏序集中每对元素都是可比的![image.png](../images/1686808834421-26f02791-5c61-410b-a9aa-fc8b8cf44166.png)![image.png](../images/1686808930969-54627218-325c-4144-8ade-19b841f7725a.png)

#### Well-ordered良序

![image.png](../images/1686808853571-914a113f-1df8-49a2-b2c5-6281d0fbde17.png)**良序归纳定理**![image.png](../images/1686809156987-1c73ee7d-fe4e-4e3d-bd94-6a570219ca4f.png)

![image.png](../images/1686809295714-a83f3162-f4e6-4457-9794-7477e2495984.png)

Lexicographic ordering 字典顺序

#### Hasse diagram 哈塞图
表示的是偏序![image.png](../images/1686811250315-652921cc-aad1-43d9-adbd-09f3a2314a67.png)![](../images/DM_1-1711365545687-470.png)

![image.png](https://cdn.nlark.com/yuque/0/2023/png/34417153/1686811301659-b79dae22-2a20-4aa8-b218-ea116d025dbf.png#averageHue=%23faf9f7&clientId=udc947211-f064-4&from=paste&height=148&id=uf2c0e388&originHeight=295&originWidth=1349&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=80561&status=done&style=none&taskId=u21f55e84-c473-4ed6-a0f8-80402c48eab&title=&width=675)<img src="../images/1686811321306-086847ad-5ae7-4a9f-85a5-c0592b716bfe.png" alt="image.png" style="zoom:50%;" />

Chain and antichain

<img src="../images/image-20240612194005266.png" alt="image-20240612194005266" style="zoom:50%;" />

#### Maximal and Minimal Elements 极大元与极小元
![image.png](../images/1686811654828-b3b429a9-7e82-4971-9725-da1e5c27f538.png)![image.png](../images/1686811669945-898270d5-b093-43c4-a9f4-1e89c71d9fb8.png)<br />![image.png](../images/1686811823201-4e6fe3a1-b950-4e51-8ec0-f6eb55125278.png)![image.png](../images/1686811808209-8d1c45c7-eead-45f5-871b-0d7cff83e980.png)![image.png](../images/1686811777510-9e103c06-cf35-46ba-bee4-dea53ddba935.png)

Let A be a partially ordered set. If A has a least element a, then a is unique, and is also a minimal element of A. However, the converse fails: a minimal element of A is generally not a least element of A, and a partially ordered set A can have many minimal elements (in which case none of them can be least elements)

**上界和下界（可以有多个）**![image.png](../images/1686811729423-1fc5bf47-56c0-4bc1-939c-3128c61b3ac9.png)

**LUB最小上界&GLB最大下界（最多只能有1个）**![image.png](../images/1686811917130-14fccbc3-d502-4579-afac-395169c50c30.png)

#### lattice 格
**Definition:** A partially ordered set in which every pair of elements has both a least upper bound and a greatest lower bound is called a **lattice**.![image.png](../images/1686812409979-f4fd83d8-44a0-41d0-b8bc-671612e084c7.png)

![图b中d和e同为b、c最小上界，不唯一](../images/1686812819575-401831b9-3557-42d7-b0c8-32a907215b8c.png)

- 图b中d和e同为b、c最小上界，不唯一，最小上界最多只能有1个

![image.png](../images/1686813124448-e5801e36-28ed-4a21-ae78-95c68b456769.png)

![image.png](../images/1686813001201-0e4f1ac2-c306-4634-a48c-0dc73269e820.png)

- 每一个全序集（totally ordered set）都是格
- (Z^+^, |) & (P(s), ⊆) 是格

#### Topological Sorting 拓扑排序
![image.png](../images/1686813655172-63fb29cf-14c7-44c7-bb3a-d794ac749ea2.png)![image.png](../images/1686813227517-933e01ac-9591-4435-811b-8c6a6c7dccf7.png)

![image.png](../images/1686813704187-4f25247f-e4ea-4212-a14e-5876ea721c83.png)![image.png](../images/1686813723475-767684a9-bd2b-4ab0-8494-828bbe4c0975.png)<br />![image.png](../images/1686813974328-1be68a69-7c62-4245-849e-74f7f37c489f.png)

## 10 Graphs
### 10.1 Graphs and Graph Models
![image.png](https://cdn.nlark.com/yuque/0/2023/png/34417153/1686815260257-ec4145f7-9afd-4709-af13-5966ecfddf41.png#averageHue=%23a1dff1&clientId=udc947211-f064-4&from=paste&height=129&id=u3a74c422&originHeight=194&originWidth=1529&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=54632&status=done&style=none&taskId=uc15ba60e-cc07-4070-87d3-9fa24dc7592&title=&width=1019.3333333333334)<br />**finite graph 有限图**<br />A graph in which each edge connects two different vertices and where no two edges connect the same pair of vertices is called a **simple graph**.
简单图没有环，无多重边，无向

Graphs that may have **multiple edges **connecting the same vertices are called **multigraphs**.<img src="../images/1686815396194-08bfd400-51ad-4c70-bc12-c88176df33ef.png" alt="image.png" style="zoom: 50%;" />

**loops:** edges that connect a vertex to itself

**undirected graphs 无向图**: a graph with undirected edges.<br />**directed graph 有向图** : a graph with directed edges.<br />**mixed graph**: a graph with both directed and undirected edges.<br />![image.png](../images/1686825656271-cb0f9e41-fb47-4da5-87e5-7837a9b3db81.png)

**Simple graph** 简单图: A graph in which each edge connects two different vertices and where no two edges connect the same pair of vertices. <br />**Multigraph** 多重图: Graphs that may have multiple edges connecting the same vertices. **Pseudograph 伪图**: Graphs that may include loops, and possibly multiple edges connecting the same pair of vertices.

![image.png](../images/1686825291124-9674cc0a-47e3-4c8c-bc9b-688a24878e83.png)<br />![image.png](../images/1686825270144-47903c47-0ed4-4212-9095-4440cd06d7c2.png)<br />When a directed graph has no loops and has no multiple directed edges, it is called a **simple directed graph.**<br />![image.png](../images/1686825442723-9a8179f7-ea5d-494b-8273-4d95cf8f7d5e.png)
### 10.2 Graph Terminology and Special Types of Graphs
#### Basic Terminology
![image.png](../images/1686826019051-20c259d9-a3b6-47a7-8dbc-be78bf3a3a97.png)<br />![image.png](../images/1686825974748-0337c081-92bd-4247-9eb3-bfc0c14da96c.png)<br />![image.png](../images/1686826037412-792658bc-db9f-4278-a226-48ecd9cc8c8a.png)

<img src="../images/1686825994996-1e59a169-cc1f-40c2-b785-2193b6f987c3.png" alt="image.png" style="zoom: 50%;" />![image.png](../images/1686826054657-70e9f8fd-8fff-407d-9f3f-9f24325bf5e5.png)![image.png](../images/1686826226290-ae18f765-5f8b-4b54-903d-009166c6fd2f.png)![image.png](../images/1686826171638-6e145380-c072-4398-bf5f-51c6e98dbf93.png)![image.png](../images/1686826204070-2b2d98b9-22de-414d-83d8-39254c1ac3ab.png)

![image.png](../images/1686826302875-af716a7c-eae9-495c-a04e-1a5d0e677133.png)![image.png](../images/1686826280920-66660138-5f89-48a6-983c-1176c7239aa7.png)

- 握手定理说明无向图顶点度数之和为偶数

![image.png](../images/1686826391963-2335df09-42d8-44a4-96af-2190f2d3ff94.png)![image.png](../images/1686826415213-25478b71-5442-4990-8a6f-7a3182a3ab71.png)![image.png](../images/1686826444981-06bb5cae-c813-4931-9923-3cfc2cb66f9b.png)<br />![image.png](../images/1686826470845-58c58a96-dc68-4139-b20d-0f57e43bf3a8.png)![image.png](../images/1686826515625-a65e4a4a-9f74-49f6-9e89-1ee02141d805.png)

![image.png](../images/1686798252962-61190870-d375-4cd2-9cfb-0763f4446dbf.png)<br />The undirected graph that results from ignoring the directions of edges is called the **underlying undirected graph**. 基本无向图忽略边的方向

非空简单图一定存在度数一样的顶点

####  Some Special Simple Graphs

##### Complete Graphs 完全图 Kn

每对顶点间都有一条边的简单图

![image.png](../images/1686826723971-51d25a14-73e3-4139-8080-ca833340bc54.png)![image.png](../images/1686826975237-8fafe05f-b6fc-4fc4-b4fe-e8e2c3354737.png)

Kn的边数：$$\frac {n (n-1)} {2}$$

##### 圆圈 Cn

![image.png](../images/1686827016560-3a4f3695-b2f7-466b-97ce-823c8aaca129.png)

##### 车轮 Wn

相同n，比Cycles多一个点放中间和周围的点连

![image.png](../images/1686827036519-d2247c86-ce00-463d-80cd-1b23d6025318.png)

##### 立方体 Qn

![image.png](../images/1686827057223-a7f6ca3a-aa47-4565-8262-41f097392cbb.png)

Qn的顶点数是2^n^，Qn的边数是n*2^(n-1)^

##### Bipartite Graphs 二分图
![image.png](../images/1686827126462-0934c8ce-d299-4705-a180-01d5177a8ed5.png)<br />![image.png](../images/1686827139903-4e955875-c677-4789-b57b-26ae57d70e46.png)

每条线段一端是红色顶点，一端是蓝色顶点

![image-20240621201705534](../images/image-20240621201705534.png)

- 树是二分图

<img src="../images/1686827263319-aafe3c32-3a61-4478-9baf-7dbaa97c9e92.png" alt="image.png" style="zoom:50%;" />![image.png](../images/1686827279902-d66c0b1f-0f9a-49cc-83c4-d20dbbc0b4f6.png)

判断二分图的条件（当且仅当可以用两个颜色着色相邻顶点不重复）

![determine whether a graph is bipartite](../images/1686827316446-7d5452ca-78ac-48b9-acb1-9a189b0aff5f.png "determine whether a graph is bipartite")<br />![image.png](../images/1686827470642-0dba08be-0a3b-41bf-ba59-d67d10542ce4.png)

**complete bipartite graphs 完全二分图** 

$K_{n,n}$

![image.png](../images/1686827513028-9220eeff-459f-4e64-b30f-8432abd8afb8.png)

##### Regular Graphs 正则图

A simply graph is called regular if every vertex of this graph has the same degree.每个顶点度数相同
A regular graph is called n-regular if every vertex in this graph has degree n.
For example, $K_n$ is a (n-1)-regualr; $K_{n,n}$ is a n-regular. 

#### New Graphs from Old

**subgraph 子图**

![image.png](../images/1686828210591-fa48bc1c-ac24-464c-9088-eabe88e6bb3d.png)

H is a *spanning subgraph* of G if W=V, F⊆E

<img src="../images/image-20240621203351742.png" alt="image-20240621203351742" style="zoom:50%;" />

- 选择顶点数✖剩下每条边2种可能情况，C(4,3)✖2^3^表示选3个顶点保留、剩下3条边每条边都有在/不在两种情况

![image.png](../images/1686828265109-461fcfa5-496a-429f-b01b-c7562922f954.png)

导出的子图：只有被移除的顶点相关的边不在

![image.png](../images/1686828497483-94a1a4ac-333f-40c5-bb38-08adb26f0beb.png)

**GRAPH UNIONS 并图**

![image.png](../images/1686828540571-9c5038bd-c301-4b79-b62c-543911715de3.png)![image.png](../images/1686828571941-07399437-271a-4080-93e4-f4d3e979147c.png)

### 10.3 Representing Graphs and Graph Isomorphism
同构<br />**adjacency lists**<br />![image.png](../images/1686829741558-dca2eab6-cdcf-4baa-8054-7919d4514278.png)<br />![image.png](../images/1686829757359-d9c48928-ce86-40de-9681-b76761b632ed.png)
#### Adjacency Matrices  邻接矩阵
邻接矩阵 $A = [a_{ij}]$​，<img src="../images/1686829817552-d9c68f67-3c85-4697-a38a-8bb0f68ced29.png" alt="image.png" style="zoom:50%;" />

![image.png](../images/1686829935273-e2dbedd4-0199-4bfe-9124-a8016a7dc89e.png)

The adjacency matrix of a simple graph is symmetric, that is, $a_{ij} = a_{ji}$.  All undirected graphs, including multigraphs and pseudographs, have **symmetric adjacency matrices**..<br />多重图、伪图、简单图的邻接矩阵都对称

![image.png](../images/1686829981763-d9a341bd-f3a5-4cd4-9a86-457c22b39b61.png)<br /><img src="../images/1686830150867-38b5d630-3ad4-435b-9132-4c245cc27df8.png" alt="image.png" style="zoom:50%;" /><img src="../images/1686830160637-cf1c2864-fbcf-4d9d-8730-1f6ea034da2c.png" alt="image.png" style="zoom: 50%;" /><br />The adjacency matrix for a directed graph does not have to be symmetric. <br />有向图的邻接矩阵不一定对称

#### Incidence Matrices 关联矩阵
n × m matrix M = $[m_{ij}]$，<img src="../images/1686830397070-26d2257b-c807-4043-af29-220f6de25db4.png" alt="image.png" style="zoom:50%;" /><br /><img src="../images/1686830625517-6d8981f6-6e3e-41a8-bfc7-41f2e853a1f4.png" alt="image.png" style="zoom:50%;" /><img src="../images/1686830651606-bf61affa-bc34-4557-ada2-f173de960ddc.png" alt="image.png" style="zoom:50%;" /><br />![image.png](../images/1686830735433-31dc7366-ce8b-4692-b89a-11d73d1e0069.png)
#### Isomorphism of Graphs 同构
![image.png](../images/1686831974024-2fb0fc10-f592-4003-82b7-f3ef6816cdf4.png)![image.png](../images/1686832009804-5f72098d-c771-4450-876d-1e32fdd4a5b2.png)<br />![image.png](../images/1686832270430-786f6bc6-28aa-473d-bf63-1b63e06ebed6.png)<br />**graph invariant 图形不变量**<br />顶点数、边数、顶点的度数

9个顶点不同构的有根树有9个

### 10.4 Connectivity
**simple path/circuit 简单通路/回路：**a path that does not contain an edge more than once 只包含一条边一次

**circuit/cycle**圆圈：路径开始、结束于同一个顶点

![image.png](../images/1686832503729-276da8c6-1be2-4086-8bda-7005ae5c2cb2.png)![image.png](../images/1686832739173-0410aa53-f38b-4e5b-bb8b-0835b82a1e02.png)<br />![image.png](../images/1686832615308-c4da4347-8dd3-4253-a23a-76974831a78a.png)<br />![image.png](../images/1686832701305-4ae347d4-f0aa-43c0-9155-4414e78fcd33.png)![image.png](../images/1686832721484-138beb15-5483-47db-8803-6605caea5dbc.png)<br />**connected graph: **an undirected graph with the property that there is a path between every pair of vertices 无向图，每对不同的顶点间都有一条路径

#### Paths in Acquaintanceship Graphs  无向图的连通性
![image.png](../images/1686833411907-22adbea3-30ce-4a07-b4ef-5160eb824272.png)每对顶点之间都有路径，则图是连通的![image.png](../images/1686833428238-cd415b90-5bfb-4b78-8451-49d1bc2e4ddb.png)<br />**connected components 连通分支组件**

图G的极大连通子图被称作连通组件

<img src="../images/1686833504822-289f8995-969a-4b20-86b8-a73618580237.png" alt="image.png" style="zoom:50%;" />

- For any nonempty subset S of set V, the number of connected components in G-S <=|S|

**cut vertices**(or **articulation points**) 割点：a vertex v such that G − v is disconnected

**cut edge **or **bridge** 割边：an edge e such that G - e is disconnected

割点和割边都能使图的组件变多

<img src="../images/image-20240621211119777.png" alt="image-20240621211119777" style="zoom:40%;" />

![image.png](../images/1686833596084-0d7a3364-e24e-4da8-b4a9-9098db573d36.png)<img src="../images/1686833623198-61b73d7c-2748-4c5e-9cf3-4fd3a1d1a712.png" alt="image.png" style="zoom:50%;" />

​	不是所有连通图都有割点，这些图被称为不可分割的 nonseparable graphs，它们可以认为比有割点的图连通性更强


We measure the graph connectivity based on the minimum number of vertices that can be removed to disconnect a graph.我们用使图变得不连通的最小移出顶点数来衡量图的连通性

**Vextex connectivity 点连通性**

![image.png](../images/1686833676624-03d1d3f0-1bc0-4863-9704-e61c353a17d4.png)

A subset V′ of the vertex set V of G = (V, E) is a **vertex cut**, or **separating set**, if G − V ′ is disconnected.

- 所有连通图都有点割集，除了完全图

**𝜿(G) (the vertex connectivity of G): **the size of a smallest vertex cut of G 点割集

![image.png](../images/1686833784708-3c8b51c0-bc93-4269-907e-822f59f5bf99.png)

**Edge connectivity 边连通度**

![image.png](../images/1686833863966-6ba2fc72-a7bd-4b86-ab46-66ff40764112.png)![image.png](../images/1686833879534-716949b5-e641-423e-acc4-d6583b37414e.png)

**𝝀(_G_) (the edge connectivity of _G_)**: the size of a smallest edge cut of _G_ 边

- 找到度最小的顶点，删边

![image.png](../images/1686833945740-805894f0-e513-4e83-ac27-f85746c1a8bb.png)<img src="../images/1686833928380-6d34a32f-0a3f-43b4-9dd0-7c660d090a2a.png" alt="image.png" style="zoom:50%;" />点≤边≤最小顶点度数

#### Connectedness in Directed Graphs 有向图的连通性
![image.png](../images/1686834047390-fcff2666-3620-4a89-a07d-828697dafcbe.png)

Strongly connected强连通：有一条路从a到b，从b到a（对所有图中的顶点a,b）

![image.png](../images/1686834061119-9733410d-d738-4428-8e77-a7d33347efbc.png)

**Strong components of a directed graph**

![image.png](../images/1686834113565-4fb4d766-cbfe-4029-b7f6-4b715b5c0c8a.png)<img src="../images/1686834682685-bda39784-6ee8-4bb8-9d3a-824d813ae14a.png" alt="image.png" style="zoom:50%;" />

#### Paths and Isomorphism

两个图同构当且仅当它们有相同长度的简单回路 or 两个图包含经过顶点的路径且两个图中路径对应的顶点具有相同的度数

<img src="../images/1686835236987-56df7785-b15d-43a2-9bd7-14e84867f99a.png" alt="image.png" style="zoom:50%;" />同构

#### Counting Paths Between Vertices
![image.png](../images/1686835279563-18eebdc0-d225-41cf-bda8-e7deba304c11.png)<br />![image.png](../images/1686835327620-bfddcb15-4882-4368-89cc-42fbdb3a3a78.png)

矩阵的乘法$A^{r+1}=A^r·A=(d_{ij})_{n✖n}$，第m行✖第n列得到第(m, n)个元素的值

![image.png](../images/1686835352586-c3ee8c49-fb7d-4425-8bb3-751fef855cbf.png)

### 10.5 Euler and Hamilton Paths
#### Euler Paths and Circuits 欧拉通路&回路
经过边<br />![image.png](../images/1686835435285-5a5b9f3b-a3e9-4c06-ba13-a5c05b5f7236.png)![image.png](../images/1686835445768-f6bd7945-8746-404c-9793-93a32c29a8f3.png)![image.png](../images/1686835497513-59d1a5ca-e27d-46ba-8000-d38958ecbfa9.png)<br />![image.png](../images/1686835513831-0c5855b7-bf8f-4156-a32b-5776c4582764.png)

**NECESSARY AND SUFFICIENT CONDITIONS FOR EULER CIRCUITS AND PATHS** 欧拉回路/通路的充分必要条件

![image.png](../images/1686835560119-273b35f1-e2d7-426f-ac3d-86a469cc94ef.png)![image.png](../images/1686835596475-4d2c4136-3f47-4932-b551-fe6e4af32871.png)<br />![image.png](../images/1686835656087-46b233bb-1747-4c8a-9a50-7a188f16748f.png)![image.png](../images/1686835640562-a3fc54d4-c30e-4765-86ca-e4303fef11b4.png)

有欧拉通路就从一个奇数度的顶点出发，于另一个奇数度的顶点结束

**Euler circuits and paths in directed graphs有向图 欧拉回路/通路的充分必要条件**

欧拉回路：A directed multigraph having no isolated vertices has an Euler circuit if and only if

- the graph is weakly connected 弱连通
- the in-degree and out-degree of each vertex are equal 每个顶点入度和出度一样

欧拉通路：A directed multigraph having no isolated vertices has an Euler path but not an Euler circuit if and only if

- the graph is weakly connected 弱连通
- the in-degree and out-degree of each vertex are equal for all but two vertices, one that has in-degree 1 larger than its out-degree and the other that has out-degree 1 larger than its in-degree 每个顶点入度和出度一样，但有两个顶点是例外：一个 入度=出度+1，另一个 出度=入度+1

#### Hamilton Paths and Circuits 哈密顿

经过顶点<br />![image.png](../images/1686835719648-cb0a07fd-118e-4d57-8e72-63269f567b99.png)<br />![image.png](../images/1686835773013-0e58f9d9-8d26-454f-a0c6-a3d4d197afae.png)<br />**CONDITIONS FOR THE EXISTENCE OF HAMILTON CIRCUITS**

哈密顿回路存在（充分）条件（没有有效的必要条件）

![image.png](../images/1686835829932-9b052f0b-3ca8-4959-adb3-396c45c3bef2.png)<br />![image.png](../images/1686835862075-72475aab-21f2-4fb5-99b1-47ced9869ce9.png)

若一个图存在哈密顿回路，就称为哈密顿图 hamilton graph

- Kn（完全图）存在哈密顿回路（n≥3）
- n个顶点的完全图有多少不同长度的哈密顿回路？$\frac{(n-1)!}{2}$

### 10.6 Shortest-Path Problems
Graphs that have a number assigned to each edge are called **weighted graphs**.加权图<br />![image.png](../images/1686839412067-4e09a4d6-1177-4eac-aaa9-dbac3c939b45.png)<br />![image.png](../images/1686839389651-56764d5c-18bd-4ed1-bf65-426ecbc7020b.png)

![image-20240622140445367](../images/image-20240622140445367.png)

### 10.7 Planar Graphs

平面图<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/34417153/1686839613472-f478b363-12ae-4780-9671-70b6e26ee444.png#averageHue=%23ddf2fb&clientId=udc947211-f064-4&from=paste&height=122&id=u41eed4e4&originHeight=183&originWidth=1512&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=54029&status=done&style=none&taskId=u096e9c72-0ed1-40a1-96ce-a4e781fbe62&title=&width=1008)<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/34417153/1686839526673-83a92a3e-f62a-4a34-9010-19ebe7726a86.png#averageHue=%23c8c8c8&clientId=udc947211-f064-4&from=paste&height=96&id=ua9b70611&originHeight=144&originWidth=1243&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=209566&status=done&style=none&taskId=uccb2dac0-cc10-40ec-a22a-3834b889f2a&title=&width=828.6666666666666)

完全二分图$K_{2,n}(n≥1)$是平面图；完全二分图$K_{1,n}$是平面图

#### Euler's Formula 欧拉公式

regions面，edges边，vertices顶点

![image.png](../images/1686839885440-457ccc85-79eb-4eb9-9a34-79fe3e1afed4.png)

- 连通！平面！简单图！才满足欧拉公式

![image.png](../images/1686839916419-4a0cb95f-25a4-43e0-9080-5fae9b39fb71.png)

<img src="../images/image-20240622143026998.png" alt="image-20240622143026998" style="zoom:40%;" />
$$
2e=\sum_{all-region-R}deg(R)
$$
如果平面图G有k个连通组件，e条边和v个顶点，那么区域r=e-v+2+(k-1)=e-v+k+1

![image.png](../images/1686839962753-59185b58-a8eb-489c-b550-ed4d7263ecdb.png)![image.png](../images/1686839983501-823194a6-527c-4537-89d0-139f2fd9b35f.png)

不连通的简单平面图e≤3v-6也成立

![image.png](../images/1686840034937-28607260-ec2c-4638-a2ba-443aa9501d95.png)![image.png](../images/1686840007910-aa1cee30-9068-4a37-b4d9-f9b510a7c308.png)

![image.png](../images/1686840081550-25379775-fb98-4eee-a3a4-ee6283ca052b.png)![image.png](../images/1686840056941-cc2b998c-3383-4415-9196-8aa5687db963.png)

如果一个连通平面图每个区域region有至少k条边，则$e≤\frac{(v-2)k}{k-2}$

![image.png](../images/1686840247170-c288a3d5-cde3-471b-b4eb-0c3a6e6abb63.png)

#### Kuratowski’s Theorem 库拉图斯基
**homeomorphic 同胚的：**two undirected graphs are homeomorphic if they can be obtained from the same graph by a sequence of elementary subdivisions

**elementary subdivision 初等细分：**the removal of an edge {_u, v_} of an undirected graph and the addition of a new vertex _w together with edges {_u, w_} and {_w, v}

![image.png](../images/1686844230975-48d7039a-f928-4cf3-8168-e3a16f154734.png)<br />![image.png](../images/1686844279208-67470c1d-bb7d-4590-bc7b-03aa3ae774de.png)![image.png](../images/1686845496487-8414fe97-9a3b-4599-a66b-aab2ec233ae7.png)![image.png](../images/1686878552395-7a412394-20b1-497b-8b67-efeac32589b3.png)<br />![image.png](../images/1686878524932-4dbebfdd-bdf6-4b9f-9838-b8016022d57e.png)![image.png](../images/1686878580061-03380554-fd83-4e87-9e47-ef0aa4002ddb.png)

### 10.8 Graph Coloring

**dual graph **对偶图

![image.png](../images/1686878658851-5885b9d5-e9dc-46b9-9359-7178794af544.png)<br />![image.png](../images/1686878700445-47355567-b764-40ec-a3ed-5a5fef8afa67.png)<br />![image.png](../images/1686878735119-1f432bf6-39eb-4cd4-b516-6892b89ae590.png)

**chromatic number** $\chi(G)$: the least number of colors needed for the coloring of this graph

![image.png](../images/1686878748957-79519aa6-3a60-413a-a6f5-772b4a476070.png)![image.png](../images/1686878923455-da0e986b-50fe-43ba-b2bb-f210f8b3c98d.png)

$\chi(K_n)=n, \chi(K_n-e)=n-1,\chi(K_{m,n}=2)$

能用两个颜色着色的简单图都是二分图；连通二分图能用2个颜色着色

![image.png](../images/1686878790453-760c88e4-d95b-425d-a490-94959a822429.png)![image.png](../images/1686878832594-56c45d5a-b4f5-41f9-b416-d1aeeb5cef8d.png)

## 11 Trees
### 11.1 Introduction to Trees
![image.png](../images/1686879252424-063b669b-be01-4bfe-99a0-3ebab2f34fc9.png)

连通+无向+n个顶点&n-1条边是一棵树；连通+无向+没有简单回路是一棵树

**forest**：

无向图是一棵树当且仅当任意一对顶点之间都有唯一简单路径(unique simple path)

**root**<br />![image.png](../images/1686879311598-cd8132fa-bd63-4a29-b467-bce4ef2ad2bc.png)![image.png](../images/1686903704123-5aa1e368-a4a7-4ee6-8539-698aaa676654.png)**parent 父母 of v in a rooted tree: **the vertex u such that (u, v) is an edge of the rooted tree<br />**child 孩子 of a vertex v in a rooted tree: **any vertex with v as its parent<br />**internal vertex 内点: **a vertex that has children<br />**leaf 树叶: **a vertex with no children<br />![image.png](../images/1686903805746-72056171-df95-4aaf-bb60-7d44931d8d80.png)![image.png](../images/1686879337372-f79758c1-984d-4738-a35c-bf702b1e2594.png)<br />**full m-ary tree 满m叉树: **a tree with the property that every internal vertex has exactly m children 每个内点都有m个孩子<br />**ordered tree 有序树: **a tree in which the children of each internal vertex are linearly ordered 每个内点的孩子都是有序的<br />![image.png](../images/1686904795079-26490e79-1584-4836-883e-6f1109e2f73d.png)

#### Properties of Trees
![image.png](../images/1686903912194-03b9e068-6987-40ea-b16f-b5fa53dd0fe7.png)<br />![image.png](../images/1686903928125-c709c6e3-152a-450a-bdfc-997fa9622da8.png)<br />![ ](../images/1686903943379-2ffa0796-8e6a-49c4-bca4-dd204333cbdf.png)<br />**BALANCED _m_-ARY TREES 平衡的m叉树**<br />**level of a vertex 顶点的层: **the length of the path from the root to this vertex <br />**height of a tree 树高: **the largest level of the vertices of a tree<br />**balanced tree: **a tree in which every leaf is at level h or h − 1, where h is the height of the tree<br />![image.png](../images/1686904079137-313e0f56-c6c8-4f0a-a685-c3bacc3349ce.png)<br />![image.png](../images/1686904659767-f30c3be1-98be-4ee1-88d8-d00c7cb77837.png)![image.png](../images/1686904694698-fc9408e7-80f1-4d9d-87a5-3879fcef8f5a.png)

根的高度是0

### 11.2 Applications of Trees

**binary search tree 二叉搜索树**

![image.png](../images/1686907933640-fe28a089-e31c-4f6f-82f3-dac0bd39b2ac.png)<br />![image.png](../images/1686907949931-c640a4a7-4706-46b8-8027-ded1f219046b.png)

Decision Trees 决策树

**Huffman coding 哈夫曼编码**<br />![image.png](../images/1686885438604-eff04e04-3993-40de-a815-80e4a549a647.png)

左边的点权重>右边

#### Game Trees 博弈树
![image.png](../images/1686908112917-398e2336-5fcc-4a23-aa76-2f68124e4572.png)<br />![image.png](../images/1686908132475-2e6749be-5c0a-4a9c-b005-500274e82933.png)![image.png](../images/1686908168441-a18a004b-2e7c-483c-934f-79163da4a767.png)![image.png](../images/1686908181818-5fd8248b-f033-4fd3-8854-21a1e6d178b1.png)
### 11.3 Tree Traversal
遍历算法<br />**preorder traversal** 前序：Visit root, visit subtrees left to right<br />![image.png](../images/1686908365539-97bd8d46-9a17-4968-a2b5-df1e57b01eb2.png)<br />**inorder traversal** 中序：Visit leftmost subtree, visit root, visit other subtrees left to right<br />![image.png](../images/1686908414823-2c32c23e-360f-45d2-827c-28de454bfb3f.png)<br />**postorder traversal **后序：Visit subtrees left to right; visit root<br />![image.png](../images/1686908456064-4c8abb13-4cfe-4fe5-8d4a-468b899a2cdc.png)<br /><img src="../images/1686908341653-7ced7bee-6a52-4d56-a797-d7eb26bf2d40.png" alt="image.png" style="zoom:50%;" /><img src="../images/1686908519344-2e36f1de-b010-4189-b71d-6a66c2ac31f3.png" alt="image.png" style="zoom:50%;" />
#### Infix, Prefix, and Postfix Notation 中缀、前后缀记法
![image.png](../images/1686908656836-114e0b7b-6b1b-44da-b53a-46606ef4d5d6.png)<br />The fully parenthesized expression obtained in this way is said to be in **infifix form. 中缀**<br />**prefix form 前缀**<br />![image.png](../images/1686908742102-3418ad28-4ec2-4ccd-9860-a5b7f2c0c666.png)<br />**postfix form 后缀**<br />![image.png](../images/1686908778362-9ef4359c-53d2-469e-b6b4-ada1408da1ed.png)![image.png](../images/1686908799208-ad5f60ad-3464-490a-abdf-8776ec91de23.png)<br />![image.png](../images/1686908876949-cfe03a3e-9a54-4efe-8dac-53d94e8662f8.png)
### 11.4 Spanning Trees
生成树<br />![image.png](../images/1686615169848-e3c15c81-e351-45c7-966e-310003a5a13c.png)![image.png](../images/1686615323202-bc9fa35b-f172-4b56-b86c-100aa2995a79.png)

![image.png](../images/1686615293328-9cd39b9f-1f57-4c89-b6cc-cb07524fa551.png)![image.png](../images/1686615341401-f7e814b6-1077-4937-900e-889333a1c8f5.png)<br />**depth-first search 深度优先搜索 **also called **backtracking** 回溯<br />![image.png](../images/1686616371665-c8be5b16-af77-4dde-ad5f-040cd5e1c350.png)<br />![image.png](../images/1686616876579-47615eec-1a14-4a78-885c-d2aff871689b.png)

1. 任意选择图形的一个顶点作为根。
2. 从这个顶点开始的路径，连续添加边，其中每条新的边都与路径中的最后一个顶点和一个还没不在路径中的顶点相连
3. 继续向这条路径添加边，越长越好。
4. 如果该路径穿过图形的所有顶点，那么由该路径组成的树就是一棵生成树。
5. 如果路径没有穿过所有顶点，就必须增加更多的边。如果可能的话，回到路径中的最后一个顶点，形成一条新的路径。从这个顶点开始，穿过尚未访问的顶点。如果做不到这一点，就向后移动路径中的另一个顶点。
6. 重复这个过程。

![image.png](../images/1686616319326-511af33c-928e-45cc-a0be-2558dd8d8f91.png)<br />**tree edges and back edges**<br />![image.png](../images/1686617435606-4fdd642e-9f62-49cf-8f94-1bd2ec3e4d74.png)<br />1.任意选择图的一个顶点作为根，并将所有与该顶点相关的边相连。<br />2.在此阶段添加的新顶点将成为生成树中的级别1。任意排序他们。<br />3.对于级别1的每个顶点，按顺序访问，添加每个边只要它不产生简单的回路，就可以入射到树的这个顶点。任意排序级别为1的每个顶点的子顶点。这将生成树中级别为2的顶点。<br />4.按照相同的过程进行操作，直到添加了树中的所有顶点。

### 11.5 Minimum Spanning Trees
**spanning tree: **a tree containing all vertices of a graph <br />生成树：包含图的所有顶点的树<br />**minimum spanning tree: **a spanning tree with smallest possible sum of weights of its edges<br />最小生成树：边的权之和最小<br />![image.png](../images/1686618223170-1a2499ba-602e-4942-9b8a-710ca7c2b03a.png)

#### Prim’s algorithm 普林算法
![image.png](../images/1686909731108-890ab062-847a-46d6-81e6-966020c1348a.png)<br />![image.png](../images/1686618379419-bfb7ed3d-a161-4f3d-986a-6ec63f9131ca.png)<br />![image.png](../images/1686619567004-fca3e361-adc9-4c65-b516-1d6cbfb68f86.png)

