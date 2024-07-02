## Verifying properties in UPPAL
- **`E<> p`** : there exists a path where **p** eventually holds. 
- **`A[] p`** : for all paths **p** always holds. 
- **`E[] p`** : there exists a path where **p** always holds.
- **`A<> p`** : for all paths **p** will eventually hold.
- **`p --> q`** : whenever **p** holds **q** will eventually hold.
where **p** and **q** are state formulas like for example `(P1.cs and x<3)`.

Note the useful special form **`A[] not deadlock`** that checks for deadlocks.
<script>
MathJax = {
  tex: {
    inlineMath: [["$", "$"], ["\\(", "\\)"]]
  }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
