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
