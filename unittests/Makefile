#
# Build script for ILEastic Unit Tests
#


#-------------------------------------------------------------------------------
# User-defined part start
#

# BIN_LIB is the destination library for the unit tests.
BIN_LIB=ILEASTIC

# This folder contains the ASSERT copybook of the unit testing framework.
RUINCDIR=/usr/local/include/irpgunit

# This library contains the ILEASTIC modules.
ILEASTIC_LIB=ILEASTIC

#
# User-defined part end
#-------------------------------------------------------------------------------

ILEASTIC_MODULES=($(ILEASTIC_LIB)/ILEASTIC) ($(ILEASTIC_LIB)/API) ($(ILEASTIC_LIB)/SIMPLELIST) ($(ILEASTIC_LIB)/VARCHAR) ($(ILEASTIC_LIB)/STREAM) ($(ILEASTIC_LIB)/XLATE) ($(ILEASTIC_LIB)/E2AA2E) ($(ILEASTIC_LIB)/STRUTIL) ($(ILEASTIC_LIB)/SNDPGMMSG)  

OBJECTS = REQUEST ROUTING

all: clean compile

compile: $(OBJECTS)

REQUEST:
	system "CRTRPGMOD MODULE($(BIN_LIB)/REQUEST) SRCSTMF('request.rpgle') INCDIR('$(RUINCDIR)') dbgview(*source) stgmdl(*teraspace)"
	system "CRTSRVPGM $(BIN_LIB)/REQUEST MODULE(($(BIN_LIB)/REQUEST) $(ILEASTIC_MODULES)) STGMDL(*TERASPACE) BNDSRVPGM(ASSERT) EXPORT(*ALL) OPTION(*DUPPROC)"

ROUTING:
	system "CRTRPGMOD MODULE($(BIN_LIB)/ROUTING) SRCSTMF('routing.rpgle') INCDIR('$(RUINCDIR)') dbgview(*source) output(*print) stgmdl(*teraspace)"
	system "CRTSRVPGM $(BIN_LIB)/ROUTING MODULE(($(BIN_LIB)/ROUTING) $(ILEASTIC_MODULES)) STGMDL(*TERASPACE) BNDSRVPGM(ASSERT) EXPORT(*ALL) OPTION(*DUPPROC)"

clean:
	-system "DLTMOD $(BIN_LIB)/REQUEST"
	-system "DLTSRVPGM $(BIN_LIB)/REQUEST"
	-system "DLTMOD $(BIN_LIB)/ROUTING"
	-system "DLTSRVPGM $(BIN_LIB)/ROUTING"
