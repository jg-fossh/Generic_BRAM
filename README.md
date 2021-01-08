# Generic BRAM Synthesizable Unit Specifications

Document        | Metadata
:-------------- | :------------------
_Version_       | v1.0.0
_Prepared by_   | Jose R Garcia
_Created_       | 2021/01/08 11:18:42
_Last modified_ | 2021/01/08 11:18:42
_Project_       | N/A

## Overview

Most modern synthesis tools can infer this code as an array of BRAM and map it to specific technologies.

## Table Of Contents

<!-- TOC -->

 - [Generic RAM Synthesizable Unit Specifications](#generic-ram-synthesizable-unit-specifications)

  - [Overview](#overview)
  - [Table Of Contents](#table-of-contents)
  - [1 Syntax and Abbreviations](#1-syntax-and-abbreviations)
  - [2 Design](#2-design)
  - [3 Clocks and Resets](#3-clocks-and-resets)
  - [4 Interfaces](#4-interfaces)

    - [4.1 Memory Interface](#41-memory-interface)

  - [5 Generic Parameters](#5-generic-parameters)

<!-- /TOC -->

 ## 1 Syntax and Abbreviations

Characters  | Definition
:---------- | :----------------------------
0b0         | Binary number syntax
0x0000_0000 | Hexadecimal number syntax
bit         | Single binary digit (0 or 1)
BYTE        | 8-bits wide data unit
BRAM        | Block Random Access Memory
FPGA        | Field Programmable Gate Array
LSB         | Least Significant bit
MSB         | Most Significant bit

## 2 Design

A generic BRAM module. Most modern synthesis tools can infer this code as an array of BRAM and map it to specific technologies. In this implementation the read enable is inferred to always be asserted. It also includes the option of loading a an memory initialization file.

## 3 Clocks and Resets

Signals  | Initial State | Direction | Definition
:------- | :-----------: | :-------: | :---------------------
`i_wclk` |      N/A      |    In     | Write interface clock.
`i_rclk` |      N/A      |    In     | Read interface clock.

## 4 Interfaces

The Dual Port RAM has a Dual synchronous memory interface for input and output.

### 4.1 Memory Interface

Signals   | Initial State |      Dimension      | Direction | Definition
:-------- | :-----------: | :-----------------: | :-------: | :-------------------------------------------------------------------------------------------
`i_we`    |      N/A      |        1-bit        |    In     | Write enable. Indicates the current write data is valid and it is to be stored into memory.
`i_waddr` |      N/A      | `[P_ADDRESS_MSB:0]` |    In     | Write Address. Address input to this addressable memory space.
`i_raddr` |      N/A      | `[P_ADDRESS_MSB:0]` |    In     | Read Address. Address input to this addressable memory space.
`i_wdata` |      N/A      |  `[P_DATA_MSB:0]`   |    In     | Write Data. Data input to this addressable memory space.
`o_rdata` |      N/A      |  `[P_DATA_MSB:0]`   |    In     | Read Data. Data output of this addressable memory space.

## 5 Generic Parameters

Parameters           | Description
:------------------- | :----------------------------------------------------------------------
`P_BRAM_DATA_MSB`    | Most significant bit of the data bus.
`P_BRAM_ADDRESS_MSB` | Most significant bit of the memory address.
`P_BRAM_DEPTH`       | Number of words the memory holds.
`P_BRAM_HAS_FILE`    | 0=Don't pre-load data into memory. 1=Pre-load values into memory block.
`P_BRAM_INIT_FILE`   | Initialization file name. example: {"./bram.mem"}
