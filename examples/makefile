#
# Build examples for ILEastic
#
# This works for:
#  make              compiles all demo programs
#  make helloworld   only compiles this single file
#

#-------------------------------------------------------------------------------
# User-defined part start
#

# BIN_LIB is the destination library for the demo programs.
BIN_LIB=ILEASTIC

# Inclucde directory for the noxDB headers
NOXDBINC='/usr/local/include/noxdb'
SHELL=/QOpenSys/usr/bin/qsh

#
# add this after CRTBNDRPG for build in vsCode:
# | grep '*RNF' | grep -v '*RNF7031' | sed  "s!*!$@: &!"
# User-defined part end
#-------------------------------------------------------------------------------


RCFLAGS=OPTION(*NOUNREF) DBGVIEW(*LIST)  OUTPUT(*NONE) INCDIR('./..' $(NOXDBINC))
SQLRPGCFLAGS=OPTION(*NOUNREF) DBGVIEW(*LIST)  OUTPUT(*NONE) INCDIR(''./..'')

.SUFFIXES: .rpgle .sqlrpgle
 
# suffix rules
.rpgle:
	liblist -a NOXDB;\
	liblist -a $(BIN_LIB);\
	system -iK "CRTBNDRPG PGM($(BIN_LIB)/$@) SRCSTMF('$<') $(RCFLAGS)" | grep '*RNF' | grep -v '*RNF7031' | sed  "s!*!$@: &!"
	
.sqlrpgle:
	system -iK "CRTSQLRPGI OBJ($(BIN_LIB)/$@) SRCSTMF('$<') RPGPPOPT(*LVL2) COMPILEOPT('$(SQLRPGCFLAGS)')"

OBJECTS = helloworld staticfile datachunks invalidreq querystr multroutes plugin

all: compile

compile: $(OBJECTS)

.PHONY:
