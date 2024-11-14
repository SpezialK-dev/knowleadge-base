# How to create makefiles 


## Rubber
If you want to create a makefile with latex, it creates some problems 
you will need to fully know all the steps you want to do. To have a simpel file where you dont want to do a whole lot. You should use [rubber](https://launchpad.net/rubber/). 
This makes it quite simpel to create a simpel makefile.


```makefile 

func: 
	rubber --pdf texfile
```

as simple as this and you have a basic working makefile 

## LatexMk
also exists but I have not looked at it 
