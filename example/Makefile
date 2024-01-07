.PHONY: all run

# Disable builtin rules (for .c, .o) by providing an empty .SUFFIXES rule
# Yes. GNU make is a rat's nest
.SUFFIXES:

# Make sure intermediate files are *NOT* deleted
# Yes. GNU make is a rat's nest
.PRECIOUS: %.s %.o


LD = ld65
CC = cc65
CA = ca65

CAFLAGS = --debug-info --listing $*.lst --verbose
# https://cc65.github.io/doc/ca65.html#ss2.1
CCFLAGS = -Oi --add-source -g  # --target nes -I$(INCLUDES) 
# https://cc65.github.io/doc/cc65.html#ss2.1


all: clean run

run: hello.nes
	open hello.nes

%.s: %.c
	$(CC) $(CCFLAGS) $< 

%.o: %.s $(S_FILES)
	$(CA) $(CAFLAGS) $<

hello.nes: hello.o crt0.o chr_generic.o vrambuf.o neslib2.lib nes.lib
	$(LD) -C nrom_128_horz.cfg  -m memmap.txt -Ln vice.txt -o hello.nes hello.o crt0.o chr_generic.o vrambuf.o neslib2.lib nes.lib

clean:
	rm -f hello.o hello.s hello.nes
