
# Reading files 
an [GeeksforGeeks](https://www.geeksforgeeks.org/c-program-to-read-contents-of-whole-file/) refernce


```c
#include <stdio.h> 
#include <stdlib.h>   
//...

FILE * filptr = fopen("pathToFile", "R")

while ((ch = fgetc(filptr)) != EOF)
	printf("%c", ch);

fclose(filptr)
//...
```
this reads out a single charackter though you could also use  fgetc() to read an entire line
fread() can read entire blocks of a file.  


if you want to read a long string from input you might also want to use fgets / fopen 

