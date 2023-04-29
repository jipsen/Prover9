# Prover9

The file Prover9.py contains some additional code for the Python interface to Prover9/Mace4 provided by the `provers` package https://pypi.org/project/provers/ on PyPI.

The provers package works well on https://colab.research.google.com, so to use it, go to the Colab site, login with a Google account, copy the following commands into a new Colab notebook cell and run them (takes about 30 seconds to compile Prover9):

```
!pip install provers
!rm -rf Prover9 #remove any previous version
!git clone https://github.com/jipsen/Prover9.git
from provers import *; execfile("/content/Prover9/Prover9.py")
```

Then you can define a first-order theory using a Python list of string with standard Prover9 syntax (as described in https://www.cs.unm.edu/~mccune/prover9/manual/2009-11A/ under Clauses and Formulas). E.g. you can copy the following commands into a notebook cell and run them to see how it works.

```
%%time
Monoids=[        #list axioms for monoids
"(x*y)*z=x*(y*z)",
"x*1=x",
"1*x=x",
]
a=p9(Monoids,[],100,0,[5])   #search up to 100 seconds for all monoids of cardinality <= 5 (up to isomorphism)
a[4] #show all monoids of cardinality 4
```

To prove some result, try the following command:

```
p9(Mon+["x'*x=1"],["x*x'=1"],0,100)  # a monoid with left inverses is a group; search 0 sec for counter_ex, 100 sec for proof
```

To export an algebra to the Universal Algebra Calculator (UACalc) format, use the following:

```
a=p9(Monoids,[],100,0,[5])   #search up to 100 seconds for all monoids of cardinality <= 5 (up to isomorphism)
print(uacalc_format(a[4][0],"A"))
```

The output can be copied into a text file with the extension ".ua" and this file can then be opened in UACalc (see uacalc.org for information about how to install and use UACalc).
