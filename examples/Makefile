EXAMPLES = $(patsubst %.cpp,bin/%,$(wildcard *.cpp))

CXX=clang++
CXXFLAGS +=\
	 -std=c++11 -stdlib=libc++\
	 -Wall\
	 -Wpedantic\
	 -Werror\
	-D_XOPEN_SOURCE=1\
	-Iinclude\
	-I../include\
	-framework CoreFoundation\
	-framework CoreServices\
	deps/http-parser/http_parser_g.o\
	deps/uv/libuv.la

CXXFLAGS += -g

all: $(EXAMPLES)

bin/%: %.cpp ../include util.h deps/http-parser/http_parser_g.o deps/uv/libuv.la
	$(CXX) $(CXXFLAGS) -o $@ $<


deps/http-parser/http_parser_g.o: deps/http-parser/Makefile
	$(MAKE) -C $(@D)

deps/uv/libuv.a: deps/uv/Makefile
	$(MAKE) -C $(@D)

deps/uv/Makefile deps/http-parser/Makefile:
	git submodule init && git submodule update
