This is just a general cheat sheet to note down things that I have learned.


# newline in echo cmd
since \\n is not valid. 
[Source of answer](https://stackoverflow.com/questions/132799/how-can-i-echo-a-newline-in-a-batch-file)

answer using multible echos 

# if else 

```sh
if[ conditio];then
	<code>
else
	<code>
fi
```


# setting a variable to the output of a cmd 
usefull in conjunction with things like pwd or other uses 

```sh
variable=$(<cmd>)
```
