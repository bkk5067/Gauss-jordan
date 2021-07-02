# Gauss-jordan
Solving linear equations using python
import numpy as np
import pandas as pd
np.set_printoptions(linewidth=np.inf) 
#The following function calculates the solution of linear equation.
def gssjrdn(a,b):
    a= np.array(a, float)   #Matrix which is created using left hand side of linear equations.
    b= np.array(b, float)    #Matrix which is created using right hand side of linear equations.
    n= len(b)                #No. rows in matrix i.e. number of unknowns
    out=open("gauss_jordan.out.txt","w")  # For creating output file in txt format
    #Printing Initial matrix a and b
    print("\nInitial Matrix a:\n",file=out)
    print(a,file=out)  
    print("\nInitial Matrix b:\n",file=out)
    print(np.matrix(b).T,file=out)
    
   #main loop
   
    for k in range(n):
        #partial Pivoting
        if np.fabs(a[k,k])<1.0e-12:     #If digonal element is zero
            for i in range(k+1,n):
                if np.fabs(a[i,k])>np.fabs(a[k,k]):
                    for j in range(k,n):
                        a[k,j],a[i,j]=a[i,j],a[k,j]  #Interchanging the row so the diagonal element will not be zero
                    b[k],b[i]=b[i],b[k]
                    break
                
       #Division of the pivot row
        pivot = a[k,k]
        for j in range(k,n):   
            a[k,j]/= pivot
        b[k]/= pivot
        
        #Elimination loop
        for i in range(n):
            if i==k or a[i,k]==0:  continue  #If non diagonal element is zero conitinue without any change
            factor=a[i,k]
            for j in range(k,n):
                a[i,j] -= factor*a[k,j]  #For non diagonal elements converting into zero
            b[i]-=factor*b[k]
            
         
               
        print("\nMatrix a:\n",file=out)  #Printing matrix a after each iteration
        print(df.round(3),file=out)
        print("\nMatrix b:\n",file=out)  #Printing matrix b after each iteration
            
        print("   b0","  "*4,file=out)
        print(np.matrix(b).T.round(3),file=out)

    print(" \nThe solution vector:",file=out)
    print(b.round(3),file=out)  #For getting solution upto 3 decimals
    print(" \nThe transformed [a]:",file=out)
    print(a.round(3),file=out)  #For getting solution upto 3 decimals
    out.close()
    return a,b
