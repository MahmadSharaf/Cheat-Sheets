# How Python runs programs

- [How Python runs programs](#how-python-runs-programs)
  - [The Programmer's View](#the-programmers-view)
  - [Python’s View](#pythons-view)
    - [Byte code compilation](#byte-code-compilation)
    - [The Python Virtual Machine (PVM)](#the-python-virtual-machine-pvm)
    - [Performance implications](#performance-implications)
    - [Development implications](#development-implications)
  - [Execution Model Variations](#execution-model-variations)
    - [Python Implementation Alternatives](#python-implementation-alternatives)
  - [Frozen Binaries](#frozen-binaries)

## The Programmer's View

- You can create a file of statements with any text editor you like. By convention, Python program files are given names that end in `.py`; technically, this naming scheme is required only for files that are “imported” but most Python files have `.py` names for consistency.

## Python’s View

- There are a few steps that Python carries out before starting the code. Specifically, it’s first compiled to something called “byte code” and then routed to something called a “virtual machine".

### Byte code compilation

- When you execute a program Python first compiles the source code (the statements in the file) into a format known as *byte code*.
  - *Compilation* is simply a translation step,
  - and *byte code* is a lower-level, platform-independent representation of the source code.
- This byte code translation is performed to speed execution.
  - *byte code* can be run much more quickly than the original source code statements.
- If the Python process has write access, it will store the *byte code* in files that end with a `.pyc` extension (“.pyc” means compiled “.py” source).
- Prior to Python 3.2, these files show up on your computer after you’ve run a few programs alongside the corresponding source code files—that is, in the same directories. For instance, you’ll notice a `script.pyc` after importing a `script.py`.
- In 3.2 and later, Python instead saves its `.pyc` *byte code* files in a subdirectory named `__pycache__` located in the directory where your source files reside, and in files whose names identify the Python version that created them (e.g., script.cpython-33.pyc). The new `__pycache__` subdirectory helps to avoid clutter, and the new naming convention for *byte code* files prevents different Python versions installed on the same computer from overwriting each other’s saved *byte code*.
- In both models, Python saves byte code like this as a startup speed  optimization. The next time you run your program, Python will load the `.pyc` files and skip the compilation step, as long as you haven’t changed your source code since the byte code was last saved, and aren’t running with a different Python than the one that created the byte code. It works like this:
  - **Source changes**: Python automatically checks the last-modified timestamps of source and byte code files to know when it must recompile.
  - **Python versions**: Imports also check to see if the file must be recompiled because it was created by a different Python version, using either a “magic” version number in the byte code file itself in 3.2 and earlier, or the information present in byte code filenames in 3.2 and later.
- If Python cannot write the byte code files to your machine, your program still works—the byte code is generated in memory and simply discarded on program exit. However, because .pyc files speed startup time, you’ll want to make sure they are written for larger programs.
- *Byte code* files are also one way to ship Python programs—Python is happy to run a program if all it can find are `.pyc` files, even if the original .`py` source files are absent. (See Frozen Binaries for another shipping option.)

### The Python Virtual Machine (PVM)

- Once your program has been compiled to byte code, it is shipped off for execution to something generally known as the Python Virtual Machine.
- The PVM is the runtime engine of Python.
- PVM is just a big code loop that iterates through your byte code instructions, one by one, to carry out their operations.
- Technically, it’s just the last step of what is called the “Python interpreter”.

### Performance implications

- There are a few differences with respect to fully compiled languages such as C and C++.
  - For one thing, there is usually no build or “make” step in Python work, code runs immediately after it is written.
  - For another, Python byte code is not binary machine code. Byte code is a Python-specific representation.
- This is why some Python code may not run as fast as C or C++ code, as the PVM loop, not the CPU chip, still must interpret the byte code, and byte code instructions require more work than CPU instructions.
- On the other hand, unlike in classic interpreters, there is
still an internal compile step—Python does not need to reanalyze and reparse each source statement’s text repeatedly. The net effect is that pure Python code runs at speeds somewhere between those of a traditional compiled language and a traditional interpreted language.

### Development implications

- There is really no distinction between the development and execution environments. That is, the systems that compile and execute your source code are really one and the same.
- This makes for a much more rapid development cycle. There is no need to precompile and link before execution may begin.
- The `eval` and `exec` built-ins, for instance, accept and run strings containing Python program code.
- This structure is also why Python lends itself to product customization—because Python code can be changed on the fly, users can modify the Python parts of a system onsite without needing to have or compile the entire system’s code.

## Execution Model Variations

### Python Implementation Alternatives

- There are at least five implementations of the Python language—CPython, Jython, IronPython, Stackless, and PyPy.
- CPython is the standard implementation, All the other
Python implementations have specific purposes and roles, though they can often serve in most of CPython’s capacities too. All implement the same Python language but execute programs in different ways.
- For example, PyPy is a drop-in replacement for CPython, which can run most programs much quicker. Similarly, Jython and IronPython are completely independent implementations of Python that compile Python source for different runtime architectures, to provide direct access to Java and .NET components. It is also possible to access Java and .NET software from standard CPython programs—JPype and Python for .NET systems, for instance, allow standard CPython code to call out to Java and .NET components. Jython and IronPython offer more complete solutions, by providing full implementations of the Python language.

## Frozen Binaries

- With the help of third-party tools that you can fetch off the Web, it is possible to turn your Python programs into true executables, known as frozen binaries in the Python world. These programs can be run without requiring a Python installation.
- Frozen binaries bundle together the byte code of your program files, along with the PVM (interpreter) and any Python support files your program needs, into a single package.
- Today, a variety of systems are capable of generating frozen binaries, which vary in platforms and features: py2exe for Windows only, but with broad Windows support; PyInstaller, which is similar to py2exe but also works on Linux and Mac OS X and is capable of generating self-installing binaries; py2app for creating Mac OS X applications; freeze, the original; and cx_freeze, which offers both Python 3.X and cross-platform support. You may have to fetch these tools separately from Python itself, but they are freely available.