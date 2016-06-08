include ../Config

TARGETS = diffusion-raw diffusion-zfp pgm simple speed testzfp zfp
LDFLAGS += -L../lib
LDLIBS += -lzfp -lm
CPPFLAGS += -I../array

all: $(TARGETS)

diffusion-raw: CPPFLAGS += -DWITHOUT_COMPRESSION
diffusion-raw: diffusion.cpp ../lib/libzfp.a
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) $< $(LDFLAGS) $(LDLIBS) -o $@

diffusion-zfp: diffusion.cpp ../lib/libzfp.a
	$(CXX) $(CPPFLAGS) $(CXXFLAGS) $< $(LDFLAGS) $(LDLIBS) -o $@

pgm:    pgm.o
simple: simple.o
speed:  speed.o

testzfp: testzfp.cpp fields.o ../lib/libzfp.a
	$(CXX) $(CXXFLAGS) -I../array testzfp.cpp fields.o -L../lib -lzfp -o testzfp

## 'fields.o' is handled by implicit rule

zfp: zfp.c ../lib/libzfp.a
	$(CC) $(CFLAGS) zfp.c -L../lib -lzfp -lm -o zfp

test: testzfp
	./testzfp

clean:
	rm -f $(TARGETS) fields.o
