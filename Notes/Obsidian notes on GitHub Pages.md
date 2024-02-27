## Obsidian notes on GitHub Pages

### Transform Wikilinks to Markdown links
By default Obsidian uses Wikilink format for links inside of documents. They are rendered as a plain text in regular Markdown. 

### Transform links to relative path format
Obsidian knows where to search for linked documents even if only their names are given. It creates a hidden directory inside the root directory for notes where it probably has some kind of lookup table. GitHub doesn't know where to look for the files and will always check current directory if instructed otherwise.

### Add note titles
Note titles that are rendered in Obsidian as H1 headers will not appear in Markdown documents rendered by GitHub Pages. Add note title in Obsidian as H2 using two '#' directly under the default title.

### Separate paragraphs with new line
When starting a new header  in Obsidian there will always be space rendered directly above it. This is not the case in Markdown used by GitHub Pages. Not only there will not be a space above header, but a header can become indented if there is a header or a bullet list above it.

### README.md links to all resources
Define links in README.md to all the resources that should be exposed to the viewer. README.md must be placed in the root directory of the GitHub repository and at the root directory of Obsidian notes at the same time. Do not make sublists in subdirectories and then try to unpack them in README.md as this will not work because of the relative file paths.

### MathJax is not supported
MathJax is not supported natively by GitHub Pages. This means that math formulas constructed using single or double '$' signs will not be rendered but displayed as plain text.
<script>
MathJax = {
  tex: {
    inlineMath: [["$", "$"], ["\\(", "\\)"]]
  }
};
</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
