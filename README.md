EE 316 Computer Engineering Junior Lab Design Project 6
Spring 2023


Specification: Text display on video using FPGA Due Dates:	Thursday, April 27- lab demo
                         Monday, April 29, written report due


Parts List:

1.	one Xilinx's Cora Z7-10 board
2.	one Digilent Pmod VGA for a monitor
3.	one VGA cable
4.	one (PS/2) keyboard
5.	one Digilent Pmod PS2 for the keyboard


You have been tasked with designing an electronic system that enables a person to display text on a VGA monitor using a PS/2 keyboard connected to Xilinx's Cora Z7 board. Although the Cora Z7 board lacks a PS/2 port, you can use the PS2 adapter to connect the keyboard to the FPGA, making it appear as if it is connected to a PS/2 port.

To accomplish this, you will create a subordinate PS/2 keyboard custom AXI IP module (ps2_keyboard) that takes bits from the serial PS/2 port and converts them into an 8-bit scancode. Once a scancode is received, an interrupt signal (IRQ_O) shall be sent to a manager. 

You will also need to create a manager reader custom AXI IP module (videomemlab_manager) that will wait for this interrupt and read the scancode from the PS/2 module. Reading the scancode will clear the interrupt. In addition, the manager will track three flags indicating whether the ctrl, shift, or alt key is pressed. Based on the scancode and the status of these flags, an ASCII code can be created using the provided scancode2ascii module. Subsequently, the module mentioned above will generate pixel data representing characters on a VGA monitor. The pixel data in the manager may or may not include color information, and it will be transmitted to a subordinate VGA_bram module through the AXI interface.

The next step is to design logic to control the synchronization (sync) signals on a VGA monitor. Your sync generator will output five signals: vga_r(3 downto 0), vga_g(3 downto 0), vga_b(3 downto 0), vga_hs, and vga_vs. After implementing the sync generator and verifying the functionality, the next goal is to create an AXI VGA subordinate module with a video memory buffer that drives a VGA monitor. The manager uses the AXI bus to write pixel data to the video memory buffer, and the graphics hardware reads that memory buffer continuously to generate the RGB pixel signals. The pixel data contains information about the color of the pixel. In this lab, you can use 4 bits per pixel. The four bits can be mapped such that two bits are used for red, and the others are used for green and blue, respectively. For a 640x480 VGA monitor, we need to generate pixels every 40 ns, which is a heavy burden for a processor. As a result, you need to design special graphics hardware containing a video memory buffer that holds the pixel data. You shall create a memory buffer of at least 153600 bytes. The FPGA on Zynq7000 provides 270KB BRAM. You can combine the block RAMs in your FPGA to create a 153600-byte memory array that is large enough to satisfy our video needs.

  Documentation:

Help for PS/2 protocol:
h ttp://www.computer-engineering.org/ps2protocol/

Digilentinc Pmod PS2: Keyboard Mouse connector
h ttps://store.digilentinc.com/pmod-ps2-keyboard-mouse-connector/

Digilentinc Pmod VGA: Video Graphics Array
h ttps://store.digilentinc.com/pmod-vga-video-graphics-array/

Learn VHDL by example (search for Structural Modeling of HD-6402 on the page) h ttp://esd.cs.ucr.edu/labs/tutorial/


Teams:

Team 1	Team 2	Team 3	Team 4	Team 5	Team 6	Writer
Kubicka	LaBue	Morris	Skinner	Ernesto	Mathew	 
Pamela	Cameron	Shawn	Kaili	Isabelle	Graham	 
Ella	Jacob	Nelson	Nathan	Zander	Keith	
 	 	 	macy	 	 	

