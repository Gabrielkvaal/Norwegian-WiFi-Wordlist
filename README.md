# Norwegian WiFi Wordlist V3

**Optimized wordlist for cracking default WiFi passwords from Norwegian ISPs and common routers.**

## Version 3.0 - Major Update

### What's New in V3
- **TELENOR PATTERN CONFIRMED**: Based on 100% verified default password sample
- **Completely new Telenor algorithm**: V2 was wrong, V3 is based on real data
- **Optimized priority ordering**: Most likely passwords first

---

## Quick Stats

| Metric | Value |
|--------|-------|
| Total passwords | 16,100,197 |
| File size (uncompressed) | 231 MB |
| File size (gzip) | 35 MB |
| Estimated crack time (RTX 3080) | ~20 minutes |
| Patterns included | 3 (Telenor, Netgear, Weak) |

---

## Confirmed Patterns

### 1. TELENOR (Norwegian ISP - 35% market share)

**Pattern**: `[NorwegianCompound][1digit][TechnicalWord][1digit]`

**Confirmed Sample**: `Hjerteonde9Parameter6`

| Component | Example | Description |
|-----------|---------|-------------|
| Word 1 | `Hjerteonde` | Norwegian compound word (heart-evil) |
| Digit 1 | `9` | Single digit 0-9 |
| Word 2 | `Parameter` | Technical/scientific term |
| Digit 2 | `6` | Single digit 0-9 |

**Characteristics**:
- PascalCase (each word capitalized)
- ~20-22 characters total
- No special characters
- Mix of Norwegian and international words

**Keyspace**: ~2 million passwords

### 2. NETGEAR (Common retail router)

**Pattern**: `[adjective][noun][3digits]`

**Example**: `quietunicorn604`

| Component | Example | Description |
|-----------|---------|-------------|
| Adjective | `quiet` | English adjective (lowercase) |
| Noun | `unicorn` | English noun (lowercase) |
| Numbers | `604` | 3 digits, 500-699 most common |

**Keyspace**: ~14 million passwords

### 3. WEAK PASSWORDS

Common weak passwords including:
- Universal: `12345678`, `password`, `qwerty123`
- Norwegian: `passord123`, `hemmelig1`, `velkommen`
- Cities: `oslo12345`, `bergen2024`, `trondheim1`
- Names: `Ole2024`, `Kari2024`, `Erik12345`
- Football: `Rosenborg1`, `Brann12345`, `Viking2024`

---

## Patterns NOT in Wordlist (Use Hashcat Masks)

### ZHONE (Telenor fiber)
```
Pattern: znid + 9 digits
Example: znid307623039
Keyspace: 1 billion (too large for wordlist)

Command:
hashcat -m 22000 -a 3 capture.hc22000 znid?d?d?d?d?d?d?d?d?d
```

### ALTIBOX/ZyXEL
```
Pattern: 8 chars mixed case a-zA-Z
Example: pEquPPKY
Keyspace: 53 trillion (requires mask attack)

Command:
hashcat -m 22000 -a 3 capture.hc22000 -1 ?l?u ?1?1?1?1?1?1?1?1
```

### THOMSON/SpeedTouch (Telia)
```
Pattern: 10 hex chars
Example: 5A3B2C1D0E
Keyspace: 1 trillion (use keygen tool)

Tool: https://github.com/routerkeygen/routerkeygenPC
```

---

## Usage

### Aircrack-ng
```bash
aircrack-ng -w norwegian_wifi_v3.txt capture.cap
```

### Hashcat (recommended)
```bash
# Convert capture to hashcat format
hcxpcapngtool -o capture.hc22000 capture.pcapng

# Run wordlist attack
hashcat -m 22000 -a 0 capture.hc22000 norwegian_wifi_v3.txt

# With rules for variations
hashcat -m 22000 -a 0 capture.hc22000 norwegian_wifi_v3.txt -r best64.rule
```

### Hashcat + Masks (combined attack)
```bash
# First try wordlist
hashcat -m 22000 -a 0 capture.hc22000 norwegian_wifi_v3.txt

# Then try Zhone mask
hashcat -m 22000 -a 3 capture.hc22000 znid?d?d?d?d?d?d?d?d?d

# Then try Altibox mask
hashcat -m 22000 -a 3 capture.hc22000 -1 ?l?u ?1?1?1?1?1?1?1?1
```

---

## Priority Order

The wordlist is ordered for fastest success:

1. **Weak passwords** (lines 1-97) - instant wins
2. **Telenor passwords** (lines 98-2,024,197) - Norwegian ISP dominant
3. **Netgear passwords** (lines 2,024,198-16,100,197) - common retail

Within each section, digit combinations are prioritized:
- Single digits: 5, 6, 4, 7, 3, 8, 2, 9, 1, 0
- Triple digits: 500-699 first, then 400-499, 700-899, etc.

---

## Hardware Performance

| GPU | Hash Rate | Time for Full Wordlist |
|-----|-----------|----------------------|
| RTX 3080 | ~800 kH/s | ~20 minutes |
| RTX 3090 | ~950 kH/s | ~17 minutes |
| RTX 4090 | ~1.4 MH/s | ~12 minutes |

---

## Files Included

| File | Size | Description |
|------|------|-------------|
| `norwegian_wifi_v3.txt` | 231 MB | Full wordlist |
| `norwegian_wifi_v3.txt.gz` | 35 MB | Compressed version |
| `norwegian_wifi_v3_sample_100k.txt` | 2.2 MB | Sample (first 100k) |

---

## Changelog

### V3.0 (2026-04-18)
- **BREAKING**: Completely new Telenor pattern based on confirmed sample
- Telenor: `[Compound][1dig][Technical][1dig]` (was `[adj][3dig][noun]`)
- Added 101 Norwegian compound words
- Added 101 technical/scientific terms
- Optimized digit priority ordering
- Total: 16.1M passwords

### V2.0 (2026-01-27)
- Added Netgear pattern (14M passwords)
- Added Norwegian weak passwords
- Total: 20.1M passwords

### V1.0 (Initial)
- Basic Norwegian words and names

---

## Research Sources

- Confirmed Telenor sample from real router
- Netgear pattern from: https://github.com/LivingInSyn/netgear_hashcat_wordlist
- RouterKeygen algorithms: https://github.com/routerkeygen/routerkeygenPC
- WPA keyspace research: https://github.com/sheimo/Wifi-WPA-Keyspace-List

---

## Legal Disclaimer

This wordlist is for **authorized security testing only**. Only use on networks you own or have explicit written permission to test. Unauthorized access to computer networks is illegal.

---

## Author

Gabriel Kvaal  
https://github.com/Gabrielkvaal/Norwegian-WiFi-Wordlist

---

## Contributing

Have confirmed default password samples from Norwegian ISPs? Open an issue with:
- ISP name
- Router model (if known)
- Default password (anonymized if needed)
- Confirmation it's unmodified default
