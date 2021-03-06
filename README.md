# Tomasulo OOO Processor
-------------------------

This is our attempt to improve on the base Tomasulo machine, designed by Shubhayu Das, as part of the VL803 course's first assignment. In this extension to the original code, we will implement various data prefetching policies for caches. Our course was instructed by professor [Nanditha Rao](https://in.linkedin.com/in/nanditha-rao-b5608928) at IIITB.

Feel free to raise Issues for feature requests and bugs.

Version: 2.0.0

*This is a mirror repository of the [original repository](https://github.com/Shubhayu-Das/tomasulo-O3-with-prefetch)*

-------------------
### Students
1. [Sai Manish Sasanapuri](https://github.com/Sai-Manish/)
2. [Shubhayu Das](https://github.com/Shubhayu-Das/)
3. [Veerendra S. Devaraddi](https://github.com/vsdevaraddi)

-----------------------------

### Future improvements
1. Add additional prefetchers and replacement policies
2. Additional GUI features(possibly migrate to Qt? Too much work)
3. Add a Wiki with all the requisite info?
4. Add argparse/optparse for taking in input params

------------------------------

### Software libraries

Language: Python 3 (3.6.x)

**GUI**

The GUI needs the ```tkinter``` and ```pysimplegui```. These can be installed using the following commands:

On Linux/Ubuntu:
```bash
$ sudo apt install python3-tk
$ pip install pysimplegui
```

On Windows:
```
$ pip install pysimplegui
```

I have tested the code on Python 3.8.7 on both the OS (Windows 1903 build and Ubuntu 20.04.01 LTS), if there are any issues, please raise an Issue on Github. The GUI might appear different in different screens, depending on the aspect ratios. I have tried to make it useable, over looking pretty. For better control over the GUI, I would have to dive too deep(using tk or Qt5), which I can't bother to do now.

**Type Checking**
We have used ```mypy``` for static type checking. With all the data that is being passed around, things can become messy. Static type checking ensures we(or future contributors) know the exact type of each variable. Static type checking is not completely enforced everywhere.

To run type checking, first install mypy. Then run it as follows:
```bash
# If you need to install mypy
$ pip install mypy
# To run static type checking on a single file
$ mypy <filename>.py
# To run type checking on the entire code/ folder
$ mypy code/
```
You can try adding additional flags like ```--show-error-context```, as per need. Please ignore warnings about PySimpleGUI, which is beyond our control.

**Linting**

This project enforces uniform code style using the pep8 standards. For this, the ```pycodestyle``` and ```autopep8``` libraries are used. The ```E501``` styling(too long lines) is ignored, because there are just too many of them and they are hard to fix properly. The libraries can be installed as extensions in VS code. However, I prefer using them from the terminal. To install them, run(in any OS):

```bash
$ pip install pycodestyle autopep8
```

After this, detect all the errors using:

```bash
$ pycodestyle code/ --statistics | grep -v E501
```
You might want to pipe the output through ```tail```, to see the statistics at the end only. Optionally, you can use ```grep``` to search for occurances of a particular error.

To fix(most of) the errors, use ```autopep8``` as follows:

```autopep8 code/ --recursive --in-place -j 8 --pep8-passes 1000```


To fix a single type of error, use:

```autopep8 code/ --recursive --in-place -j 8 --pep8-passes 1000 --select=<error code>```.

Note that for both the above steps, you need to be in the directory which contains this README file.


**References**:
1. [PySimpleGUI documentation website](https://pysimplegui.readthedocs.io/en/latest/)
2. [autopep8 documentation](https://pypi.org/project/autopep8/#usage)
3. [pep8 documentation](https://www.python.org/dev/peps/pep-0008/)

--------------------

### Instructions for running

This simulator supports LW/SW, ADD/SUB from RISC-V RV32I, and MUL/DIV from RISC-V RV32M. 

Summary to execute program:
- To simply start the simulation, for the given question: ```python main.py```

- To load custom assembled program: ```python main.py build/<filename.bin>```

- To load in custom data memory along with assembled program: ```python main.py build/<filename.bin> <data_mem.data>```

### GUI doesn't open up

The GUI library might throw an error saying that the DISPLAY environment variable is not available. To fix this, set ```DISPLAY=":0"```. In Ubuntu(Linux in general), one way to do this is:
```bash
$ echo 'export DISPLAY=":0"' >> ~/.profile
$ source ~/.profile
# Just to confirm that the env is really set
$ echo $DISPLAY
```

Try running the program after this, it should not cause any problems. You can remove that line from ```.profile``` later on, if needed. That line of code selects the monitor on which the GUI will be displayed. So, if you have a multi-monitor display, you can remove it after running this program. You will have to run ```source ~/.profile``` after removing the line from the file.

### Detailed instructions:
- Place your ```asm``` program in the src folder.
- Open a terminal and navigate to the ```code/``` folder. Execute: ```python assembler.py src/<filename.asm>```.
- This will generate the ```bin``` file in ```build/<filename.bin>```.
- Now run: ```python main.py build/<filename.bin>``` to launch the simulation
- The simulation supports pausing, stepping back and forward - one step at a time.
- To stop the simulation, simply close the window
- The data memory is stored in ```data_memory.dat```. You can either modify the same file, or create a separate file.
  The data memory file can be chosen from the GUI itself(Load > Load from data memory). Or while executing the program:

  ```python main.py build/<filename.bin> <data_mem.data>```

- To change the duration spent on each cycle, open ```constants.py``` and adjust the ```CYCLE_DURATION``` in *milliseconds* to your desired value.

-----

### Known Bugs

1. ```DEBUG=True``` doesn't print a whole lot of intelligible data. This is sorely because I didn't have the time and patience to complete it yet. Enjoy the GUI though.

--------------

### License

We have MIT licensed this project **except for the RISC-V references**. RISC-V opcodes repo [riscv/riscv-opcodes](https://github.com/riscv/riscv-opcodes) is licensed by the University of California.
