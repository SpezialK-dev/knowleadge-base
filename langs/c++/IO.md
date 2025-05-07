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

## My solution to the problem 

I choose to write it in c cause why not so it should also work in c++ but you should pobably adapt it to c++ if you want to use it in prod code To fundamentally its the same

```c

```