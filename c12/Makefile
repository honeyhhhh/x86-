NASM = nasm
DD = dd
BOCHS = bochs
BXIMAGE = bximage
BOCHSRC = ./bochsrc

DIR_ASM = ./asm
DIR_BIN = ./bin
DIR_IMG = ./img

ASMs = $(wildcard $(DIR_ASM)/*.asm)
BINs = $(patsubst %.asm,$(DIR_BIN)/%.bin,$(notdir $(ASMs)))
BXIMG = $(DIR_IMG)/c12.img
ALLDIRs := $(DIR_ASM) $(DIR_BIN) $(DIR_IMG)

bochs: $(BINs)
	@$(BXIMAGE) -mode=create -hd=16 -q $(BXIMG)
	@$(DD) if=$(DIR_BIN)/c12_mbr.bin of=$(BXIMG) conv=notrunc
	#@$(DD) if=$(DIR_BIN)/c12.bin of=$(BXIMG) seek=100 conv=notrunc
	$(BOCHS) -q -f $(BOCHSRC)

MK_DIRs = \
for i in $(ALLDIRs); \
	do (if [ -d $$i ]; then exit 0; else mkdir $$i; fi); \
done



$(DIR_BIN)/%.bin: $(DIR_ASM)/%.asm
	@$(MK_DIRs)
	$(NASM) -f bin $< -o $@




.PHONY: clean

clean:
	-rm -rf $(DIR_BIN) $(DIR_IMG)
