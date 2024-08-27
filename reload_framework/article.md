### **Getting Started with ncurses**

#### **1. creating your first `ncurses` program**
create a `main.c` or a `main.cpp` file and open it in your IDE of choice (i personally use vim and micro). copy the code below to your file:
```
#include<ncurses.h>
void main (){
  initscr();
  printw(" C is the fastest language");
  endwin ();
}
```
if you compile and run the program, you would see nothing. 
to compile; if you are using Visual studio or similiar IDE, add the ncurses library to the linker and click the run button. However since i am coding in my linux terminal i would just run:
```
gcc main.c -o main -lncurses
./main
```
so the program ran successful but no output, well first let's understand what each line of our program does.
- **`initscr()`**: This function initializes the `ncurses` environment. It sets up memory and prepares the terminal for `ncurses` mode. Without calling `initscr()`, none of the other `ncurses` functions will work.
- **`endwin()`**: This function ends the `ncurses` mode and returns the terminal to its normal mode. It’s crucial to call this function before your program exits, or the terminal may not return to its usual state.
- **`printw()`** is used to print a string to the screen.

...
the reason our Program doesn't do anything is because we did not call the `refresh()` function after our printw("String"). the `refresh()` is responsible for keeping the screen updated for what ever is to be displayed.
... However even after adding the `refresh()` we still wouldn't see anything because the program closes immediately and the human eye's is too slow to see what was displayed.
to ensure the program waits for us to finish seeing the output of our program we would add the `getch()` function after our refresh. this function `getch()` (get char) stops and waits for the user to press any key and then store the key value in memory before proceeding with the program, which then ends
... so now if you add `refresh()` and `getch()` to our main.c you should see the output:
// img Here
...
Here is another simple structure of an `ncurses` program:

```c
#include <ncurses.h>

int main() {
    initscr();            // Start ncurses mode

    printw("Hello, world!"); // Print message to the screen
    refresh();            // Refresh the screen to show the output
    getch();              // Wait for user input

    endwin();             // End ncurses mode
    return 0;
}
```

- **`initscr()`** is called first to initialize `ncurses`.
- **`printw()`** is used to print a string to the screen.
- **`refresh()`** updates the screen with the printed output.
- **`getch()`** waits for the user to press a key before exiting.
- **`endwin()`** ends `ncurses` mode.
<hr>
#### **2. Basic Screen Manipulations**


##### **Moving the Cursor: `move()`**

One of the things that make NCurses appeal to programmers is the control it
offers, not only can you control the text you display but also the location of the text (text position).
- **`move(y, x)`**: Moves the cursor to the position `(y, x)` on the screen. `y` is the row and `x` is the column.

Example:

```c
move(0, 8);    // Moves cursor to row 5, column 10
printw("I am Here!");  // Prints "Here!" at position (5, 10)
move(3,15);
printw("Now i am here!")
```
... we will discuss more on move in later chapters.
##### **Clearing the Screen: `clear()`, `clrtobot()`, `clrtoeol()`**

- **`clear()`**: Clears the entire screen.
- **`clrtobot()`**: Clears from the current cursor position to the bottom of the screen.
- **`clrtoeol()`**: Clears from the current cursor position to the end of the current line.

Example usage:

```c
clear();      // Clears the whole screen
move(5, 10);  // Moves cursor to row 5, column 10
printw("Text");
clrtobot();   // Clears from the cursor to the bottom of the screen
```

##### **Refreshing the Screen: `refresh()`**

- **`refresh()`**: After making any changes to the screen, you must call `refresh()` to update the terminal display. Without this, the changes will not appear.

<hr>
#### **3. Simple Output**

##### **`printw()`, `mvprintw()`, and `addch()` Functions**

- **`printw()`**: Similar to `printf()`, it prints a formatted string at the current cursor position.
  
  Example:
  ```c
  printw("Hello, %s!", "world");
  ```

- **`mvprintw(y, x, ...)`**: Combines `move()` and `printw()`. It moves the cursor to `(y, x)` and prints the string in one function call.
  
  Example:
  ```c
  mvprintw(3, 5, "Positioned Text");
  ```

- **`addch(ch)`**: Adds a single character `ch` at the current cursor position.
  
  Example:
  ```c
  addch('A');
  ```

##### **Handling Basic Input: `getch()`, `getstr()`**

- **`getch()`**: Waits for and returns a single character input from the user.

  Example:
  ```c
  int ch = getch();  // Waits for a key press and stores it in `ch`
  ```

- **`getstr()`**: Reads a string of characters from the user input and stores it in a buffer.

  Example:
  ```c
  char str[100];
  getstr(str);  // Reads a string and stores it in `str`
  ```

### **Putting It All Together**

Here’s a more complete example that combines everything:

```c
#include <ncurses.h>

int main() {
    initscr();              // Initialize ncurses
    clear();                // Clear the screen

    mvprintw(5, 10, "Enter your name: ");  // Prompt for input
    char name[50];
    getstr(name);           // Get the user input

    clear();                // Clear the screen again
    mvprintw(10, 10, "Hello, %s!", name);  // Display the entered name
    refresh();              // Refresh to show the output

    getch();                // Wait for a key press
    endwin();               // End ncurses mode
    return 0;
}
```

This simple program asks for the user’s name and then displays a greeting.

### **Conclusion**

The `ncurses` library is powerful for creating text-based user interfaces. With basic functions like `initscr()`, `printw()`, `getch()`, and `refresh()`, you can start building interactive programs in a terminal. Experiment with these functions to get comfortable, we will explore more advanced features like windows, colors, and key handling as you progress.