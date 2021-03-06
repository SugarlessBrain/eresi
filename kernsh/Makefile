##
## Makefile for kernsh
##
## Started on  Mon Jun  4 21:49:42 2007 pouik
##

include ../config.h

SRC			= main.c open.c close.c mem.c hash.c alloc.c mode.c autotypes.c tables.c misc.c virtm.c dump.c
OBJ			= $(SRC:.c=.o)
OBJ32			= $(SRC:.c=.32.o)
OBJ64			= $(SRC:.c=.64.o)
CC			?= gcc
RM			= rm -f
NAME			= kernsh
NAME32			= kernsh32 
NAME64			= kernsh64

CFLAGS32		+= -fPIC -g3 $(GSTABS) -Wall -Iinclude $(DYNOPT) $(BUILDOP) \
			 -I../libelfsh/include/  $(STATOPT2)   \
			 -I../libdump/include/ -I../libasm/include/          \
			 -I../e2dbg/include/ -I/usr/pkg/include/             \
			-I../libui/include/ -I../libmjollnir/include/        \
			-I../libaspect/include/ -I../librevm/include/        \
			-I../libedfmt/include/ -I../libstderesi/include/     \
			-I../libkernsh/include/ -I../libetrace/include/      \
			$(ASMOPT) -DERESI32 $(NCURSESLNOPT) $(READLNOPT)

CFLAGS64		+= -fPIC -g3 $(GSTABS) -Wall -Iinclude $(DYNOPT) $(BUILDOP) \
			 -I../libelfsh/include/ -I../libetrace/include/    \
			 -I../libdump/include/ -I../libasm/include/        \
			 -I../e2dbg/include/ -I/usr/pkg/include/           \
			-I../libui/include/ -I../libmjollnir/include/      \
			-I../libaspect/include/ -I../librevm/include/      \
			-I../libedfmt/include/  -I../libstderesi/include/  \
			-I../libkernsh/include/  $(STATOPT2) \
			$(ASMOPT) -DERESI64 $(NCURSESLNOPT) $(READLNOPT)

LDFLAGS32		+= -L../libedfmt/ -L../libelfsh/ -ledfmt32 -lelfsh32      \
			-L../libdump/ -L/usr/pkg/lib/ -L../libmjollnir/		  \
			-lmjollnir32 $(LPTHREAD) -L../libasm/ -lasm32             \
			-L../liballocproxy -L../libmjollnir/ -L../libui/ -lui32   \
			-L../libaspect/ -laspect32 -L../librevm/ -lrevm32         \
			-L../libetrace/ -letrace32				  \
			-L../libkernsh/ -lkernsh32 -L../libstderesi/ -lstderesi32 \
			-lallocproxy $(LDMJOLLNIR) $(DLOPT) -g3  	          \
			-L/usr/freeware/lib32/ $(DYNOPT) $(BITS) $(EXTRAOPT) 	  \
			$(LDDUMPOPT32) $(LDNCURSESLNOPT) $(LDREADLNOPT)

LDFLAGS64		+= -L../libelfsh/ -lelfsh64 -L../libdump/ -L/usr/pkg/lib/ \
			-L../libmjollnir/ -lmjollnir64 $(LPTHREAD) 	          \
			-L../libasm/ -lasm64 -L../libui/ -lui64 -g3 	          \
			-L../liballocproxy -L../libmjollnir/          		  \
			-L../libaspect/ -laspect64 -L../librevm/ -lrevm64         \
			-L../libetrace/ -letrace64				  \
			-L../libkernsh/ -lkernsh64 -L../libstderesi/ -lstderesi64 \
			-lallocproxy -L../libedfmt/ -ledfmt64 $(LDMJOLLNIR)       \
			$(DLOPT)  -L/usr/freeware/lib32/ $(DYNOPT) $(BITS)        \
			$(EXTRAOPT) $(LDDUMPOPT64) $(LDNCURSESLNOPT) $(LDREADLNOPT)

all			: all32 

$(NAME32)		: $(OBJ32) 
			$(CC) $(OBJ32) -o $(NAME32) $(LDFLAGS32) $(STATOPT)

$(NAME64)		: $(OBJ64) 
			@$(CC) $(OBJ64) -o $(NAME64) $(LDFLAGS64) $(STATOPT)

all32:	$(NAME32)
all64:  $(NAME64)

clean		       :
		       @$(RM) $(OBJ) *~ \#* *\# .\#* *.32.o *.64.o
		       @$(RM) include/*~ include/\#* include/*\# include/.\#*

fclean		       : clean
		       @$(RM) $(NAME) $(NAME32) $(NAME64) $(OBJ_DYN)

%.32.o : %.c
			$(CC) $(CFLAGS32) -c -o $@ $<
%.64.o : %.c
			$(CC) $(CFLAGS64) -c -o $@ $<
