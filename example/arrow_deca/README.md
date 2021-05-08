# Arrow DECA FPGA Board JTAG UART Example

If you have an [Arrow DECA FPGA board](https://tomverbeure.github.io/2021/04/23/Arrow-DECA-FPGA-board.html), 
you can test this package as follows:

* Load the included `arrow_deca_mini_cpu_jtag_uart.sof` bitstream into the FPGA

    After loading the bitstream, you should see 3 LEDs toggling in succession.

* Run `python3 demo.py` 

    If all goes well, the LEDs will change the toggle sequence.


The source code of this demo design can be found in [this GitHub repo](https://github.com/tomverbeure/jtag_uart_example).

