include ../lib/config.mk

#CC += -faddress-sanitizer -fno-omit-frame-pointer
LDFLAGS := -L"../lib" -lccv $(LDFLAGS)
CFLAGS := -O3 -Wall -I"../lib" $(CFLAGS)
NVFLAGS := -O3 -I"../lib" $(NVFLAGS)

TARGETS = bbffmt msermatch siftmatch bbfcreate bbfdetect swtcreate swtdetect dpmcreate dpmdetect convert tld icfcreate icfdetect icfoptimize cifar-10 image-net

all: libccv.a $(TARGETS) cwc-bench

clean:
	${MAKE} clean -C ../lib ; rm -f *.o $(TARGETS)

cwc-bench: %: %.o cwc-bench-runtime.o libccv.a
	$(CC) -o $@ cwc-bench-runtime.o $< $(LDFLAGS)

$(TARGETS): %: %.o libccv.a
	$(CC) -o $@ $< $(LDFLAGS)

libccv.a:
	${MAKE} -C ../lib

%.o: %.c ../lib/ccv.h
	$(CC) $< -o $@ -c $(CFLAGS)

%.o: %.cu ../lib/ccv.h ../lib/cuda/*.h ../lib/cuda/*.cu
	$(NVCC) $< -o $@ -c $(NVFLAGS)
