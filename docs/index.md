# Welcome to this guide for Open Source Analog and Mixed-Signal Design!

This guide will help you understand the principles of mixed-signal design using open-source tools. We will cover topics such as:

- Digital design with SystemVerilog
- Analog design with SPICE with XSCHEM
- Cosimulation of digital and analog components with ngspice
- Visualization of simulation results with XSCHEM and Python

By the end of this guide, you will have a solid understanding of how to create and simulate mixed-signal designs using open-source tools.

## Useful Repositories

- [osams-playground](https://github.com/CedricHirschi/osams-playground) Repository containing the designs looked at in this guide.
- [osams-saradc](https://github.com/CedricHirschi/osams-saradc) Repository containing a SAR ADC design created using the workflow described in this guide.
- [IHP-Open-PDK](https://github.com/IHP-GmbH/IHP-Open-PDK) IHP's Open PDK used in this guide.
- [osams-docs](https://github.com/CedricHirschi/osams-docs) The repository containing this documentation. If you have suggestions or questions, please open an issue!

## Useful(ish) Tools

[XSCHEM Symbol Generator](./tools/symbol_gen.html){ .md-button }

Generates XSCHEM symbols from (System)Verilog modules. This simplifies the process of creating symbols for use in cosimulation with XSCHEM.

[YOSYS Online Playground](./tools/yosys_online.html){ .md-button }

A web-based interface for experimenting with YOSYS, an open-source synthesis tool. This playground allows you to write and work with (System)Verilog code directly in your browser.