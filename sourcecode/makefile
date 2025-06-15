.PHONY: all upx ptf web webrun test dbg clean

name = FishtankDungeons
SHELL := /bin/bash

all:
	cc main.c -Ofast -lSDL2 -lGLESv2 -lEGL -lm -o $(name)_linux

upx:
	strip --strip-unneeded $(name)_linux
	upx --lzma --best $(name)_linux

ptf:
	cc assets/ptf.c -lm -Ofast -march=native -o assets/ptf

web:
	mkdir -p web
	source ~/emsdk/emsdk_env.sh && emcc main.c -DWEB -O3 --closure 1 -s FILESYSTEM=0 -s USE_SDL=2 -s ENVIRONMENT=web -s TOTAL_MEMORY=1024MB -o web/index.html --shell-file t.html && emrun web/index.html

webrun:
	source ~/emsdk/emsdk_env.sh && emrun web/index.html

test:
	gcc main.c -Ofast -lSDL2 -lGLESv2 -lEGL -lm -o /tmp/$(name)_test
	/tmp/$(name)_test
	rm /tmp/$(name)_test

clean:
	rm -f $(name)_linux
	rm -f web/index.html
	rm -f web/index.js
	rm -f web/index.wasm
	rm -f assets/ptf