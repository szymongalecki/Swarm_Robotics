Progress:
- I removed the strict synchronisation from the model
- Now the robot transitions are not forced by a single clock
- Each robot has its own clock
- Unfortunately the values of the clock do not make sense for all robots
- For `n` robots, only `n-1` clocks are used
- Implementation in **alpha_algorithm_int_invariant.xml**
- Issue described in [Recreating alpha algorithm in UPPAAL pt.2](../Notes/Recreating%20alpha%20algorithm%20in%20UPPAAL%20pt.2.html)
- Additionally I managed to export trace from concrete simulator
- Trace is a JSON like object with all the transitions and variable values including clocks

Formal:
- I updated the research project problem statement to the corrected version
- I uploaded the master thesis problem statement to the learnIT page created for second attempt (it needs approval before 24 June)

Organisational:
- I am leaving for vacation and I won't be able to attend meetings on 
	- 12 June
	- 19 June
- Because I still have to work to make SU this month I won't be able to attend meeting on:
	- 26 June
<script>
MathJax = {
  tex: {
    inlineMath: [["$", "$"], ["\\(", "\\)"]]
  }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
