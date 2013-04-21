% 550 400 
% Quiz 5 Topics 
% Date Apr 29, Monday


* interweaving your computation with your text
    * Know the correct solution to the odd numbered HW 4 problems
    * Rmd/\LaTeX\ commands 
        * Inserting a table using `Rmd` 
        * Inserting a figure 
            * using the usual `Rmd` command 
            * using `\centerline{ ... }` 
            * using `\begin{center} ... \end{center}` 
            * using `\includegraphics{ ... }` and changing the figure size 
        * referencing using `\ref{...}` together with `\label{...}` 
    * `R` commands
        * Inserting a figure 
            * directly/automatically after plotting (default behavior)
            * `ggsave` + \LaTeX\ command 
            * `pdf` + \LaTeX\ command
        * Inserting a table using `xtable`
        * R code block options 
            * `echo`/`eval`/`message`/`error`/`comment`
    * `pandoc` commands from `Rmd` to 
        * \LaTeX\-beamer 
            * directly to `pdf`
            * to `tex` and then `pdf`
            * for changing theme and colortheme
        * \LaTeX\-article `pdf`/`tex`
            * directly to `pdf` 
            * to `tex` and then `pdf`
        * MS-Words
            * directly to docx
