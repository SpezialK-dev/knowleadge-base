# Reading inputs - none cannonical 
the goal is to get inputs without pressing enter when typing something. 
meaning we want unbuffered input, in my case I only care for linux. 

I thought an unbuffered input is the call it is not enough you are still waiting for an EOL -> what I am really is an Non-Canonical input processing apparently, this should take direct input from the console. 


## Possible sources
- [Stackoverflow input without enter press](https://stackoverflow.com/questions/421860/capture-characters-from-standard-input-without-waiting-for-enter-to-be-pressed)
- [Stackoverflow: unbuffered and buffered Stream](https://stackoverflow.com/questions/10518608/buffered-and-unbuffered-stream)
- [Man: setbuf](https://www.man7.org/linux/man-pages/man3/setbuf.3.html)
- [Man: STDIN]

### more on the none canonical things
- [pubs opengroup specification](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap11.html)
- [cannonical or not GNU](https://www.gnu.org/software/libc/manual/html_node/Canonical-or-Not.html)
- [Stackoverflow: Cannonical vs none cannonical](https://stackoverflow.com/questions/358342/canonical-vs-non-canonical-terminal-input)
- [terminos](https://www.man7.org/linux/man-pages/man3/termios.3.html)


[wikibooks: serial programming](https://en.wikibooks.org/wiki/Serial_Programming/termios)
## My solution to the problem 

I choose to write it in c cause why not so it should also work in c++ but you should pobably adapt it to c++ if you want to use it in prod code To fundamentally its the same

```c
#include <stdio.h>
#include <string.h>
#include <stdio.h>
#include <termios.h>
#include <unistd.h>



int main(){
  struct termios ttable;
  //disableing ICANON 
  ttable.c_cflag = -ICANON;
  ttable.c_cflag = -ECHO;
  //doing this for 0 stdin 
  tcsetattr(0, TCSANOW,&ttable );
  
  size_t size = 4095;
  char buf[size];
  // ensuring nulltermination
  buf[size-1] = '\0';
  while(1){
    read(0 ,&buf, size-1 );
    
  }
  }
```

the above code works and simply reads in without stoping, this is done for the input stream
# File descriptors 
[Man pages](https://www.man7.org/linux/man-pages/man3/stdin.3.html)


| name   | file descriptor ID |
| ------ | ------------------ |
| stdin  | 0                  |
| stdout | 1                  |
| stderr | 2                  |
