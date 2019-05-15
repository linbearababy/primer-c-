# write ahead 
For this week I want to learn some useful ways or functions in c++.

# cin & cout
There are some rounding issues here so be careful! To make the km calculations, use the constants (speed and distance) provided. To make the mile calculations, use the constants (speed and distance) provided. To make the round trip calculation, use your distance in km and the speed of light constant provided. You'll get slightly different answers if you try to convert the two distances or the two speeds.

You will need to work with the cin and cout streams and their operators >> (for cin) and << (for cout). You will also need to declare the appropriate variables: long (a 64 bit integer) for values like days and double for calculation values.

cout takes either variable values or strings (between " ") and outputs them to the console. You can use multiple << operators on the same cout stream, usually ending with endl. Assuming the variable int_var has the value 23:
      std::cout << "This is a string: " << int_var << " the end"
          << std::endl;
would output:
      This is a string: 23 the end
      
      
cin will input a value from the command line into a variable of a particular type. It does so until it hits a space (space separated values) or an end of line. For example:

       std::cin >> int_var;
If you enter a value on the command line, an integer, it will be read into the variable (no conversion required).

      int multiplier, number;
      std::cin >> number;
      std::cin >>  multiplier;
      std::cout << "The number " << number << " times "<< multiplier
                << " is " << number * multiplier << std::endl;
With inputs 10 and 2 respectively, you would get:
      The number 10 times 2 is 20

The operations on these numbers are, respectively: + (sum), - (difference), * (product), / (division) and % (remainder, integer only). The last two deserve special comment.

If an integer is divided by another integer, the result is an integer. Thus the result of 6/4 is 1. In contrast, 6.0/4 is 1.5. That is, the / operation results in the integer quotient if using integers, floats if using floats. The result of 6%4 is the integer remainder of the division, thus 2 (6 divided by 4 is 1 with a remainder of 2). There is no equivalent for % in floating point math.

provide 2 decimal points of accuracy using std::fixed and std::setprecision (the later requiring #include<iomanip>). You would use them as follows:
      
      std::cout << std::fixed;
      std::cout << std::setprecision(2);
      

# The Files
extra.cpp : It defines the function extra which will be used in the main program.

extra.h : This is the header file. Notice that is only really provides the declaration of the function.
      In the declaration, the names of the parameters are not required, only their types.
      Note that the function declaration ends in a ; (semicolon). Don't forget!!!
      There are some weird # statements, we'll get to that.
main.cpp : This is the main program. Notice that it has the following statement in it:

#include "extra.h"
This means that the main program is "including" the declaration of the function so that the compiler may check the type use of extra by main. Notice the quotes. When the include uses quotes, it is assumed that the .h file is in the same directory as the other files. Includes with <> means get the includes from the "standard include place". Since it is our include file, we need to use quotes for it.

# Function split
The split function should take in a string and return a vector<string> of the individual elements in the string that are separated by the separator character (default ' ', space). Thus: "hello mom and dad" → {"hello", "mom", "and", "dad"}

Open functions.h and store the function declaration of split there. The declaration should be:

                 vector<string> split (const string &s, char separator=' ');
As discussed in lecture, default parameter values go in the header file only. The default does not occur in the definition if it occurred in the declaration.
This header file should wrap all declarations using the #ifndef, #define, #endif as discussed above. Make up your own variable.
Open functions.cpp and write the definition of the function split. Make sure it follows the declaration in functions.h. The parameter names do not matter but the types do. Make sure the function signature (as discussed in lecture) match for the declaration and definition.
You can compile functions.cpp (not build, at least not yet) to see if functions.cpp is well-formed for C++. It will not build an executable, but instead a .o (object) file. The object file is the result of compilation but before building an executable, an in-between stage.
      

# Function print_vector
This function prints all the elements of vector<string> v to the ostream out provided as a reference parameter (it must be a reference). Note out and v are passed by reference.

      print_vector : Store the function print_vector in functions.cpp, put its declaration       in functions.h. It should look a lot like the below:
      
      void print_vector (ostream &out, const vector<string> &v);
compile the function (not build, compile) to make sure it follows the rules.





