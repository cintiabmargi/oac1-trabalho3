FLAGS = -O2 -Wall -Wextra -std=c99 -fopenmp -lm

.PHONY : all
all : edge_float edge_int edge_simd

image.o: image.c image.h
	gcc -c image.c $(FLAGS)

gradient_magnitude.o: gradient_magnitude.c gradient_magnitude.h
	gcc -c gradient_magnitude.c $(FLAGS)

main.o: main.c image.h gradient_magnitude.h
	gcc -c main.c $(FLAGS)

convolution_float.o: convolution_float.c convolution.h
	gcc -c convolution_float.c $(FLAGS)

convolution_int.o: convolution_int.c convolution.h
	gcc -c convolution_int.c $(FLAGS)

convolution_simd.o: convolution_simd.c convolution.h
	gcc -c convolution_simd.c $(FLAGS) -mavx -mavx512f

edge_float: main.o image.o gradient_magnitude.o convolution_float.o
	gcc -o edge_float main.o image.o gradient_magnitude.o convolution_float.o $(FLAGS)

edge_int: main.o image.o gradient_magnitude.o convolution_int.o
	gcc -o edge_int main.o image.o gradient_magnitude.o convolution_int.o $(FLAGS)

edge_simd: main.o image.o gradient_magnitude.o convolution_simd.o
	gcc -o edge_simd main.o image.o gradient_magnitude.o convolution_simd.o $(FLAGS)

clean:
	rm -f *.o images/magnitude.pgm edge_float edge_int edge_simd
