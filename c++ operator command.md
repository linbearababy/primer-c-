# Learning about the terminal
Many tasks can only be performed at the terminal (or are easier to perform at the terminal), so becoming comfortable there is important. Many of the classes after this one will expect at least a basic familiarity of the command line, so pay special attention to these sections.

Log into Mimir and open the IDE. Use the terminal in Mimir's IDE to follow along.

# pwd
The first command you need to learn is one of the simplist, pwd. At the terminal, type the command pwd and hit enter.

pwd is short for "print working directory". It outputs the path of the working directory, the directory your terminal currently has open. If you get lost (and it is easy to do with only the text-based terminal for navigation), pwd can show you where you are.


PWD
你需要学习的第一个命令是简单的pwd之一。在终端上，输入命令pwd并按Enter键。

pwd是“打印工作目录”的缩写。它输出工作目录的路径，即终端当前打开的目录。如果你迷路了（并且很容易只使用基于文本的导航终端），pwd可以告诉你你在哪里。

# ls
The ls command outputs the names of all of the folders and files in the working directory. ls is short for "list" (as in "list" the contents).

Folder names end with a /, file names do not. Some terminals also add colorized output to ls to denote different types of files. For instance, Mimir's terminal has folders in blue, and files in white.

LS
ls命令输出工作目录中所有文件夹和文件的名称。 ls是“list”的缩写（如“list”中的内容）。

文件夹名称以/结尾，文件名不以。 一些终端还将颜色输出添加到ls以表示不同类型的文件。 例如，Mimir的终端有蓝色文件夹和白色文件。

# cd
The cd command is short for "change directory". It allows you to change your working directory to some different folder.

Lets say you run pwd and you get the output of:

/home/joshua/cse_232__summer_2017/lab01_new_horizons
Your current working directory is named "lab01_new_horizons". If you run ls, you would get:

lab01/
This means there is only one thing in this folder, a subfolder called "lab01". If you wanted to do things in that subfolder, you would use the cd command like so:

cd lab01
Now you are in the folder named "lab01", you can confirm such with pwd and ls

光盘
cd命令是“更改目录”的缩写。 它允许您将工作目录更改为某个不同的文件夹。

让我们说你运行pwd，你得到的输出：

/家庭/约书亚/ cse_232__summer_2017/ lab01_new_horizons
您当前的工作目录名为“lab01_new_horizons”。 如果你运行ls，你会得到：

lab01/
这意味着此文件夹中只有一个东西，一个名为“lab01”的子文件夹。 如果你想在那个子文件夹中做一些事情，你可以像这样使用cd命令：

cd lab01
现在您位于名为“lab01”的文件夹中，您可以使用pwd和ls确认

# Special Directory Names
There are a few "special" directory names that you need to know. The first is the home directory. This directory's name is usually the username of the account, and it contains all of the user's files and folders. Inside the home folder is the "Desktop" folder (for all the things on your desktop), the "Downloads" folder and other folders as well (like "Music", "Videos", "Applications", etc.). The home folder is often specified using the tilde symbol (~). So if you want to cd to your home folder, run:

cd ~
Note: On most systems, running cd with no arguments also takes you to the home folder.

Sometimes you want to go the the parent folder of your working directory. In the example above, we moved from the folder "lab01_new_horizons" to its subfolder "lab01". Trying to get back by running:

cd lab01_new_horizons
would fail, because there is no folder named "lab01_new_horizons" in "lab01".

The way to go to the parent directory (in this case "lab01_new_horizons"), you need to run:

cd ..
The .. is a strange way to symbolize the parent directory. In fact, . denotes the working directory, a fact that will be useful to know in later labs.

The last "special" directory is the root directory. The root directory is the directory that is the ultimate parent of all the other directories on the computer. It is denoted by the single / symbol. In fact, you can specify any folder on the computer by starting with the root directory and working your way to the directory you actually want. So the path /home/joshua/cse_232__summer_2017/lab01_new_horizons specifies that the folder I want is:

In the root folder (the starting /)
In the folder named "home"
In the folder named "joshua"
In the folder named "cse_232__summer_2017"
And it is named "lab01_new_horizons"

特殊目录名称
您需要了解一些“特殊”目录名称。第一个是主目录。此目录的名称通常是帐户的用户名，它包含所有用户的文件和文件夹。在主文件夹内是“桌面”文件夹（适用于桌面上的所有内容），“下载”文件夹和其他文件夹（如“音乐”，“视频”，“应用程序”等）。通常使用波形符号（〜）指定主文件夹。因此，如果您想要cd到您的主文件夹，请运行：

cd~
注意：在大多数系统上，运行不带参数的cd也会将您带到主文件夹。

有时您想要转到工作目录的父文件夹。在上面的示例中，我们从文件夹“lab01_new_horizons”移动到其子文件夹“lab01”。试图通过运行回来：

cd lab01_new_horizons
会失败，因为“lab01”中没有名为“lab01_new_horizons”的文件夹。

转到父目录的方式（在本例中为“lab01_new_horizons”），您需要运行：

cd ..
..是一种象征父目录的奇怪方式。事实上， 。表示工作目录，这在以后的实验中有用。

最后一个“特殊”目录是根目录。根目录是计算机上所有其他目录的最终父目录。它由单个/符号表示。实际上，您可以通过从根目录开始并指向您实际需要的目录来指定计算机上的任何文件夹。所以路径/ home / joshua / cse_232__summer_2017 / lab01_new_horizons指定我想要的文件夹是：

在根文件夹中（起始/）
在名为“home”的文件夹中
在名为“joshua”的文件夹中
在名为“cse_232__summer_2017”的文件夹中
它被命名为“lab01_new_horizons”


# file
# cp 
The cp command "copies" files from one path (location) to another. The cp is used with two arguments:

The source file: This is the file you want to copy.
The destination file: This is where you want your copy to be placed
You copy files that are in you working directory or by specifing a path to the file. Examples:

cp a.txt b.txt           # This copies a.txt into a file called b.txt

cp ../c.txt ../../c.txt
. This copies c.txt (which is in the parent folder) to a file called c.txt (which is in the grandparent folder)

cp ~/Downloads/d.txt .
. This copies the d.txt file in my Downloads folder to the current directory
. If you specify a directory as a destination, it will create a file with the same name there.
The cp can also copy directories if you use the -r flag. The "r" stands for recursive, meaning to copy the directory and all sub-directories of it. Example:

cp -r other other2 # copies the directory "test" into a directory called "test2"
Save the file (lab02_folder.zip) to your Desktop. You may need to right click the link and select "Save Link As ..."
Right click the zipped file on the Desktop and select "Extract Here". You should now have a folder called "lab02_folder" on your Desktop now.
Change directories to the Desktop (cd ~/Desktop).
cd to the folder named "lab02_folder", then to the subfolder named "b_folder", then to the folder named "start".
If you run ls, you should see a folder named "other" and a file named "f.txt".
Copy the file named "f.txt" to the file "f2.txt".
Copy the folder named "a_folder" to the working directory. The "a_folder" is in the same folder as "b_folder".

CP
cp命令将文件从一个路径（位置）“复制”到另一个路径。 cp使用两个参数：

源文件：这是您要复制的文件。
目标文件：这是您希望放置副本的位置
您复制工作目录中的文件或指定文件的路径。例子：

cp a.txt b.txt＃将a.txt复制到名为b.txt的文件中

cp ../c.txt ../../c.txt
＃将c.txt（位于父文件夹中）复制到名为c.txt的文件（位于祖父文件夹中）

cp~ / Downloads / d.txt。
＃这会将Downloads文件夹中的d.txt文件复制到当前目录
＃如果指定目录作为目标，它将在那里创建一个具有相同名称的文件。
如果使用-r标志，cp也可以复制目录。 “r”代表递归，意味着复制目录及其所有子目录。例：

cp -r other other2＃将目录“test”复制到名为“test2”的目录中
将文件（lab02_folder.zip）保存到桌面。您可能需要右键单击该链接并选择“将链接另存为...”
右键单击桌面上的压缩文件，然后选择“Extract Here”。您现在应该在桌面上有一个名为“lab02_folder”的文件夹。
将目录更改为桌面（cd~ / Desktop）。
cd到名为“lab02_folder”的文件夹，然后到名为“b_folder”的子文件夹，再到名为“start”的文件夹。
如果运行ls，则应该看到名为“other”的文件夹和名为“f.txt”的文件。
将名为“f.txt”的文件复制到文件“f2.txt”。
将名为“a_folder”的文件夹复制到工作目录。 “a_folder”与“b_folder”位于同一文件夹中

# mv
The mv command is short for move and is identical to cp, except the original source doesn't exist after if is moved to the destination. Also, mv doesn't need the -r flag to move folders, it is happy to move folders just like files. Example:

mv other other2
Run the above command, and confirm the the "other" folder no longer exists, and there's now a "other2" folder present. Be sure your working directory is the "start" folder.

The mv command is often used to rename directories and folders.

MV
mv命令是move的缩写，与cp相同，除了在移动到目标之后原始源不存在。 此外，mv不需要-r标志来移动文件夹，它很高兴像文件一样移动文件夹。 例：

另外其他2
运行上面的命令，并确认“other”文件夹不再存在，现在有一个“other2”文件夹。 确保您的工作目录是“开始”文件夹。

mv命令通常用于重命名目录和文件夹。

# rm
The rm command is short for remove (delete). WARNING: files deleted with rm are effectively gone forever. They don't go to the TrashCan/RecycleBin. So please be careful with rm.

The rm command takes one argument: the file or folder you wish to delete. Note: if you wish to delete a folder, you need to supply the -r flag. Example:

rm f.txt # Deletes the file f.txt
rm -r a_folder # Deletes the folder a_folder and everything within it.

R M
rm命令是删除（删除）的简称。 警告：用rm删除的文件实际上已经永远消失了。 他们不会去TrashCan / RecycleBin。 所以请小心rm。

rm命令采用一个参数：您要删除的文件或文件夹。 注意：如果要删除文件夹，则需要提供-r标志。 例：

rm f.txt＃删除文件f.txt
rm -r a_folder＃删除文件夹a_folder及其中的所有内容。

# Pagers
Often, you want to be able to view files in the terminal (instead of opening them in a text editor like Atom or gedit). There are a few ways view files from the terminal.

# cat
The command cat is short for concatenate, which means to link things together. The cat program is often used to link the output from one program to the input from another. But another useful trait of cat is to output the contents of a file to the terminal. Invoking the cat program is quite simple:

cat some_file_name.txt
The above command will print the contents of the file to the terminal. However, for large files, cat is not very user-friendly. Instead, you should use a pager.

猫
命令cat是连接的缩写，这意味着将事物链接在一起。 cat程序通常用于将一个程序的输出链接到另一个程序的输入。 但cat的另一个有用特性是将文件的内容输出到终端。 调用cat程序非常简单：

cat some_file_name.txt
上面的命令会将文件的内容打印到终端。 但是，对于大文件，cat不是非常用户友好。 相反，您应该使用寻呼机。

# less
Pagers are programs that show you content one page at a time. They are useful for viewing large files (files to big to fit in the terminal window). The most popular pager is called less because it was derived from a program called more, computer science history is a little silly. You can invoke the less program like so:

less some_file_name.txt
To go the the next page, push the f key (forward). To go back a page, push the b key (backwards). To quit the pager and return to the command line, push q (use your imagination for why it is the q key).

减
寻呼机是一次向您显示一页内容的程序。 它们对于查看大文件（文件大到适合终端窗口）非常有用。 最受欢迎的寻呼机被称为较少，因为它来自一个名为more的程序，计算机科学历史有点傻。 您可以像这样调用less程序：

少some_file_name.txt
要转到下一页，请按f键（向前）。 要返回页面，请按b键（向后）。 要退出寻呼机并返回命令行，请按q（使用您的想象力来解释为什么它是q键）。

# Help
There are a few programs that are intended to provide documentation on the programs install on your computer. However, they are often difficult to understand, especially for a beginner. You invoke them by typing the help program and the name of the program you want information about. They may open up a pager if the entry is long.

# help
This command is used to provide information about bash, which is the language the terminal is running.

# man
This command (short for manual) is used to retrieve the documentation about the programs installed on the computer.

# info
This command is an alternate to man, often used by unix distributions.

Examples:

      help cd
      
救命
此命令用于提供有关bash的信息，bash是终端运行的语言。

人
此命令（手动简称）用于检索有关计算机上安装的程序的文档。

信息
此命令是man的替代命令，通常由unix发行版使用。

例子：

帮助cd
信息ls
男人python3
-H
如果使用-h标志调用程序，许多程序将为您提供一些关于自己的文档（比如它们接受的参数）。 例：

python -h

      info ls
      man python3
#-h
Many programs will give you a bit of documentation about themselves (like what arguments they accept) if you invoke the program with the -h flag. Example:

      python -h


# Command Completion
One very common mistake in typing in any programming language are small typos that break your program or instruction. One way to avoid them is to use an autocompletion feature so you don't have to type out a full name or variable. When you hit the TAB key, the terminal attempts to fill the rest of the command of filename you are typing. If there isn't a unique match (for instance, you are typeing: "cp fi" and then hit TAB when there are files with the names "file_01" and "file_02" present), it will fill in as much as it can (in this case "cp file_0"). If you hit TAB again, the terminal will present the potential options that it can autofill with. You can specify more characters until a unique match is found.

Example:

cp f<TAB>
cp file_0<TAB>
cp file_02 f<TAB>
cp file_02 file_0<TAB>
cp file_02 file_01
I recommend making use of tab completion as the terminal doesn't make typos, and humans do.

命令完成
输入任何编程语言的一个常见错误是打破你的程序或指令的小错别字。 避免它们的一种方法是使用自动完成功能，这样您就不必输入全名或变量。 当您点击TAB键时，终端会尝试填写您正在键入的其余文件名。 如果没有唯一匹配（例如，您正在键入：“cp fi”，然后在存在名称为“file_01”和“file_02”的文件时点击TAB），它将尽可能多地填写 （在本例中为“cp file_0”）。 如果再次点击TAB，终端将显示可以自动填充的潜在选项。 您可以指定更多字符，直到找到唯一匹配。

例：

cp f <TAB>
cp file_0 <TAB>
cp file_02 f <TAB>
cp file_02 file_0 <TAB>
cp file_02 file_01
我建议使用制表符完成，因为终端不会拼写错误，人类也会这样做。

# History
The terminal remembers each command you type into it in its history. When you execute the history command, the terminal will report each command run, with a number. Example:

  495  ls
  496  cd ../../
  497  ls
  498  ls
  499  cd ..
  500  cp file_02 file_01
  501  history
You can run a command again by noting its number. For instance, !500 will run the cp command again.

A neat trick is the !! command which runs the last command again.

历史
终端会记住您在其历史记录中键入的每个命令。 执行history命令时，终端将报告每个命令运行，并带有一个数字。 例：

   495 ls
   496 cd ../../
   497 ls
   498 ls
   499 cd ..
   500 cp file_02 file_01
   501历史
您可以通过记下其编号再次运行命令。 例如，！500将再次运行cp命令。

一个巧妙的技巧是!! 命令再次运行最后一个命令。

# Configuration (.bashrc and .bash_profile)
Sometimes there are bash commands you always want to run before you get to work. Perhaps, you want your terminal to configure some settings, or tell you how much disk space you have left. To make this easier, there are two config files that BASH looks for (in your HOME directory).

.bashrc is BASH script file is run everytime you invoke bash (example: bash my script.sh) and when you login in. .bash_profile is a script that runs when you login to your user account. Both of these are used to execute BASH commands that set up your environment.

配置（.bashrc和.bash_profile）
有时在你开始工作之前总是想要运行bash命令。 也许，您希望终端配置一些设置，或者告诉您剩余的磁盘空间。 为了使这更容易，BASH查找了两个配置文件（在您的HOME目录中）。

.bashrc是每次调用bash时运行的BASH脚本文件（例如：bash my script.sh）和登录时.bash_profile是一个在您登录用户帐户时运行的脚本。 这两个用于执行设置环境的BASH命令。

# Header Files
If we are going to define a function in one file and use the function in a main file, we are going to have to find a way to inform the main file about the types of the function. That is, we have to tell the main file:

the function's name
the type the function returns
the type of the parameters the function uses
the name of each parameter is unimportant. It can be given, changed in the main function or just left out. All that matters is each parameter's type
If we tell the main function this information, that is enough for the C++ compiler to check that the function is being used correctly in main, and by correctly I mean that main is using all the types correctly in calling the function, even though it does not yet have available the actual function code.

Providing this information is the job of a header file. Header files that users write typically end in .h, and are used to indicate the type information of a some C++ elements (of functions, or classes, or some other C++ thing). This header file is used by the compiler to make sure that, whoever is using this function, they are at least using the types correctly. Thus without the function itself, we can know that we followed the compiler rules and used the correct types.

Example
Make a new directory/folder, call it lab6, as you have been doing all along (either with your File Browser and the Create Folder dropdown or with the command line command mkdir).

The mkdir command takes a folder name and creates that (empty) folder. Example:

mkdir lab6
Download the following three files. Copy these files to your desktop (easiest, right click each file, then Save As into your lab 6 directory/folder).

main.cpp
extra.cpp
extra.h
Navigate your terminal to the "lab6" folder. Then compiler your three files with the following command:

g++ -std=c++11 -Wall  *.cpp
That means, it will compile all (* means all names, *.cpp means all files ending in .cpp) the .cpp files and build an executable.

Two warnings!
It's nice that the previous command compiles all the files, but if you have too many files (from different projects, things you are working on temporarily etc.) it won't work. Instead, you can do it with a list of files. You can even name your executable using the -o modifier to be something than the dreaded a.out.
g++ -std=c++11 -Wall file1.cpp file2.cpp file3.cpp -o namedExecutable.exe
We never compile a .h file. That doesn't make any sense. All a .h file provides is a list of declarations to be used by other files. It is never compiled and would not show up in the list of files to compile (shown above).

头文件
如果我们要在一个文件中定义一个函数并在主文件中使用该函数，我们将不得不找到一种方法来通知主文件有关函数类型的信息。也就是说，我们必须告诉主文件：

函数的名称
函数返回的类型
函数使用的参数类型
每个参数的名称都不重要。它可以在主函数中给出，改变或者只是省略。重要的是每个参数的类型
如果我们告诉main函数这个信息，这足以让C ++编译器检查函数是否在main中正确使用，并且正确的意思是main在调用函数时正确地使用了所有类型，即使它确实还没有可用的实际功能代码。

提供此信息是头文件的作用。用户编写的头文件通常以.h结尾，用于指示某些C ++元素（函数，类或其他一些C ++事物）的类型信息。编译器使用此头文件来确保使用此函数的用户至少正确使用这些类型。因此，如果没有函数本身，我们可以知道我们遵循编译器规则并使用了正确的类型。

例
创建一个新目录/文件夹，将其称为lab6，就像您一直在做的那样（使用文件浏览器和创建文件夹下拉列表或使用命令行命令mkdir）。

mkdir命令采用文件夹名称并创建该（空）文件夹。例：

mkdir lab6
下载以下三个文件。将这些文件复制到桌面（最简单，右键单击每个文件，然后另存为您的lab 6目录/文件夹）。

main.cpp中
extra.cpp
extra.h
将终端导航到“lab6”文件夹。然后使用以下命令编译您的三个文件：

g ++ -std = c ++ 11 -Wall * .cpp
这意味着，它将编译所有（*表示所有名称，* .cpp表示以.cpp结尾的所有文件）.cpp文件并构建可执行文件。

两个警告！
上一个命令编译所有文件很好，但如果你有太多的文件（来自不同的项目，你正在临时工作等等），它将无法正常工作。相反，您可以使用文件列表来完成。您甚至可以使用-o修饰符将可执行文件命名为可怕的a.out。
g ++ -std = c ++ 11 -Wall file1.cpp file2.cpp file3.cpp -o namedExecutable.exe
我们从不编译.h文件。这没有任何意义。所有.h文件提供的是其他文件要使用的声明列表。它永远不会被编译，也不会出现在要编译的文件列表中（如上所示）。


# g++ -std=c++11 -Wall (file or cpp) （运行）

# ./a.out (输出）
