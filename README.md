<p align="center">
  <a href="https://github.com/EnAccess/oseas26-mpm-openpaygo-plugin">
    <img
      src="https://drive.google.com/uc?id=1gtL_p7l3HbOcCzc09A7KW5d7B5qn-BDs"
      alt="Manage OpenPAYGO Compliant Devices on MicroPowerManager (MPM)"
      width="640"
    >
  </a>
</p>
<p align="center">
    October 26-27 | Open Source in Energy Access Symposium Hackathon | Kigali, Rwanda
</p>

---

# Manage OpenPAYGO Compliant Devices on MicroPowerManager (MPM)

Build a native OpenPAYGO integration (plugin) for
[MicroPowerManager (MPM)](https://micropowermanager.io/) so that a customer
transaction in MPM produces a valid OpenPAYGO token that activates a real device.

## Abstract and goal

MicroPowerManager (MPM) is an open-source CRM platform for managing off-grid
energy deployments — customers, payments, and device fleets. Today, it integrates
with proprietary vendor ecosystems such as Angaza, Calin, and SparkMeter through
its manufacturer-plugin system, allowing operators to provision and manage
PAYGo-enabled devices through vendor-specific APIs.

OpenPAYGO is an open-source protocol that standardizes Pay-As-You-Go token
generation for energy access devices: a customer's payment is converted into a
short numeric token which, when entered on the device, unlocks a corresponding
amount of usage credit. Because the standard is open, any manufacturer can
implement it — enabling interoperability across hardware vendors and reducing
dependence on proprietary ecosystems.

These two open technologies don't yet meet. MPM cannot natively generate or manage
OpenPAYGO tokens, so operators using OpenPAYGO-compliant hardware must leave MPM
and rely on separate vendor portals or custom tooling — fragmenting their
operational workflow and losing the main benefit of an open management platform.

The goal of this challenge is to bridge that gap: build a native OpenPAYGO
integration (plugin) for MPM so that a customer transaction in MPM produces a
valid OpenPAYGO token that activates a real device. Concretely, the integration
should enable MPM to:

- Register OpenPAYGO devices (device serial, secret key, starting counter) so MPM
  can generate tokens for them.
- Generate and manage OpenPAYGO tokens directly within MPM when a customer
  transaction occurs — including tracking the per-device token counter that
  prevents token replay.
- Support any hardware implementing the OpenPAYGO specification, regardless of
  manufacturer.
- Eliminate dependence on proprietary vendor portals for OpenPAYGO-enabled
  devices.

During the hackathon, the "real device" is the [OpenPAYGO Hardware Simulator](https://enaccess.github.io/OpenPAYGO-HW-sim/) — a
browser-based virtual PAYGo appliance that validates tokens using the real
OpenPAYGO cryptography and visibly activates (or rejects a token, with a reason)
on screen. It exports each virtual device's provisioning payload (JSON/QR), which
is what you register into MPM. Whatever works against the simulator will work
against real hardware.

By combining MPM's operational management capabilities with the OpenPAYGO
standard, the project provides a unified, open-source solution for managing PAYGo
energy assets across diverse hardware vendors — making off-grid energy management
more accessible, scalable, and interoperable.

## Expected outcomes

Create a Feature Request and an accompanying PR on the MPM repository that:

- Integrates an OpenPAYGO plugin into MPM, following the shape of MPM's existing
  manufacturer plugins so a maintainer can review and merge it.
- Registers OpenPAYGO appliances in MPM — an operator can take the provisioning
  payload (JSON/QR) exported by the [OpenPAYGO Hardware Simulator](https://enaccess.github.io/OpenPAYGO-HW-sim/) and register that
  device against a customer, no code changes required.
- Generates valid OpenPAYGO tokens from customer transactions — a payment
  recorded in MPM produces a token that, when entered into the simulator,
  activates the device for the corresponding amount of credit.
- Manages per-device token state correctly — the token counter advances across
  successive transactions, MPM's stored state stays in sync with the device, and
  an old token entered a second time is rejected by the device as a replay.
- Demonstrates the full round-trip end to end: provision a virtual device in the
  simulator → register it in MPM → drive a transaction → deliver the token →
  device activates. This should work across multiple devices, and for at least one
  device on its second or later token.

## Required knowledge

### Stack

- PHP/Laravel backend.
- Vue.js 2 frontend.
- OpenPAYGO protocol — reference libraries exist in Python and JavaScript; there
  is no PHP port today. How you bridge that gap (a PHP port, a sidecar service, or
  something else) is part of the challenge. Hardware-level protocol knowledge is
  **not** required.

### Programming languages

- PHP/Laravel
- JavaScript

### Helpful experiences

- Backend/API integration with PHP/Laravel.
- Knowledge of frontend development.
- Experience with the OpenPAYGO protocol or other token/OTP-style schemes
  (helpful, not required).

## Person of contact supporting this challenge

- Obinna Ikeh

## Getting started

- Join the OSEAS Discord server: <https://community.oseas.org/>
- Introduce yourself in the `#introductions` channel and join the relevant
  channels for this challenge:
  - `#micropowermanager`
- Read the documentation:
  - <https://enaccess.github.io/OpenPAYGO-docs/docs/>
  - <https://micropowermanager.io/get-started.html>
  - <https://github.com/EnAccess/micropowermanager/>
  - <https://github.com/EnAccess/OpenPAYGO-js>
  - <https://github.com/EnAccess/OpenPAYGO-HW-sim>
