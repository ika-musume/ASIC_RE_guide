# ASIC cell mugshots
This list is a compilation of ASIC cell mugshots I've found so far. Information is always subject to change. By default, cell names follow the <b>Squid ASIC cell naming convention</b>. I wrote the original name together if I can find it in original document. This may violate copyright, but masking rights only last 10 years, so there shouldn't be a problem - no one equates 80s gate array cell layout works with <i><b>Art</b></i>, right? 

# Squid ASIC cell naming convention
<i>Why Squid? - Watch Shinryaku Ika Musume S1 E1 and come again.</i>

- **INVERTER/BUFFER FAMILY**
    - **INV** - inverter
    - **BUF** - buffer
    - prefix **COMP** - _(e.g. COMPBUF...)_ with complementary output, **ONLY FOR BUF** 
    - suffix **P{n}** - _(e.g. INVP, INVP2...)_ power inverter, n can represent the number of parallel transistors, or it can simply represent the units of output from that ASIC.
    - suffix **D** - _(e.g. INVD, BUFD...)_ with RC delay

- **TRI-STATE INVERTER/BUFFER FAMILY**
    - **TSI** - tri-state inverter
    - **TSB** - tri-state buffer
    - suffix **PEN** - _(e.g. TSIPEN...)_ with positive enable
    - suffix **NEN** - _(e.g. TSBNEN...)_ with negative enable
    - suffix **P{n}** - _(e.g. TSBPPEN...)_ power inverter/buffer; This prefix is used in special cases. Typically, tri-state inverters use a four MOS stack, but I've seen cases where a transmission gate controls the output of the inverter. In this case, the output of the CMOS inverter is attenuated by the pass transistors, so use this suffix to distinguish between a 4-stack inverter cell and a 2-stack inverter + pass transistor cell _only_ if it's present.

- **AND/OR FAMILY**
    - **NAND{n}/NOR{n}** - n specifies the number of input ports
    - **AND{n}/OR{n}** - n specifies the number of input ports
    - prefix **COMP** - _(e.g. COMPOR2...)_ with complementary output
    - suffix **P{n}** - _(e.g. OR2P, NAND2P...)_ power inverter, n can represent the number of parallel transistors, or it can simply represent the units of output from that ASIC.
    - suffix **OD** - _(e.g. AND2OD...)_ open drain output. If the logic output is zero, the transistor pulls that signal to GND. If it is 1, the output is Hi-Z and the line is _released_.

- **AND-OR FAMILY**
    - **AOI{pqr...}** - AND-OR-INVERTER gate, p, q, r... specifies the number of inputs for each AND. _(e.g. AOI223 = ~{AND2|AND2|AND3})_
    - **OAI{pqr...}** - OR_AND-INVERTER gate, p, q, r... specifies the number of inputs for each OR. _(e.g. AOI223 = ~{OR2|OR2|OR3})_
    - **AO{pqr...}** - AND-OR gate, p, q, r... specifies the number of inputs for each AND.
    - **OA{pqr...}** - OR_AND gate, p, q, r... specifies the number of inputs for each OR.

- **EXCLUSIVE OR FAMILY**
    - **XOR{n}** - n specifies the number of input ports, normally 2
    - **XNOR{n}** - n specifies the number of input ports, normally 2

- **MULTIPLEXER FAMILY**

- **COMPLEX**
    - Often people create strange gates. This practice is most common in NMOS chips, but sometimes CMOS chips also create strange gates. See _AOI222(MF23 wired)_

To find the input and output ports, see the svgs I uploaded. You can find the specific cell with Ctrl+F and I basically write the names of all the cell input/output ports.

# NEC CMOS-5 gate array
<p align=center><img alt="LSI Logic SCAN power flip flop" src="./assets_list_main/nec_cmos5_topology.jpg" height="auto" width="640"></p>

There are variants of NEC CMOS-5, 5V, 5U, and there's no difference in the internal structure: it's a 1.2um double Al metal gate array.

This is a gate array with a rare 6-transistor cell. The only other gate array I've seen with 6T cells is Hitachi's BiCMOS gate array. I'm not sure what the advantage is compared to conventional 4T cells, I'd have to look at the patent or paper. All standard cells can be positioned in four different orientations: default, MX, MY, and R180.

**[NEC CMOS-5 cell list](./CELL_NEC_CMOS5.md)**

# Toshiba TC2xSC series standard cell
* TC21SC: 2.0um 1.5ns standard cell ASIC, no macros or embedded memory, <10k gates
* TC22SC: 2.0um 1.5ns standard cell ASIC with embedded memory or multiplier, <10k gates
* TC23SC: 1.5um 1.0ns standard cell ASIC with analog/CPU macros, <50k gates
* TC24SC: 1.0um ?
* TC25SC: 0.8um ?

A standard cell type ASIC developed in-house by Toshiba. Unlike the TC13/15/17G 4T gate array series, it was possible to place embedded ROM and RAM. The family was found in the 2.0-0.7um process node and was all double metal. The M2 is placed high that the polysilicon is not visible, so delayer is required in most cases. Konami SCC didn't require top metal shaving, but the sound chip from Roland or the math chip named SEI300 from Seibu Cup Soccer would definitely require delayering process.

**[Toshiba TC2xSC cell list](./CELL_TOSHIBA_TC2XSC.md)**


# Toshiba TC15/17/19 gate array

# LSI Logic LCA10/100k gate array
LSI Logic and Toshiba had a working relationship. I think LSI Logic was providing Toshiba with a more efficient ASIC structure and toolchain, and Toshiba was providing them with manufacturing services, so the master slice design of this gate array is shared by LSI Logic and Toshiba. 

Unfortunately, I haven't seen many chips in this family, so I don't know if they shared the same cell design, or how the cell layout changed as the process evolved. The combinational gates look similar in design, but I haven't looked at the flip flops yet.

The family doesn't have a huge standard cell like a 4-bit counter, and the macros that were supposedly provided by the EDA are scattered and disassembled into smaller unit cells. **I'll collect all the cells from LSI Logic and Toshiba in a doc below until I find a noticeable difference.**

**[LSI Logic LCA10/100k cell list](./CELL_LSI_LCA10_100K.md)**

# Yamaha single row standard cell(YM3xxx)

# Yamaha double row standard cell(YM6xxx, F7xxxx)