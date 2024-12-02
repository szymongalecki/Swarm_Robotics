## Guarded commands
The guard is a proposition, which must be true before the statement is executed. The use of guarded commands makes it easier to prove the program meets the specification. The statement is often another guarded command. 

"So-called 'guarded commands' are introduced as a building block for alternative and repetitive constructs that allow nondeterministic program components for which at least the activity evoked, but possibly even the final state, is not necessarily uniquely determined by the initial state." 
**~ Edsger W. Dijkstra - "Guarded Commands, Nondeterminacy and Formal Derivation of Programs"**

### Syntax
A guarded command is a statement of the form $G \rightarrow S$, where
- $G$ is a proposition, called the guard
- $S$ is a statement

### Semantics
At the moment $G$ is encountered in a calculation, it is evaluated
- If $G$ is true, execute $S$
- If $G$ is false, look at the context to decide what to do (in any case, do not execute $S$)

### Selection: if
The selection is a list of guarded commands, of which one is chosen to execute. If more that one guard is true, one statement whose guard is true is nondeterministically chosen to be executed.
```
if G0 → S0
 □ G1 → S1
...
 □ Gn → Sn
fi
```

### Repetition: do
Execution of the repetition consists of executing 0 or more iterations, where an iteration consists of nondeterministically choosing a guarded command  $G_i \rightarrow S_i$  whose guard $G_i$ evaluates to true and executing the command $S_i$. Thus, if all guards are initially false, the repetition terminates immediately, without executing an iteration.
```
do G0 → S0
 □ G1 → S1
...
 □ Gn → Sn
od
```


<script>
MathJax = {
  tex: {
    inlineMath: [["$", "$"], ["\\(", "\\)"]]
  }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
