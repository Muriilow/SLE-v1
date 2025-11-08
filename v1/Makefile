CC = gcc

CFLAGS = -O0 -g -fopenmp -DLIKWID_PERFMON -L$LIKWID_LIB -I$LIKWID_INCLUDE
LFLAGS = -lm -llikwid

PROG = cgSolver
MODULES = utils	sislin utils $(PROG)
OBJS = $(addsuffix .o,$(MODULES))
SRCS = $(addsuffix .c,$(MODULES)) $(addsuffix .h,$(MODULES))

# Lista de arquivos para distribuição
DISTFILES = *.c *.h Makefile README.md
DISTDIR = gvso24-mpb24

.PHONY: clean purge dist all

%.o: %.c %.h utils.h
	$(CC) -g -c $(CFLAGS) $<

$(PROG):  $(OBJS)
	$(CC) -g -o $@ $^ $(LFLAGS)

all: $()

clean:
	@echo "Limpando sujeira ....."
	@rm -rf core *~ *.bak *.o

purge: clean
	@echo "Fazendo a faxina ....."
	@rm -f a.out $(PROG)


dist: purge
	@echo "Gerando arquivo de distribuição ($(DISTDIR).tgz) ..."
	@ln -s . $(DISTDIR)
	@tar -chzvf $(DISTDIR).tgz $(addprefix ./$(DISTDIR)/, $(DISTFILES))
	@rm -f $(DISTDIR)
