---
project: JustTheTip
type: decisions
---

# Architecture Decisions

## Use SPI As Primary Sensor Interface

Status: selected for first hardware pass.

Reason: five TMF8829 sensors at high zone counts need more bandwidth and cleaner multi-sensor control than I2C provides. SPI also avoids address reassignment during normal operation.

## Carry Optional I3C/I2C Pins

Status: selected.

Reason: the TMF8829 supports I3C/I2C-compatible operation, and spare FFC pins make future bring-up or alternate topologies easier.

## Use 16-Pin FFC Ports

Status: selected for planning.

Reason: 16 pins fit power, grounds, SPI, optional I3C/debug, EN, INT, and DET/ID without forcing risky multiplexing.

## Use Native STM32 USB For Main Data

Status: selected.

Reason: CP2102N is excellent for debug UART but should not be the primary pipe for five sensors.

## Use STM32H573ZI-Class MCU

Status: selected baseline.

Reason: enough performance, SRAM, USB, UCPD, I3C, and SPI resources for the first design.

## Keep PCB2 Minimal

Status: selected.

Reason: fingertip integration is mechanically constrained. PCB2 should contain only TMF8829, local passives, FFC, mounting, optional ID, and optical/mechanical features.
