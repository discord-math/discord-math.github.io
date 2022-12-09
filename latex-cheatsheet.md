---
title: LaTeX cheatsheet
updated_at: 2022-12-07
mathjax: true
extra_styles: cheatsheet
---

## Table of Contents
{:.no_toc}

* TOC
{:toc}
<hr>

## What is $\LaTeX$?
$\LaTeX$ is the standard system used for rendering mathematical and scientific documents. It is also how you can render mathematical expressions and formulae server-wide using the [@TeXiT](https://discord.com/users/510789298321096704){: .mention target="_blank"} bot. If you've ever wondered how scientific papers or textbooks are laid out in the way they are, this is the guide for you.

Unlike other document creation systems such as Microsoft Word, documents produced using $\LaTeX$ are not written using a so-called "what-you-see-is-what-you-get" format. Instead, documents are written in plaintext `.tex` files in the $\LaTeX$ language that are then *compiled* into `.pdf` documents.

Regular text will be rendered as itself, but the following punctuation symbols have special meaning: The backslash symbol `\` is used for "commands" or "macros" which insert specical symbols or notation into the text. Braces (`{` and `}`) are used to group symbols together into a block. Dollar signs (`$` and `$$`) are used to include formulae in the text.

There are two general modes of operation: "math mode" is used for formulae, and "text mode" is used for text. Formulae can be surrounded by single dollars to be included in the text "inline", for example `$a + b = c$` produces $a+b=c$. Double dollars render a large fomrula in "display style", which inserts line breaks around the formula, and also has an effect on how some notation is rendered (more on this in [Examples](#examples)). 

Most symbols are rendered as themselves (namely, `!`, `'`, `(`, `)`, `*`, `+`, `,`, `-`, `.`, `/`, `:`, `;`, `<`, `>`, `=`, `?`, `[`, `]`, `|`). To render other, more interesting characters, the commands given in the [Commands Reference](#command-reference) below can be used. To write literal braces and dollars, `\{`, `\}`, and `\$` must be used, respectively.

## Examples
In this section we explore some demonstrative examples of how to render mathematical expressions and formulae using $\LaTeX$, as well as point out some common mistakes.

### Inline vs Display mode
Let's look at a $\LaTeX$ snippet that renders an equation in math mode:
```latex
Perhaps the most famous equation in all of physics is $E=mc^2$
```
This is rendered as:
<div class="latexexample">
$\text{Perhaps the most famous equation in all of physics is } E=mc^2$
</div>

There are a few things worth noting here. First, the $\LaTeX$ rendering engine will automatically add whitespace around symbols such as `=`. Second, the math that is rendered is *inline* with the rest of the text. 

Let's see what happens when we try rendering the same equation in display mode.
```latex
Perhaps the most famous equation in all of physics is $$E=mc^2$$
```
<div class="latexexample">
$\text{Perhaps the most famous equation in all of physics is}$

$$ E = mc^2 $$

</div>

Display mode renders your mathematical expression on its own centered line. A common use case for display mode is for rendering "large" operators in a more readable format. Let's look at another two examples where the only difference is that the first is rendered in math mode and the second in display mode.

<div class="latexexample">
$\text{Fubini's theorem gives conditions under which} \int_{X\times Y} f(x,y)\,\text{d}(x,y) = \int_X\left(\int_Y f(x,y)\,\text{d}y\right)\,\text{d}x$
</div>
versus
<div class="latexexample">
$\text{Fubini's theorem gives conditions under which}$

$$\int_{X\times Y} f(x,y)\,\text{d}(x,y) = \int_X\left(\int_Y f(x,y)\,\text{d}y\right)\,\text{d}x$$

</div>

### Large operators
Mathematics (and therefore $\LaTeX$) contains many large operators, such as $\sum$, $\int$, and $\prod$. Other symbols that act like large operators are $\lim$, $\sup$, $\limsup$, etc. Common between all these symbols is that they are most often seen with expressions placed below and/or above them. Thankfully, this is easy to achieve in $\LaTeX$. The most common way to achieve this is to use the subscript `_` and superscript `^` characters; for example,
```latex
\int_a^b
```
is rendered in inline mode as
<div class="latexexample">
$\int_a^b$
</div>
and in display mode as
<div class="latexexample">
$$\int_a^b$$
</div>
A common mistake people make is in trying to render more complex expressions. For example, you may try to write a sum from $n=1$ to $5$ with `\sum_n=1^5`. This, however, renders as:
<div class="latexexample">
$$\sum_n=1^5$$
</div>
The correct way to render what we want is to use braces to enclose the lower bound of the sum; i.e. `\sum_{n=1}^5`, giving
<div class="latexexample">
$$\sum_{n=1}^5$$
</div>
A special case of "large operator" is the fraction. Fractions are rendered with their own syntax[^1]; namely, `\frac{a}{b}`, which renders in inline mode as
<div class="latexexample">
$\frac{a}{b}$
</div>
and in display mode as
<div class="latexexample">
$$\frac{a}{b}$$
</div>

### Parentheses
$\LaTeX$ does not automatically (at least, not by default), scale parentheses to match the vertical height of the enclosed expression. For example, `(\frac{a}{b})` is rendered as
<div class="latexexample">
$$(\frac{a}{b})$$
</div>
Thankfully, there is an easy means by which to scale parentheses (as well as braces, brackets, and other symbols); specifically, prefix the left symbol with `\left` and the right symbol with `\right`. So, rewriting our example from above, we obtain `\left( \frac{a}{b} \right)`, which is rendered as
<div class="latexexample">
$$\left( \frac{a}{b} \right)$$
</div>
Note that there is also a `\middle` command that is most often used for matching the height of the vertical bar glyph `|`. An example of this being used may be
```tex
\left\{ x \middle\mid x \leq \frac{1}{2} \right\}
```
rendered in display mode as
<!-- BUG For some reason the vertical bar here is not rendering properly -->
<div class="latexexample">
$$\left\{ x \middle\lvert x \leq \frac{1}{2} \right\}$$
</div>

### Spacing
In general, $\LaTeX$ handles the horizontal spacing of mathematical expressions automatically. Sometimes, however, this produces undesirable results. Compare the following two expressions,
```latex
$$ \int f(x) dx $$
```
<div class="latexexample">
$$ \int f(x) dx $$
</div>
and
```latex
$$ \int f(x)\, dx$$
```
<div class="latexexample">
$$ \int f(x)\, dx$$
</div>
In the former case the space between $f(x)$ and $dx$ may seem too small. To fix this, authors commonly add a spacing macro (in this example `\,`) to add some additional horizontal space. A list of common spacing macros is given in the [Commands Reference](#spacing) below.

### Some common mistakes
There are a number of common mistakes that $\LaTeX$ beginners make. The most obvious case of this is not using macros for standard functions such as triogonometric functions ($\sin$, $\cos$, etc) and logarithms ($\ln$ and $\log$). Compare, for example,
```latex
$$ \int tan(x)\, dx = ln \lvert sec(x) \rvert + c $$
```
<div class="latexexample">
$$ \int tan(x)\, dx = ln \lvert sec(x) \rvert + c $$
</div>
with
```latex
$$ \int \tan(x) dx = \ln \lvert \sec(x) \rvert + c $$
```
<div class="latexexample">
$$ \int \tan(x) dx = \ln \lvert \sec(x) \rvert + c $$
</div>
One can also render derivatives and infinitesimals in a more standard way by using the `\text` macro

## Using $\LaTeX$ on the server
The <a class="mention">@TeXiT</a> bot can be used anywhere on the server to render mathematics using $\LaTeX$. To use it, simply write a normal message with any latex expressions that you want to be rendered enclosed in either `$ ... $` or `$$ ... $$`.

## Command reference

### Simple algebraic symbols

| Name | Expression | $\LaTeX$ code |
|:---|:---:|---:|
| Fraction | $\frac{a}{b}$ | `\frac{a}{b}` |
| Multiplication | $\times$ | `\times` |
| Multiplication (dot) | $\cdot$ | `\cdot` |
| Composition | $\circ$ | `\circ` |
| Superscript | $a^{b}$ | `a^{b}`|
| Subscript | $a_{b}$ | `a_{b}` |
| Plus/Minus | $\pm$ | `\pm` |
| Minus/Plus | $\mp$ | `\mp` |
| Square root | $\sqrt{a}$ | `\sqrt{a}` |
| Arbitrary root | $\sqrt[n]{a}$ | `\sqrt[n]{a}` |
| Not equals | $\neq$ | `\neq` or `\not=`|
| Approximately equals | $\approx$ | `\approx` |
| Tilde | $\sim$ | `\sim` | 
| Proportional to | $\propto$ | `\propto` |
| Less than or equal to | $\leq$ | `\leq` or `\le` |
| Greater than or equal to | $\geq$ | `geq` or `\ge` |
| Much less than | $\ll$ | `\ll` |
| Much greater than | $\gg$ | `\gg` |
| Congruent to | $\cong$ | `\cong` |
| Magnitude | $\lvert a \rvert$ | `\lvert a \rvert` |
| Norm | $\lVert a \rVert$ | `\lVert a \rVert` |
| Floor | $\lfloor a \rfloor$ | `\lfloor a \rfloor` |
| Ceiling | $\lceil a \rceil$ | `\lceil a \rceil` |
| Bar | $\bar{a}$ | `\bar{a}` |
{: .latex_table}

### Greek letters
Below is a list of all greek letters available in $\LaTeX$. The commands given are for the lowercase versions; however, to obtain the uppercase version of a letter you simply make the first letter of the command uppercase. For example `\gamma` gives $\gamma$ whereas `\Gamma` gives $\Gamma$.

| Letter | Rendered version | $\LaTeX$ code |
|:---|:---:|---:|
| Alpha | $\alpha$ | `\alpha` |
| Beta | $\beta$ | `\beta` |
| Gamma | $\gamma$ | `\gamma` |
| Delta | $\delta$ | `\delta` |
| Epsilon | $\epsilon$ | `\epsilon` |
| Zeta | $\zeta$ | `\zeta` |
| Eta | $\eta$ | `\eta` |
| Theta | $ \theta $ | `\theta` |
| Iota | $ \iota $ | `\iota` |
| Kappa | $ \kappa $ | `\kappa` |
| Lambda | $ \lambda $ | `\lambda` |
| Mu | $ \mu $ | `\mu` |
| Nu | $ \nu $ | `\nu` |
| Pi | $ \pi $ | `\pi` |
| Rho | $ \rho $ | `\rho` |
| Sigma | $ \sigma $ | `\sigma` |
| Tau | $ \tau $ | `\tau` |
| Upsilon | $ \upsilon $ | `\upsilon` |
| Phi | $ \phi $ | `\phi` |
| Chi | $ \chi $ | `\chi` |
| Psi | $ \psi $ | `\psi` |
| Omega | $ \omega $ | `\omega` |
{: .latex_table}

#### Mathematical variants
A handful of variant greek letters see widespread use in mathematics and physics. These are listed below.

| Letter | Rendered version | $\LaTeX$ code |
|:---|:---:|---:|
| Epsilon | $\varepsilon$ | `\varepsilon` |
| Theta | $\vartheta$ | `\vartheta` |
| Phi | $\varphi$ | `\varphi` |
{: .latex_table}

### Other scripts
Note that most of these fonts require the <a href="https://ctan.org/pkg/amsfonts" target="_blank">`amsfonts`</a> package.

| Script | Examples | $\LaTeX$ code |
|:---|:---:|---:|
| Blackboard Bold | $\mathbb{N}$ and $\mathbb{R}$ | `\mathbb{N}` and  `\mathbb{R}` |
| Fraktur | $\mathfrak{N}$ and $\mathfrak{R}$ | `\mathfrak{N}` and `\mathfrak{R}` |
| Script | $\mathscr{N}$ and $\mathscr{R}$ | `\mathscr{N}` and `\mathscr{R}` |
| Caligraphic | $\mathcal{N}$ and $\mathcal{R}$ | `\mathcal{N}` and `\mathcal{R}` |
| Boldface | $\mathbf{N}$ and $\mathbf{R}$ | `\mathbf{N}` and `\mathbf{R}` |
| Sans-serif | $\mathsf{N}$ and $\mathsf{R}$ | `\mathsf{N}` and `\mathsf{R}` |
| Typewriter | $\mathtt{N}$ and $\mathtt{R}$ | `\mathtt{N}` and `\mathtt{R}` |
| Italic | $\mathit{N}$ and $\mathit{R}$ | `\mathit{N}` and `\mathit{R}` |
| Normal (default math font) | $\mathnormal{N}$ and $\mathnormal{R}$ | `\mathnormal{N}` and `\mathtt{R}` |
{: .latex_table}

### Set-theoretic and logical symbols

| Name | Symbol | $\LaTeX$ code |
|:---|:---:|---:|
| In | $\in$ | `\in` |
| Not in | $\notin$ | `\notin` |
| Empty set | $\varnothing$ | `\varnothing` |
| Proper subset | $\subset$ | `\subset` |
| Subset | $\subseteq$ | `\subseteq` |
| Proper superset | $\supset$ | `\supset` |
| Superset | $\supseteq$ | `\supseteq` |
| Union | $\cup$ | `\cup` |
| Cap | $\cap$ | `cap` |
| Set minus / Backslash | $\setminus$ | `\setminus` |
| For all | $\forall$ | `\forall` |
| There exists | $\exists$ | `\exists` |
| Implies | $\implies$ | `\implies` |
| If and only if | $\iff$ | `\iff`| 
{: .latex_table}

### Calculus

| Name | Symbol | $\LaTeX$ code |
|:---|:---:|---:|
| Sum | $\sum$ | `\sum` |
| Product | $\prod$ | `\prod` |
| Coproduct | $\coprod$ | `\coprod` |
| Infinity | $\infty$ | `\infty` |
| To | $\to$ | `\to` |
| Maps to | $\mapsto$ | `\mapsto` |
| Prime | $\prime$ | `\prime` |
| Partial derivative | $\partial$ | `\partial` |
| Velocity | $\dot{x}$ | `\dot{x}` |
| Acceleration | $\ddot{x}$ | `\ddot{x}` |
| Integral | $\int_{a}^{b}$ | `\int_{a}^{b}` |
| Double integral | $\iint$ | `\iint` |
| Triple integral | $\iiint$ | `\iiint` |
| Contour integral | $\oint$ | `\oint` |
| Del / Nabla | $\nabla$ | `\nabla` |
{: .latex_table}

### Simple geometry

| Name | Symbol | $\LaTeX$ code |
|:---|:---:|---:|
| Parallel | $\parallel$ | `\parallel` |
| Not parallel | $\nparallel$ | `\nparallel` |
| Perpendicular | $\perp$ | `\perp` |
| Angle | $\angle$ | `\angle` |
| Triangle | $\triangle$ | `\triangle` |
| Square | $\square$ | `\square` |
| Vector | $\overrightarrow{AB}$ | `\overrightarrow{AB}` |
| Line segment | $\overline{AB}$ | `\overline{AB}` |
{: .latex_table}

### Other useful symbols/macros

| $\LaTeX$ spacing command | Description |
|:---|:---|
| `\quad` | A space equal to the current font size |
| `\qquad` | Twice the length of `\quad` |
| `\,` | 3/18ths of `\quad` |
| `\:` | 4/18ths of `\quad` |
| `\;` | 5/18ths of `\quad` |
| `\!` | -3/18ths of `\quad` |
| `\ ` (backslash followed by a space) | A space equivalent to that in normal text |



## Further resources
Below is a list of further learning resources and reference material for $\LaTeX$ alongside guides on how you can get up and running with $\LaTeX$ quickly and easily.

- [#latex-help](https://discord.com/channels/268882317391429632/840667252793802752){: .mention target="_blank"} - The server channel for $\LaTeX$ help.
- [Overleaf Learn](https://www.overleaf.com/learn){:target="_blank"} - A high-quality and comprehensive set of guides and instructions using $\LaTeX$.
- [DeTeXify](https://detexify.kirelabs.org/classify.html){:target="_blank"} - A useful utility for finding symbols you don't know the command for. Uses OCR handwriting recognition to recommend a symbol.
- [Overleaf](https://www.overleaf.com){:target="_blank"} - An online cloud-based $\LaTeX$ editor. Free for personal use with additional paid features for collaboration and quality-of-life.
- [TeX Live](https://www.tug.org/texlive/){:target="_blank"} - A multiplatform $\LaTeX$ compiler.
- [CTAN](https://ctan.org/){:target="_blank"} - The Comprehensive $\TeX$ Archive Network, the canonical repository for $\TeX$ and $\LaTeX$ packages.

[^1]: Note that braces are not always *required* to pass arguments to macros. For example, both `\frac 1 2` and `\frac{1}{2}`, as well as `\mathbb N` and `\mathbb{N}`, produce the same output; nevertheless, in each case the latter style is customarily preferred.