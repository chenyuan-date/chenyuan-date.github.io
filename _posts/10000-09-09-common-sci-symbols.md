---
layout: post
title: Commonly used scientific symbols in pandoc markdown
author: CY
tags: [English]
categories: [English]
share: false
image:
  background: triangular.png 
---





### Commonly used scientific symbols in pandoc markdown





per mille sign    
* plain text: ‰ (doesn't render properly in PDF)
* HTML: `&permil;`  (renders properly in PDF) 
* LaTeX: `$\text{\textperthousand}$` (renders properly in PDF) 

delta sign   
* plain text: δ (doesn't render properly in PDF)
* LaTeX: `$\delta$` (renders properly in PDF) 

plus-minus sign   
* plain text: ±  (doesn't render properly in PDF) 
* HTML: `&plusmn;`  (renders properly in PDF) 
* LaTeX: `$\pm$`  (renders properly in PDF) 

degree sign   
* plain text:  °  (doesn't render properly in PDF) 
* HTML:  `&deg;`    (renders properly in PDF) 
* LaTeX:  `$\text{\textdegree}$` (renders properly in PDF) 

subscript    
* surround with one tilda one each side (~): `CO~2~` for subscript

superscript   
* surround with one hat on each side (^): `E=mc^2^` for superscript

more on super/sub-scripts: http://johnmacfarlane.net/pandoc/README.html#superscripts-and-subscripts
