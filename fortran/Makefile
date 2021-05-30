# Makefile for program ring_generate
#
# Lines starting with "#" are comments.
#
# The executable has its name, then all dependencies (object files).
#   Beneath that is the statement to link them and create the program.
#
# The last statements say how to turn .f90 or .c files into .o files: compiling.
#
# Makefiles can get confusing, but they are quite useful in compiling programs.
# Type "man make" for more information, or try one of these help pages:
#
#          http://kiwi.atmos.colostate.edu/fortran/docs/fortran90-mar30.pdf
#	   http://genius2k.is-programmer.com/posts/40301.html
#	   https://www.sharcnet.ca/help/index.php/Make_utility_and_makefiles
#	   http://www.cs.colby.edu/maxwell/courses/tutorials/maketutor/
#

#F90	= gfortran-mp-7
F90	= ${FC}

### switch to these to note use OpenBLAS ###
#OPTION	= -fdump-core -fcheck=bounds,do,mem,pointer,recursion -Wunused -Wuninitialized -fopenmp -fbacktrace -lgomp -lgfortran -O3

### switch to these to use OpenBLAS ###
OPTIONS	= -fdump-core -fcheck=bounds,do,mem,pointer,recursion -Wunused -Wuninitialized -fexternal-blas -fopenmp -fbacktrace -lgomp -lgfortran -O3
LIBRARIES = -I/usr/local/Libraries/OpenBLAS/0.3.7/include -L/usr/local/Libraries/OpenBLAS/0.3.7/lib -lopenblas


OBJECTS = params.o searches_and_sorts.o octree.o ring_objects.o ring_procedures.o energy_terms.o ring_config.o read_write.o ring_polymer.o ring_grow.o ring_generate.o
PROGRAM	= ring_generate.exe 	#target- executable that is generated
ARCHIVE = ring_polymer

help:
	@echo Try:
	@echo make $(PROGRAM) .... to build the program named $(PROGRAM)
	@echo make clean .... to clean up, removing object files and program $(PROGRAM)
	@echo make listing .... to make a printable listing ... you may want to adjust the page length
	@echo make archive .... to make an archive tar file you can transfer or submit


%.o:	%.f90
	$(F90) $(OPTIONS) -c $<

### switch to this to not use OpenBLAS
# $(PROGRAM):	$(OBJECTS)
# 	$(F90) $(OBJECTS) $(OPTIONS) -o $(PROGRAM)

### switch to this to use OpenBLAS ###
$(PROGRAM):	$(OBJECTS)	
	$(F90) $(OBJECTS) $(OPTIONS) $(LIBRARIES) -o $(PROGRAM)	

profile:	$(OBJECTS)
	$(F90) $(OBJECTS) $(OPTIONS_PROFILE) $(LIBRARIES) -o $(PROGRAM)	

#	$(F90) $(OBJECTS) $(OPTIONS) -o $(PROGRAM)

#	$(F90) $(OBJECTS) $(OPTIONS) $(LIBRARIES) -o $(PROGRAM)	

clean:
	rm $(OBJECTS) $(PROGRAM)

listing:
	@echo Creating code listing named listing.txt ...
	pr -F --length=58 --page-width=80 -n    \
	   bd.f90 params.f90 geometry.f90 move.f90 Makefile > listing.txt
	@echo listing.txt is `cat listing.txt | wc -l` lines long.
	@echo Your listing file is ready.

archive:
	@echo Creating code archive tar-file $(ARCHIVE) ...
	tar cf $(ARCHIVE) bd Makefile
	@ls -l $(ARCHIVE)
	@echo Your archive file is ready.

