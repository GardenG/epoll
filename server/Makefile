
###############################################################################
CC = g++
SRC_DIR = ./ ../wrap
INC_DIR = -I../wrap
LIB_DIR = 
LIBS = 
DESTDIR = ./
DESTNAME = server
OUTPUT = ./
###############################################################################

DEST = $(DESTDIR)$(DESTNAME)

SRCS = $(shell find $(SRC_DIR) -maxdepth 1 -name "*.cpp")
OBJS = $(patsubst %.cpp, $(OUTPUT)/%.o, $(SRCS))
DEPS = $(patsubst %.o, %.d, $(OBJS))

$(foreach dir, $(SRC_DIR), $(eval OBJ_DIR += $(OUTPUT)/$(dir)))

CPPFLAGS = -g -O2 $(INC_DIR) -Wall 
LDFLAGS = -g -O2 $(LIB_DIR) $(LIBS)

$(shell rm -f $(DEST))
$(shell mkdir -p $(DESTDIR))

all: $(DEST)
$(shell mkdir -p $(sort $(OBJ_DIR)))
include $(DEPS)

$(DEST): $(OBJS)
	$(CC) -o $@ $^ $(LDFLAGS)

$(OUTPUT)/%.o: %.cpp
	$(CC) -o $@ -c $< $(CPPFLAGS)

$(OUTPUT)/%.d: %.cpp
	@set -e; rm -f $@; \
	$(CC) -MM $(CPPFLAGS) $< > $@.$$$$; \
	sed 's,.*\.o[ :]*,$(patsubst %.d,%.o,$@) $@ : ,g' < $@.$$$$ > $@; \
	rm -f $@.$$$$

$(OUTPUT)/%.o: %.c
	$(CC) -o $@ -c $< $(CPPFLAGS)

$(OUTPUT)/%.d: %.c
	@set -e; rm -f $@; \
	$(CC) -MM $(CPPFLAGS) $< > $@.$$$$; \
	sed 's,.*\.o[ :]*,$(patsubst %.d,%.o,$@) $@ : ,g' < $@.$$$$ > $@; \
	rm -f $@.$$$$

clean:
	rm -rf $(OUTPUT)
	rm -rf $(DEST)
