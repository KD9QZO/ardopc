#
# ARDOPC Makefile
#

PROJ_NAME := ardop1ofdm


PREFIX ?= /usr/local


OBJS := ofdm.o
OBJS += LinSerial.o
OBJS += KISSModule.o
OBJS += pktARDOP.o
OBJS += pktSession.o
OBJS += BusyDetect.o
OBJS += i2cDisplay.o
OBJS += ALSASound.o
OBJS += ARDOPC.o
OBJS += ardopSampleArrays.o
OBJS += ARQ.o
OBJS += FFT.o
OBJS += FEC.o
OBJS += HostInterface.o
OBJS += Modulate.o
OBJS += rs.o
OBJS += berlekamp.o
OBJS += galois.o
OBJS += SoundInput.o
OBJS += TCPHostInterface.o
OBJS += SCSHostInterface.o

LIBS := -lrt
LIBS += -lm
LIBS += -lpthread
LIBS += -lasound


# Configuration:

CROSS :=

AR      := $(CROSS)ar
AS      := $(CROSS)as
CC      := $(CROSS)gcc
CPP     := $(CROSS)cpp
CXX     := $(CROSS)g++
LD      := $(CROSS)ld
NM      := $(CROSS)nm
OBJCOPY := $(CROSS)objcopy
OBJDUMP := $(CROSS)objdump
RANLIB  := $(CROSS)ranlib
READELF := $(CROSS)readelf
SIZE    := $(CROSS)size
STRINGS := $(CROSS)strings
STRIP   := $(CROSS)strip

DOXYGEN := doxygen
RM      := rm -f
ECHO    := echo -e
MKDIR   := mkdir


DEFINES    := -DLINBPQ
#DEFINES   += -DDEBUG
DEFINES    += -DNDEBUG

UNDEFINES  := -U__DOXYGEN__
#UNDEFINES += -UNDEBUG
UNDEFINES  += -UDEBUG


C_STDLVL   := gnu11
CXX_STDLVL := gnu++14
OPTLVL     := 2
DBGLVL     := 2


CFLAGS   := -pipe -std=$(C_STDLVL) -O$(OPTLVL) -g$(DBGLVL) $(DEFINES) $(UNDEFINES) -MMD
CXXFLAGS := -pipe -std=$(CXX_STDLVL) -O$(OPTLVL) -g$(DBGLVL) $(DEFINES) $(UNDEFINES) -MMD
LDFLAGS  := -Wl,-Map=$(PROJ_NAME).map -Wl,--cref $(LIBS)

all: ardopc

ardopc: $(OBJS)
	$(CC) $(OBJS) $(LDFLAGS) -o $(PROJ_NAME)

install: $(PROJ_NAME)
	install $(PROJ_NAME) $(PREFIX)/bin
	ln -sf $(PREFIX)/bin/$(PROJ_NAME) $(PREFIX)/bin/ardop
	install ../initscripts/ardop.service /etc/systemd/system

-include *.d

clean:
	$(ECHO) "Cleaning compiler output..."
	$(RM) $(PROJ_NAME)
	$(RM) *.o
	$(RM) *.map

