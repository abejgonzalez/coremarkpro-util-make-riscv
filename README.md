# coremarkpro-util-make-riscv

This repository provides the utility files to port CoreMark-Pro EEBMC to RISC-V.

**Purpose**

Port RISC-V (RV64G) to CoreMark-Pro.

**Requirements**

- You must have your own copy of EEMBC's [CoreMark-Pro](http://www.eembc.org/coremark/faq.php?b=pro).
- You must have installed the RISC-V tools (preferably, the Linux-ELF/glibc toolchain).

**Setup**

- Clone the repository from the [EEMBC GitHub repository](https://github.com/eembc/coremark.git)
- Copy the `riscv` folder into the top level directory of the `coremark` repository

```
git clone https://github.com/eembc/coremark.git
cp -r riscv/ /path/to/coremark/
```

**Building and Run Coremark Binaries**

make PORT_DIR=riscv

**Running Coremark on Spike**

By default, the `core_portme.mak` file sets `RUN` to use `spike pk`. Change `RUN` to suit your needs.

## Depreceated extra files from fork

**Making a Portable Directory**

If you would like to compile CMP and then move the binaries to an other platform (say, an FPGA), you can find the binaries in:

> coremarkpro_1.1.2743/builds/riscv64/riscv-gcc64/bin

Move this directory as desired.

**Invoking Binaries Manually**

Move to your directory of CMP binaries and set `RUN` as desired:

$RUN ./cjpeg-rose7-preset.riscv -c1 -v0 -i100
$RUN ./core.riscv -h -c1 -v0
$RUN ./linear_alg-mid-100x100-sp.riscv -c1 -v0
$RUN ./loops-all-mid-10k-sp.riscv -c1 -v0 -i20
$RUN ./nnet_test.riscv -c1 -v0
$RUN ./parser-125k.riscv -c1 -v0 -i50
$RUN ./radix2-big-64k.riscv -c1 -v0
$RUN ./sha-test.riscv -c1 -v0 -i75
$RUN ./zip-test.riscv -c1 -v0

`-c1` is single-core, `-v0` is verification turned off (vs. `-v1`), and `-i` is iteration count. 

**Getting a CMP Score**

If you are manually running CMP on a separate platform -- and not invoking it from the CMP build system -- you will not get a valid CMP score. Nonetheless, here is a hacky, terrible, lying script you can use to get a feel for your CMP performance. DO NOT REPORT THIS SCORE.

Place the output from each of your experiments in `${DIR}/${b}.out` where `${b}` is the name of the CMP benchmark as described from within `get-coremarkpro-score.sh`.

Modify this script as necessary to point to your CMP installation and then run it:

 ./get-coremarkpro-score.sh
 


