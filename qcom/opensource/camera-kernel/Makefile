# Makefile for use with Android's kernel/build system

<<<<<<< HEAD
KBUILD_OPTIONS += CAMERA_KERNEL_ROOT=$(shell pwd)
KBUILD_OPTIONS += KERNEL_ROOT=$(ROOT_DIR)/$(KERNEL_DIR)
=======
CAMERA_GENERATED_DIR := $(OUT_DIR)/camera-kernel
CAMERA_GENERATED_H := $(CAMERA_GENERATED_DIR)/cam_generated_h

KBUILD_OPTIONS += CAMERA_KERNEL_ROOT=$(KERNEL_SRC)/$(M)
KBUILD_OPTIONS += CAMERA_GENERATED_DIR=$(CAMERA_GENERATED_DIR)
KBUILD_OPTIONS += KERNEL_ROOT=$(KERNEL_SRC)
>>>>>>> 41241ba52e (sm8550-modules: camera-kernel: Use OUT_DIR for generated headers)
KBUILD_OPTIONS += MODNAME=camera

all: modules

CAMERA_COMPILE_TIME = $(shell date)
CAMERA_COMPILE_BY = $(shell whoami | sed 's/\\/\\\\/')
CAMERA_COMPILE_HOST = $(shell uname -n)

cam_generated_h: $(CAMERA_GENERATED_H)

$(CAMERA_GENERATED_H): $(shell find . -iname "*.c") $(shell find . -iname "*.h") $(shell find . -iname "*.mk")
	mkdir -p $(CAMERA_GENERATED_DIR)
	echo '#define CAMERA_COMPILE_TIME "$(CAMERA_COMPILE_TIME)"' > $(CAMERA_GENERATED_H)
	echo '#define CAMERA_COMPILE_BY "$(CAMERA_COMPILE_BY)"' >> $(CAMERA_GENERATED_H)
	echo '#define CAMERA_COMPILE_HOST "$(CAMERA_COMPILE_HOST)"' >> $(CAMERA_GENERATED_H)

modules: cam_generated_h

modules dtbs:
	$(MAKE) -C $(KERNEL_SRC) M=$(M) modules $(KBUILD_OPTIONS)

modules_install:
	$(MAKE) M=$(M) -C $(KERNEL_SRC) modules_install

clean:
	$(MAKE) -C $(KERNEL_SRC) M=$(M) clean
