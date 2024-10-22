## Expressions in UPPAAL
Expressions are used with the following labels: 

### Select 
A select label contains a comma separated list of *name : type* expressions where *name* is a variable name and *type* is a defined type (built-in or custom). These variables are accessible on the associated edge only and they will take a non-deterministic value in the range of their respective types. 

### Guard
A guard is a particular expression satisfying the following conditions: it is side-effect free; it evaluates to a boolean; only clocks, integer variables, and constants are referenced (or arrays of these types); clocks and clock differences are only compared to integer expressions; guards over clocks are essentially conjunctions (disjunctions are allowed over integer conditions). A guard may call a side-effect free function that returns a bool, although clock constraints are not supported in such functions.

### Synchronisation 
A synchronisation label is either on the form `Expression!` or `Expression?` or is an empty label. The expression must be side-effect free, evaluate to a channel, and only refer to integers, constants and channels. 

### Update
An update label is a comma separated list of expressions with a side-effect; expressions must only refer to clocks, integer variables, and constants and only assign integer values to clocks. They may also call functions. 

### Invariant 
An invariant is an expression that satisfies the following conditions: it is side-effect free; only clock, integer variables, and constants are referenced; it is a conjunction of conditions of the form `x<e` or `x<=e` where `x` is a clock
reference and `e` evaluates to an integer. An invariant may call a side-effect free
function that returns a bool, although clock constraints are not supported
in such functions.

<script>
MathJax = {
  tex: {
    inlineMath: [["$", "$"], ["\\(", "\\)"]]
  }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
