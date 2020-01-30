

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```
Get packages installed and loaded

Optimzing means max or min of something (usually money, could be clinicans)

Objective function: this contains deciions variables that take the values defined by the constraits (so number of clients is 30 per day)

Cost coeiffients are affected by 
Constrcinst are a so a*x (decision variable like number of clients) must be equal to less than some constraint

Contraisnts are like no more than 2 clincians each day
```{r}
library(lpSolve)
library(Rglpk)
library(Rsymphony)
```

Test example
```{r}
library (lpSolve)
#defining parameters
obj.fun <- c(20,60)
constr <- matrix (c(30 , 20, 5, 10, 1, 1) , ncol = 2, byrow =
TRUE)
constr.dir <- c("<=", "<=", ">=")
rhs <- c(2700 , 850 , 95)
#solving model
prod.sol <- lp("max", obj.fun , constr , constr.dir , rhs ,
compute.sens = TRUE)
prod.sol

```
My example
Min = staff * (.5 no show rate)
Constraints: 
must have at least 2 clincians 
No more than 8 clincians
```{r}
obj.fun_staff <- c(.5)
constr_staff <- matrix (c(1,1) , ncol = 1, byrow =
TRUE)
constr.dir_staff <- c(">=", "<=")
rhs_staff <- c(3,8)
#solving model
prod.sol_staff <- lp("min", obj.fun_staff , constr_staff , constr.dir_staff , rhs_staff ,
compute.sens = TRUE)
prod.sol_staff$solution

```

