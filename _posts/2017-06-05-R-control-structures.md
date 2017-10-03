---
layout: post
title: R control structures
author: CY
tags: [R]
categories: [R]
share: false
image:
  background: triangular.png 
---



### R control structure types  

- conditional execution             
  + if(condition){expression1} else{expression2}    
  + ifelse(condition, expression1, expression2)       
- loops              
  + repeat{ statements }                 
  + while(condition){ statements }      
  + for(index in object){ statements }        
  + (i)break: The keyword break breaks at once and exits from the loop.       
  + (ii)next: The keyword next jumps to the start of the next iteration in the loop      
- apply family             
  + apply(): applying functions on matrices or arrays       
  + lapply()
  + sapply()
  + tapply()


### apply family

| 函数           | 作用                                       |
| ------------ | ---------------------------------------- |
| apply(x,i,f) | 针对数据框(x)来说, 对各行(i = 1)或者各列(i = 2)进行(f)算法处理 |
| lapply(x,f)  | 针对列表(x)中的各个要素就行算法(f)处理, 结果以列表返还          |
| sapply(x,f)  | 针对列表(x)中的各个要素就行算法(f)处理, 结果以矢量返还          |

####  apply 
对数组或者矩阵的一个维度使用函数生成值得到列表, 数组或者向量    

```
apply(X, MARGIN, FUN, ...)

  X: an array, including a matrix
  MARGIN: 1 (rows), 2 (columns), c(1, 2) (rows and columns)    
  FUN: Functions
```
计算按照行(1)或列(2)的方式进行。           
如果apply函数命令应用到矩阵的每一个与元素上时，函数的运算顺序为：从第一列第一个数值到第一列最后一个数值，再从第一列到最后一列的顺序。请小伙伴们注意，这是函数的运算顺序。运算之后我们有了对矩阵全部数据的运算结果，结果排序为：当向量值为1的时候，每一列的运算结果变成新的一行，即第一列的运算结果变为第一行，第二列的运算结果变为第二行，以此类推直到最后一列的运算结果变为最后一行。


```r
m <- matrix(1:16, nrow = 4)
apply(m, 1, sqrt)
```

```
##          [,1]     [,2]     [,3]     [,4]
## [1,] 1.000000 1.414214 1.732051 2.000000
## [2,] 2.236068 2.449490 2.645751 2.828427
## [3,] 3.000000 3.162278 3.316625 3.464102
## [4,] 3.605551 3.741657 3.872983 4.000000
```

```r
apply(m, 2, sqrt)
```

```
##          [,1]     [,2]     [,3]     [,4]
## [1,] 1.000000 2.236068 3.000000 3.605551
## [2,] 1.414214 2.449490 3.162278 3.741657
## [3,] 1.732051 2.645751 3.316625 3.872983
## [4,] 2.000000 2.828427 3.464102 4.000000
```

#### lapply
通过对x的每一个元素运用函数，生成一个与元素个数相同的值列表    

#### sapply
是lapply 函数的包装版, 该函数返回结果是向量或者矩阵, 如果simplify="array", 且合适的情况下, 将会通过 simplify2array() 函数转换为阵列    

### ifelse 
`ifelse()` can be nested in many ways:
```
ifelse(<condition>, <yes>, <no>)         

ifelse(<condition>, <yes>, ifelse(<condition>, <yes>, <no>))

ifelse(<condition>, ifelse(<condition>, <yes>, <no>), <no>)

ifelse(<condition>, 
       ifelse(<condition>, <yes>, <no>), 
       ifelse(<condition>, <yes>, <no>)
      )

ifelse(<condition>, <yes>, 
       ifelse(<condition>, <yes>, 
              ifelse(<condition>, <yes>, <no>)
             )
       )
```












