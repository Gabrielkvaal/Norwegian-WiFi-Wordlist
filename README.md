# Norwegian WiFi Wordlist 🇳🇴

A 20 million entry wordlist optimized for Norwegian WiFi networks, designed for authorized penetration testing and security research.

## Download

**Full wordlist (20M passwords):** [Download from Releases](https://github.com/Gabrielkvaal/Norwegian-WiFi-Wordlist/releases/download/v2.0/norwegian_wifi_v2.zip)

## What's New in v2.0

- **Telenor pattern discovered**: `adjective + 3digits + noun` (Norwegian with æøå)
- **ISP priority**: Telenor tested first (35-40% market share)
- **Number priority**: 5XX-6XX tested first (statistical analysis)
- **20.1M passwords** with research-backed patterns

## Features

- **20M passwords** prioritized from most to least likely
- **Norwegian-specific patterns**: names, places, football teams, cultural words
- **ISP default patterns**: Telenor (adj+digits+noun), Netgear (adj+noun+digits)
- **Keyboard walks**: Norwegian keyboard layout patterns

## Quick Start
```bash
# Download
wget https://github.com/Gabrielkvaal/Norwegian-WiFi-Wordlist/releases/download/v2.0/norwegian_wifi_v2.zip
unzip norwegian_wifi_v2.zip

# Use with wifite
wifite --dict norwegian_wifi_v2.txt --no-wps --kill

# Use with hashcat
hashcat -m 22000 -a 0 capture.hc22000 norwegian_wifi_v2.txt

# Use with aircrack-ng
aircrack-ng -w norwegian_wifi_v2.txt capture.cap
```

## ISP Default Password Patterns

### Telenor (35-40% market share in Norway)
```
Structure: adjective + 3digits + noun
Examples:  grå542rev, blå891bjørn, mørk367snø
Language:  Norwegian (with æøå)
```

### Netgear (Common worldwide)
```
Structure: adjective + noun + 3digits  
Examples:  quietunicorn604, reddragon123
Language:  English
```

## Priority Structure

1. **Top weak passwords** - qwerty123, 123456, passord
2. **Keyboard walks** - Norwegian layout patterns (æøå)
3. **Telenor patterns** - grå542rev, blå891bjørn (~5.8M)
4. **Netgear patterns** - quietunicorn604, reddragon123 (~14.3M)
5. **Name + year** - Ole2024, Lars1990, Kari2023
6. **Place names** - Oslo123, Bergen2024, Tromsø
7. **Football teams** - Rosenborg, Vålerenga, Lillestrøm
8. **Norwegian words** - fjord, hytte, sommer + variants
9. **Compound words** - sommerhytte, fjelltur
10. **L33t speak** - h3mm3lig, pa55ord

## Sample

See `norwegian_wifi_sample_100k.txt` for the first 100,000 entries.

## Research Sources

- 26+ confirmed Netgear passwords (eBay photos, hashcat forum)
- WoNDeR-List research (Mike Allen)
- NetgearKiller wordlist analysis (fyy0r)
- NordPass Norwegian password statistics
- First-hand Telenor router observation

## Legal Disclaimer

⚠️ **For authorized security testing only.** 

Only use this wordlist on networks you own or have explicit written permission to test. Unauthorized access to computer networks is illegal.

## License

MIT License - See [LICENSE](LICENSE) for details.
