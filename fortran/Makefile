# Makefile for program ring_generate
F90	= ${FC}

### switch to these to not use OpenBLAS ###
#OPTION	= -fdump-core -fcheck=bounds,do,mem,pointer,recursion -Wunused -Wuninitialized -fopenmp -fbacktrace -lgomp -lgfortran -O3

### switch to these to use OpenBLAS ###
OPTIONS	= -fdump-core -fcheck=bounds,do,mem,pointer,recursion -Wunused -Wuninitialized -fexternal-blas -fopenmp -fbacktrace -lgomp -lgfortran -O3
LIBRARIES = -I/usr/local/Libraries/OpenBLAS/0.3.9/include -L/usr/local/Libraries/OpenBLAS/0.3.9/lib -lopenblas


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
