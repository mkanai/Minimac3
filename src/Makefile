# Name of your executable, replace sampleProgram with your program name
EXE=Minimac3
OPTFLAG_OPT = -O4 
OPTFLAG_DEBUG = -ggdb -O0
########################
# Specify your Files:
# TOOLBASE - files with both .cpp and .h.  Just include the base name.
# Example if you have Class1.cpp, Class1.h, Class2.cpp, and Class2.cpp, specify:
# TOOLBASE = Class1 Class2
TOOLBASE = HaplotypeSet Unique Imputation MarkovModel MarkovParameters ImputationStatistics
# SRCONLY - .cpp only files.  Specify the entire name, including the .cpp.
# Example, if you have Main.cpp, and File1.cpp, specify:
# SRCONLY = Main.cpp File1.cpp
SRCONLY = Main.cpp
# HDRONLY - .h only files.  Specify the entire name, including the .h.
# Example, if you have Template1.h and Template2.h, specify:
# HDRONLY = Template1.h Template2.h
HDRONLY = 

########################
# Optional settings if you need them.
# Specify any additional compile varaibles you want
# Example:
DATE=$(shell date)
USER=$(shell whoami)
USER_COMPILE_VARS = -DDATE="\"${DATE}\"" -DUSER="\"${USER}\"" 
#USER_COMPILE_VARS = 

# Specify any additional includes you need.
USER_INCLUDES = -I ../

# Specify any additional warnings you need to enable.
# Example: 
# USER_WARNINGS ?= -Werror -Wno-unused-variable $(shell if [ X$(CCVERSION) \> X4.2.0 ] ; then echo " -Wno-unused-result" ; fi)
USER_WARNINGS =-Wno-unknown-pragmas -Wno-unused-local-typedefs
USER_REMOVES = $(MAKE) -C $(ACTUAL_PATH)  --no-print-directory clean; rm -f $(BINDIR)/$(OMP_EXE); rm -rf $(OBJDIR)/omp

# If you don't want to include the current directory (-I.), uncomment this line:
#CURRENT_DIR_INCLUDE=

# Specify any TOOLBASE that needs to be re-compiled when any other file
# is modified.  Do NOT specify this same file in TOOLBASE.
# Example: if you have Executable.cpp and Executable.h, specify:
# COMPILE_ANY_CHANGE = BamExecutable
COMPILE_ANY_CHANGE = 

# If you want to overwrite the default directory for the binaries, from the
# Default setting of 'bin', uncomment the next line and specify a value.
# BIN_DIR = bin

########################
# Include the base Makefile
PARENT_MAKE = Makefile.src

include ../Makefile.inc
.DEFAULT_GOAL := both

both: opt openmp
all: opt openmp debug profile

# Handle openmp
OMP_EXE:=Minimac3-omp
OBJDIR_OMP := $(OBJDIR)/omp
OBJECTS_OMP := $(patsubst %,$(OBJDIR_OMP)/%,$(TOOLOBJ))

openmp: USER_COMPILE_VARS = -fopenmp -DDATE="\"${DATE}\"" -DUSER="\"${USER}\""
openmp: $(BINDIR_OPT)/$(OMP_EXE)

$(BINDIR_OPT)/$(OMP_EXE): PROG_OPT=$(BINDIR_OPT)/$(OMP_EXE)
$(BINDIR_OPT)/$(OMP_EXE): OBJECTS_OPT=$(OBJECTS_OMP)
$(BINDIR_OPT)/$(OMP_EXE): $(USER_LIBS) $(REQ_LIBS_OPT) $(OBJECTS_OMP) | $(BINDIR_OPT)
	$(OPT_BUILD)


$(OBJECTS_OMP): TYPE = OPT
$(OBJECTS_OMP): $(INCLUDE_PATH)/*h | $(STAT_GEN_LIB_OPT) $(OBJDIR_OMP)

$(OBJDIR_OMP):
	mkdir -p $@
$(OBJDIR_OMP)/%.o: %.c
	$(CCOMPILE)
$(OBJDIR_OMP)/%.o: %.cpp 
	$(CXXCOMPILE)

########################
# Add any additional targets here.
