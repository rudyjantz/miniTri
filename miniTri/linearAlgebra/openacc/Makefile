##############################################################################
#                                                                            #
# File:      Makefile                                                        #
# Project:   miniTri                                                         #
# Author:    Michael Wolf                                                    #
#                                                                            #
# Description:                                                               #
#              Makefile for code.                                            #
#                                                                            #
##############################################################################
UTILDIRS = ../../utils/
INCDIRS = -I. -I$(UTILDIRS)
CCC = pgc++
# Will crash if NDEBUG not defined
CCFLAGS = -O3 -DNDEBUG -std=c++11 -acc -ta=nvidia -Minfo=accel
LIBPATH = -L. 


#--------------------------------------------------
LIBSOURCES =             \
          CSRMatrix.cc   \
          Graph.cc 

LIBOBJECTS         = $(LIBSOURCES:.cc=.o) 
UTILOBJECTS        = mmio.o mmUtil.o binFileReader.o

#--------------------------------------------------

.SUFFIXES:

%.o : %.cc
	$(CCC) $< -c $(CCFLAGS) $(INCDIRS)

%.o : %.cpp
	$(CCC) $< -c $(CCFLAGS) $(INCDIRS)

%.o : %.f
	$(F77) $< -c $(CCFLAGS) $(INCDIRS)


#--------------------------------------------------
vpath %.cc $(UTILDIRS)
vpath %.cpp $(UTILDIRS)

all 		:	lib miniTri
matrix.o	:	CSRMatrix.h 

lib		:	$(LIBOBJECTS) $(UTILOBJECTS)
	ar rvu libSPLA.a $(LIBOBJECTS) $(UTILOBJECTS)

miniTri	:	lib CSRMatrix.h Graph.h
	$(CCC) $(INCDIRS) $(LIBPATH) $(CCFLAGS) -o miniTri.exe miniTri.cc -lSPLA 

clean	:
	rm -f *.o *~ libSPLA.a *.out miniTri.exe
