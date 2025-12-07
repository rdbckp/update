# SPDX-License-Identifier: GPL-2.0
OBJECT_FILES_NON_STANDARD := y
CFLAGS_empty.c += $(DISABLE_LTO)

hostprogs-y	:= modpost elfconfig
always		:= $(hostprogs-y) empty.c

modpost-objs	:= modpost.o file2alias.o sumversion.o

devicetable-offsets-file := devicetable-offsets.h

$(obj)/$(devicetable-offsets-file): $(obj)/devicetable-offsets.c FORCE
	$(call filechk,offsets,__DEVICETABLE_OFFSETS_H__)

targets += $(devicetable-offsets-file) devicetable-offsets.c

# dependencies on generated files need to be listed explicitly

$(obj)/modpost.o $(obj)/file2alias.o $(obj)/sumversion.o: $(obj)/elfconfig.c
$(obj)/file2alias.o: $(obj)/$(devicetable-offsets-file)

quiet_cmd_elfconfig = MKELF   $@
      cmd_elfconfig = $(obj)/elfconfig < $< > $@

$(obj)/elfconfig.c: $(obj)/empty.c $(obj)/elfconfig FORCE
	$(call if_changed,elfconfig)

targets += elfconfig.c
