CC      = cc
CXX     = c++

# Use the following CFLAGS and LIBS if you don't want to use gpsd.
CFLAGS  = -g -O3 -Wall -DHAVE_LOG_H -std=c++0x -pthread
LIBS    = -lpthread

# Use the following CFLAGS and LIBS if you do want to use gpsd.
#CFLAGS  = -g -O3 -Wall -DHAVE_LOG_H -DUSE_GPSD -std=c++0x -pthread
#LIBS    = -lpthread -lgps

LDFLAGS = -g

OBJECTS = APRSWriter.o Conf.o GPSHandler.o IcomNetwork.o KenwoodNetwork.o Log.o Mutex.o NXDNCRC.o NXDNGateway.o NXDNLookup.o NXDNNetwork.o \
	  Reflectors.o RptNetwork.o StopWatch.o Thread.o Timer.o UDPSocket.o Utils.o Voice.o

all:		NXDNGateway

NXDNGateway:	GitVersion.h $(OBJECTS)
		$(CXX) $(OBJECTS) $(CFLAGS) $(LIBS) -o NXDNGateway

%.o: %.cpp
		$(CXX) $(CFLAGS) -c -o $@ $<

NXDNGateway.o: GitVersion.h FORCE

.PHONY: GitVersion.h

FORCE:


install:
		install -m 755 NXDNGateway /usr/local/bin/

clean:
		$(RM) NXDNGateway *.o *.d *.bak *~

# Export the current git version if the index file exists, else 000...
GitVersion.h:
ifneq ("$(wildcard ../.git/index)","")
	echo "const char *gitversion = \"$(shell git rev-parse HEAD)\";" > $@
else
	echo "const char *gitversion = \"0000000000000000000000000000000000000000\";" > $@
endif

