obj-m += memflow.o
memflow-objs := main.o vmtools.o
MCFLAGS += -O3
ccflags-y += ${MCFLAGS}
CC += ${MCFLAGS}
KDIR := /lib/modules/$(shell uname -r)/build
ifndef OUT_DIR
	KOUTPUT := $(PWD)/../build
else
	KOUTPUT := $(OUT_DIR)
endif

KOUTPUT_MAKEFILE := $(KOUTPUT)/Makefile

all: $(KOUTPUT_MAKEFILE)
	@echo "$(KOUTPUT)"

	make -C $(KDIR) M=$(KOUTPUT) src=$(PWD) modules

$(KOUTPUT):
	mkdir -p "$@"

$(KOUTPUT_MAKEFILE): $(KOUTPUT)
	touch "$@"

clean:
	make -C $(KDIR) M=$(KOUTPUT) src=$(PWD) clean
	$(shell rm $(KOUTPUT_MAKEFILE))
	rmdir $(KOUTPUT)
