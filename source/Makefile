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

all: clean run

run: hello.nes
	open hello.nes

%.s: %.c
	$(CC) $(CCFLAGS) $< 

%.o: %.s $(S_FILES)
	$(CA) $(CAFLAGS) $<

hello.nes: hello.o crt0.o vrambuf.o chr_generic.o nes.lib
	$(LD) -C nrom_128_horz.cfg  -m memmap.txt -o hello.nes hello.o crt0.o vrambuf.o chr_generic.o neslib2.lib

hello.o: hello.c
	$(CC) -Oi hello.c --target nes -I/opt/homebrew/include/ --add-source
	$(CA) hello.s

clean:
	rm -f hello.o hello.s hello.nes
