`#include <ncurses.h>`
You must include the NCURSES.H header file so that the compiler doesn’t
choke on your NCurses functions.
NOTE Please note that including the NCURSES.H header file does not
automatically link in the NCurses library. No, you must do that with the
–lncurses switch when you compile (as covered in Chapter 1). There is a
difference between the header and library files!
The NCurses header file does a few nifty tricks. First, it automatically
includes the following other header files:
stdio.h
unctrl.h
stdarg.h
stddef.h
Therefore, there is no need to re-include these header files in your source
code. In fact, if you do, you may end up slowing things down and creating files
much larger than they need to be. So if you’re tempted to do this:
#include <stdio.h>
#include <ncurses.h>
Do only this instead:
#include <ncurses.h>
Also, the NCURSES.H file defines such things as TRUE, FALSE, OK, ERR, and
other useful constants. It contains definitions for structures you’ll be using
later. Plus, it includes many other wonderful and useful goodies. If you have
the time, peruse the header file, which can be found at /USR/INCLUDE/
NCURSES.H.