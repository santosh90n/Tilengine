CC       = gcc
SOURCES  = $(wildcard *.c)
OBJECTS  = $(SOURCES:.c=.o)
TARGETS  = barrel mode7 platformer racer scaling shadow shooter tutorial wobble colorcycle benchmark supermarioclone test_mouse

ifeq ($(OS),Windows_NT)
	RM = del /Q *.exe
	CFLAGS  = -m32 -msse2 -std=c99 -O2 -I"../../include"
	LDFLAGS = ../../lib/win32/Tilengine.lib -s
else
	RM = rm
	name := $(shell uname -s)
	arch := $(shell uname -m)
	ifeq ($(name),Linux)
		ifeq ($(arch),i686)
			CFLAGS = -m32 -msse2 -std=c99 -O2
		endif
		ifeq ($(arch),x86_64)
			CFLAGS = -m64 -msse2 -std=c99 -O2
		endif
		ifeq ($(arch),armv7l)
			CFLAGS = -std=c99 -O2
		endif
		LDFLAGS = -lTilengine -lm -s
	endif
	ifeq ($(name),Darwin)
		CFLAGS = -std=c99 -O2
		LDFLAGS = "/usr/local/lib/Tilengine.dylib" -lm
	endif
endif

.PHONY: all all-before all-after clean clean-custom

all: $(TARGETS)

barrel: Barrel.o Simon.o
	$(CC) Barrel.o Simon.o -o barrel $(LDFLAGS)
	
mode7: Mode7.o Sin.o
	$(CC) Mode7.o Sin.o -o mode7 $(LDFLAGS)
	
platformer: Platformer.o
	$(CC) Platformer.o -o platformer $(LDFLAGS)
	
racer: Racer.o Tree.o Actor.o
	$(CC) Racer.o Tree.o Actor.o -o racer $(LDFLAGS)
	
scaling: Scaling.o
	$(CC) Scaling.o -o scaling $(LDFLAGS)
	
shadow: Shadow.o
	$(CC) Shadow.o -o shadow $(LDFLAGS)

shooter: Shooter.o Actor.o Boss.o Enemy.o Explosion.o Ship.o Sin.o
	$(CC) Shooter.o Actor.o Boss.o Enemy.o Explosion.o Ship.o Sin.o -o shooter $(LDFLAGS)
	
tutorial: Tutorial.o
	$(CC) Tutorial.o -o tutorial $(LDFLAGS)

wobble: Wobble.o Sin.o
	$(CC) Wobble.o Sin.o -o wobble $(LDFLAGS)
	
colorcycle: ColorCycle.o
	$(CC) ColorCycle.o -o colorcycle $(LDFLAGS)

benchmark: Benchmark.o
	$(CC) Benchmark.o -o benchmark $(LDFLAGS)
	
supermarioclone: SuperMarioClone.o
	$(CC) SuperMarioClone.o -o supermarioclone $(LDFLAGS)
	
test_mouse: TestMouse.o
	$(CC) TestMouse.o -o test_mouse $(LDFLAGS)
	
%.o: %.c
	$(CC) -c $(CFLAGS) $< -o $@

# clean
clean: clean-custom
	$(RM) $(OBJECTS) $(TARGETS)
	