### Formatting text and Coloring
### Colors
ncurses comes with different function to apply colors to characters in your terminal, but first you would have to make sure your terminal supports color (all terminals does these days).
<hr>
to check if your terminal supports colors you will use The `has_colors()` function. which returns a logical TRUE if the terminal is able to
display colored text, FALSE otherwise. (Both TRUE and FALSE are defined in
NCURSES.H, so don’t fret over them or redefine them in your code.)
```c
#include<ncurses.h>
int main(){ 
	initscr();
	if (has_colors()){
		printf("Colors: True");
		continue;
	} else{
		printf("Colors: False");
		exit(0);
	}
	printw(“NCurses reports that you can use %d colors,\n”,COLORS);
	printw(“and %d color pairs.”,COLOR_PAIRS);
	refresh();
	getch();
	endwin();
}
```

#### Here’s the output I see on my computer:
Colors: True!
NCurses reports that you can use 8 colors,
and 64 color pairs. 

... Note the use of the COLORS and COLOR_PAIRS. These constants are set
when start_color() checks to see how many colors are available to the terminal, as well as how much space is left for storing color information in the NCurses attr_t variable type. The next section explains the difference between COLORS and COLOR_PAIRS.

### Colors and Color Pairs 
The COLORS and COLOR_PAIRS constants report how many col-
ors the terminal can display and how many color combinations can be defined (foreground +
background ).
The typical PC reports only eight colors available. These are the standard eight
text colors used on PCs since the first IBM PC color graphics adapter set the
standard back in 1981. The colors are listed in Table 3-2, along with their
NCurses constant names and values.