MODULE=example
svpath=vsrc
tb_c_path=csrc

.PHONY:sim
sim: waveform.vcd

.PHONY:verilate
verilate: .stamp.verilate

.PHONY:build
build: obj_dir/V$(MODULE)

.PHONY:waves
waves: waveform.vcd
	@echo
	@echo "### WAVES ###"
	gtkwave waveform.vcd

waveform.vcd: ./obj_dir/V$(MODULE)
	@echo
	@echo "### SIMULATING ###"
	@./obj_dir/V$(MODULE)

./obj_dir/V$(MODULE): .stamp.verilate
	@echo
	@echo "### BUILDING SIM ###"
	make -C obj_dir -f V$(MODULE).mk V$(MODULE)

.stamp.verilate: $(svpath)/$(MODULE).v  $(tb_c_path)/tb_$(MODULE).cpp
	@echo
	@echo "### VERILATING ###"
	verilator -Wall --trace -cc $(svpath)/$(MODULE).v --exe $(tb_c_path)/tb_$(MODULE).cpp
	@touch .stamp.verilate

.PHONY:lint
lint: $(svpath)/$(MODULE).v .v
	verilator --lint-only $(svpath)/$(MODULE).v .v

all:
	@echo "Write this Makefile by your self."

sim_temp:
	$(call git_commit, "sim RTL") # DO NOT REMOVE THIS LINE!!!
	@echo "Write this Makefile by your self."


.PHONY: clean
clean:
	rm -rf .stamp.*;
	rm -rf ./obj_dir
	rm -rf waveform.vcd

include ../Makefile
