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

## Script does not work with > 

If you encounter a script not properly working when being piped out to a file with 

```sh
sh foo.sh > foo.txt
```

then we can use the following command and it might work at least when the previous one had given me trouble this worked

```sh
sh foo.sh | tee foo.txt
```