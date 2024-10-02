#makefile

start:
	rm bin/*.*

serial:
	${LLVM}/bin/clang++ --target=riscv64-unknown-elf  -march=rv64g -mepi -O2 -fno-vectorize -c -o src/blackscholes_serial.o src/blackscholes.cpp
	${LLVM}/bin/clang++ --target=riscv64-unknown-elf  -march=rv64g -mepi -O2 -fno-vectorize -o bin/blackscholes_serial.exe src/blackscholes_serial.o -lm
	rm src/*.o
	${LLVM}/bin/llvm-objdump --mattr=+m,+f,+d,+a,+c -ds  bin/blackscholes_serial.exe > bin/blackscholes_serial.dump

vector:
	#${LLVM}/bin/clang++ --target=riscv64-unknown-elf --verbose -march=rv64g -mepi -DUSE_RISCV_VECTOR -O2 -fno-vectorize -c -o src/blackscholes.o src/blackscholes.cpp ; \
		${LLVM}/bin/clang++ --target=riscv64-unknown-elf  -march=rv64g -mepi -DUSE_RISCV_VECTOR -O2 -fno-vectorize -S -o src/blackscholes.s	src/blackscholes.cpp ; \
		
	${LLVM}/bin/clang++ --target=riscv64-unknown-elf --verbose -march=rv64g -mepi -DUSE_RISCV_VECTOR -O2 -fno-vectorize -o bin/blackscholes_vector.exe src/blackscholes.cpp -lm --gcc-toolchain=/software-local/riscv-llvm-EPI-2024-09-28; 
#	i
	#--gcc-toolchain=/software-local/riscv-gcc-13 -I/software-local/riscv-gcc-13/lib/gcc/riscv64-unknown-linux-gnu/13.1.1/include -I/software-local/riscv-gcc-13/lib/gcc/riscv64-unknown-linux-gnu/13.1.1/include-fixed -I/software-local/riscv-gcc-13/lib/gcc/riscv64-unknown-linux-gnu/13.1.1/../../../../riscv64-unknown-linux-gnu/include -I/software-local/riscv-gcc-13/sysroot/usr/include -L/software-local/riscv-gcc-13/riscv64-unknown-linux-gnu/lib64/lp64d -L/software-local/riscv-gcc-13/riscv64-unknown-linux-gnu/lib64 -L/software-local/riscv-gcc-13/riscv64-unknown-linux-gnu/lib ; \
	rm src/*.o ; \
	${LLVM}/bin/llvm-objdump --mattr=+m,+f,+d,+a,+c,+experimental-v -ds bin/blackscholes_vector.exe > bin/blackscholes_vector.dump ;

clean:
	rm bin/*.dump; \
	rm bin/*.exe;
