# Convert or Knit Notebook for Corporate

The product team is often asked to make a notebook for several materials in one complete pdf. Although the task sounds simple, it's really a pain in the ass to do it. You must first ensure what programming language is used for the company training.

## Using Python programming language

Refer to this [guideline](https://github.com/Litaa/convert-jupyter-to-rmd) to convert jupyter ipynb to rmd files.

> Note: if you get an error when you knit Rmd to pdf, try to block all the code with `ctrl + a` in jupyter.R and converter.R before running it. Make sure each variable appears in the rstudio env.

> Another Note: include **all** of the assets, data_inputs, scripts, etc in the `Rmd` folder

## Using R programming language

One step easier.

## Anticipate revise from BD team: YAML format

### 1. Ask example pdf from previous corporate training.

### 2. Title, author, date
```
---
title: 'Data Science in Python Specialization: PT XYZ'
author: "Algoritma"
date: "October, 2022"
---
```

### 3. Offside Code:
```
---
title: 'Data Science in Python Specialization: PT XYZ'
author: "Algoritma"
date: "October, 2022"
header-includes:
  \usepackage{fvextra}
  \DefineVerbatimEnvironment{Highlighting}{Verbatim}{breaklines,commandchars=\\\{\}}
output:
  pdf_document:
    toc: yes
    toc_depth: 4
    latex_engine: xelatex
---
```

### 4. Offside **Output** Code:
```
---
title: 'Data Science in Python Specialization: PT XYZ'
author: "Algoritma"
date: "December, 2022"
header-includes:
  \usepackage{fvextra}
  \DefineVerbatimEnvironment{Highlighting}{Verbatim}{breaklines,commandchars=\\\{\}}
output:
  pdf_document:
    toc: yes
    toc_depth: 4
    latex_engine: xelatex
    fig_caption: yes
    pandoc_args: --listings
    includes:
      in_header: preamble.tex
always_allow_html: true
---
```

Make `preamble.tex` and save in line (sejajar) with the Rmd file and contain the following:
```
\lstset{
  breaklines=true,
  basicstyle=\ttfamily
}
```


### 5. No space between subheading 4 and the next paragraph

xelatex doesn't read subheading 4 (####). make sure there is a `\hfill\\` between the title and the paragraph below it so that there is a space between them. 

Example:
```
#### Theory

\hfill\\

Logistic regression is a classification algorithm used to fit a regression curve, $y = f(x)$ ...
```
### 6. Page Break for new materials

To make a complete Table of Contents, you must copy all the codes and narration from each Rmd file into a one-big Rmd file. Ensure the first page of new materials is always on a new page. You can use `\newpage`.

Example:
```
## References

- [Prophet Documentation](https://facebook.github.io/prophet/docs/quick_start.html)
- [Paper: Forecasting at Scale](https://peerj.com/preprints/3190/)
- [Algoritma: Time Series Forecasting using `prophet` in R](https://business-forecasting.netlify.app/#5_time_series_forecasting_using_prophet)
- [Algoritma: Time Series Forecasting using `prophet` in Python](https://github.com/tomytjandra/tsf-prophet)

\newpage

# Neural Network and Deep Learning

**Coursebook: Neural Network and Deep Learning**

- Part 11 of Machine .......
```

## Error

### Error using modulo operator (%)

If you using modulo operator such as `%matplotlib inline` in Rmd, you can't.  In python a % is a modulo operator or a string formatter. The %magic_command comes from IPython, so what would be needed is to integrate IPython into the notebook. Not worth investing in.

Solution:
just comment the line.

### Text line contains an invalid character from Output results

```{python echo=T, results='hide'}
```{python echo=T, results='hide'}


```
### Error unicode

use xelatex engine.
```
---
title: 'Data Science in Python Specialization: PT XYZ'
author: "Algoritma"
date: "October, 2022"
output:
  pdf_document:
    toc: yes
    toc_depth: 4
    latex_engine: xelatex
---
```
