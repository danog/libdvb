# libdvb

libdvb is an interface library for DVB-API v5 devices in Linux.

Supports three types of delivery systems:

- Satellite: DVB-S, DVB-S2
- Terretrial: DVB-T, DVB-T2, ATSC, ISDB-T
- Cable: DVB-C

TODO:

- Cenelec EN 50221 - Common Interface Specification for Conditional Access and
  other Digital Video BroadcastingDecoder Applications
- DiSEqC 1.0
- DiSEqC 1.1
- EN 50494 - Unicable I
- EN 50607 - Unicable II

## FeDevice

Example DVB-S2 tune:

```rust
let fe = FeDevice::open_rw(0, 0)?;
set_dtv_properties!(
    fe, 
    DTV_DELIVERY_SYSTEM(SYS_DVBS2),
    DTV_FREQUENCY((11044 - 9750) * 1000),
    DTV_MODULATION(PSK_8),
    DTV_VOLTAGE(SEC_VOLTAGE_13),
    DTV_TONE(SEC_TONE_OFF),
    DTV_INVERSION(INVERSION_AUTO),
    DTV_SYMBOL_RATE(27500 * 1000),
    DTV_INNER_FEC(FEC_AUTO),
    DTV_PILOT(PILOT_AUTO),
    DTV_ROLLOFF(ROLLOFF_35),
    DTV_TUNE(()),
)?;
```

Frontend information:

```rust
let fe = FeDevice::open_ro(0, 0)?;
println!("{}", &fe);
```

Frontend status:

```rust
let fe = FeDevice::open_ro(0, 0)?;
let mut status = FeStatus::default();
status.read(&fe)?;
println!("{}", &status);
```
