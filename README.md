
`intel_jtag_uart` is a Python module that can be used to interact with the JTAG UART instances inside
Intel FPGA designs.

The official ways to do this are either interactively, through `nios2-terminal` utility,
or by scripting some TCL code inside the Quartus System Console. There is no official 
straightforward way to interact with a JTAG UART with Python. 

This module is a wrapper around the `jtag_atlantic` shared library/DLL that is part of any
modern Quartus installation. (`jtag_atlantic` is the internal code name for the JTAG UART.)

To use this module, you need access to the `jtag_atlantic` shared library as well as the `jtag_client`
shared library, which provides lower level JTAG-related functions.

## Usage

* Install this package with `pip3 install intel_jtag_uart`.
* Point to the `jtag_atlantic` and `jtag_client` shared libraries, so that the module can find it.

    The module uses the following sequence to find these libraries:

    1. Look in the directory in which `intel_jtag_uart.py` is located
    1. Look in the directory in which the executable that uses this module is located
    1. Use the OS-provided way to find shared libraries. (E.g. for Linux, it will check
       the directories of the `$LD_LIBRARY_PATH` environment variable.) 
    1. Look in the `$QUARTUS_ROOTDIR` directory

    Most default Quartus installations will have `$QUARTUS_ROOTDIR` environment variable
    set to the correct directory, so everything should just work&trade;.

* Use some variation of the script below:

```python
import intel_jtag_uart

try:
    ju = intel_jtag_uart.intel_jtag_uart()

except Exception as e:
    print(e)
    sys.exit(0)

ju.write(b'r')
time.sleep(1)
print("read: ", ju.read())
```

The script sends `r` to the JTAG UART, waits 1 seconds for a reply, and reads the
reply, if there is any. If you have an Arrow/Terasic DECA FPGA board, you can check
things out right away with a [precompiled example bitstream](https://github.com/tomverbeure/intel_jtag_uart/tree/main/example/arrow_deca).

## Full List of Functions/Methods

Use [the source](https://github.com/tomverbeure/intel_jtag_uart/blob/main/src/intel_jtag_uart/intel_jtag_uart.py), Luke!

This module is a very thin wrapper around a handful of function calls that are mostly self-explanatory.

## Bug Reports/Comments/Questions

Bug reports, comments, or questions can be entered through [the GitHub issue tracker](https://github.com/tomverbeure/intel_jtag_uart/issues)
of this project.

## References

* [The Intel JTAG UART - Add a Serial Console to Your Design without Extra IO Pins](https://tomverbeure.github.io/2021/05/02/Intel-JTAG-UART.html)
* [Write Your Own C and Python Clients for the Intel JTAG UART](https://tomverbeure.github.io/2021/05/08/Write-Your-Own-C-and-Python-Clients-for-Intel-JTAG-UART-with-libjtag_atlantic.html)
* [`jtag_uart_example` project](https://github.com/tomverbeure/jtag_uart_example)
* [intel-jtag-uart on pypi.org](https://pypi.org/project/intel-jtag-uart/)


