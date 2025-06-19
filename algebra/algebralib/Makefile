include ../../flags.mk

INCFLAGS=-Isrc -I$(FFTINC)

SRCDIR  = src
SRCEXT  = cpp
OBJDIR  = ./bin/obj
BINDIR  = ./bin

SRCS    := $(shell find $(SRCDIR) -name '*.$(SRCEXT)')
SRCDIRS := $(shell find $(SRCDIR) -name '*.$(SRCEXT)' -exec dirname {} \; | uniq)
OBJS    := $(patsubst %.$(SRCEXT),$(OBJDIR)/%.o,$(SRCS))

TARGET=$(BINDIR)/algebralib.a

all: $(TARGET)

$(TARGET): buildrepo $(OBJS)
    $(AR) -r "$@" $(OBJS) $(LIBS)

$(OBJDIR)/%.o: %.$(SRCEXT)
    $(CC) $(CFLAGS) $(CPPFLAGS) $(INCFLAGS) -fPIC -c -o "$@" "$<"

clean:
    $(RM) -rf $(BINDIR) $(OBJDIR) $(DEPS)

buildrepo:
    $(call make-repo)

define make-repo
for dir in $(SRCDIRS); \
    do \
    mkdir -p $(OBJDIR)/$$dir; \
    done
mkdir -p $(BINDIR)
endef
