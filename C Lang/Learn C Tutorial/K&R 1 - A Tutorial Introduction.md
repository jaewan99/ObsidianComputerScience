


 https://www.cc4e.com/lessons/tutorial#


- [1:55:36](https://www.youtube.com/watch?v=PaPN51Mm5qQ#t=1:55:36.79) 
- String in C, they are array of characters
	-  there is no length - with loop until the "0" ("\n"

- [1:59:14](https://www.youtube.com/watch?v=PaPN51Mm5qQ#t=1:59:14.77) 
- Exercise 1-17



- [2:00:51](https://www.youtube.com/watch?v=PaPN51Mm5qQ#t=2:00:51.52) 
- Start of the chapter 1 



- [2:26:48](https://www.youtube.com/watch?v=PaPN51Mm5qQ#t=2:26:48.46) 
1.3 For statement

The choice between `while` and `for` is arbitrary, based on what seems clearer. The `for` is usually appropriate for loops in which the initialization and re-initialization are single statements and logically related, since it is more compact than `while` and keeps the loop control statements together in one place.

````C
#include <stdio.h>

main() /* Fahrenheit-Celsius table */
{
    int fahr;

    for (fahr = 0; fahr <= 300; fahr = fahr + 20)
        printf("%4d %6.1f\n", fahr, (5.0/9.0)*(fahr-32));
}


````



- [2:29:25](https://www.youtube.com/watch?v=PaPN51Mm5qQ#t=2:29:25.78) 
1.4 Symbolic Constants



- [2:32:06](https://www.youtube.com/watch?v=PaPN51Mm5qQ#t=2:32:06.89) 
1.5 A collections of useful program

````C
#include <stdio.h>

main() /* Fahrenheit-Celsius table */
{
    int c;
    
    while ((c = getchar()) != EOF)
	    putchar(c);
}
/* Typing -1 sends the characters - and 1, not the EOF signal. So this will not work */


````
