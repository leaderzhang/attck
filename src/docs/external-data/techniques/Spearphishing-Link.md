
# Spearphishing Link

## Description

### MITRE Description

> Spearphishing with a link is a specific variant of spearphishing. It is different from other forms of spearphishing in that it employs the use of links to download malware contained in email, instead of attaching malicious files to the email itself, to avoid defenses that may inspect email attachments. 

All forms of spearphishing are electronically delivered social engineering targeted at a specific individual, company, or industry. In this case, the malicious emails contain links. Generally, the links will be accompanied by social engineering text and require the user to actively click or copy and paste a URL into a browser, leveraging [User Execution](https://attack.mitre.org/techniques/T1204). The visited website may compromise the web browser using an exploit, or the user will be prompted to download applications, documents, zip files, or even executables depending on the pretext for the email in the first place. Adversaries may also include links that are intended to interact directly with an email reader, including embedded images intended to exploit the end system directly or verify the receipt of an email (i.e. web bugs/web beacons). Links may also direct users to malicious applications  designed to [Steal Application Access Token](https://attack.mitre.org/techniques/T1528)s, like OAuth tokens, in order to gain access to protected applications and information.(Citation: Trend Micro Pawn Storm OAuth 2017)

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: intentionally left blank
* Permissions: None
* Platforms: ['Windows', 'macOS', 'Linux', 'Office 365', 'SaaS']
* Remote: intentionally left blank
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1192

## Potential Commands

```

```

## Commands Dataset

```

```

## Potential Detections

```json

```

## Potential Queries

```json

```

## Raw Dataset

```json

```

# Tactics


* [Initial Access](../tactics/Initial-Access.md)


# Mitigations

None

# Actors


* [APT33](../actors/APT33.md)

* [APT28](../actors/APT28.md)
    
* [Turla](../actors/Turla.md)
    
* [Cobalt Group](../actors/Cobalt-Group.md)
    
* [Elderwood](../actors/Elderwood.md)
    
* [APT32](../actors/APT32.md)
    
* [APT29](../actors/APT29.md)
    
* [Leviathan](../actors/Leviathan.md)
    
* [Night Dragon](../actors/Night-Dragon.md)
    
* [Patchwork](../actors/Patchwork.md)
    
* [Dragonfly 2.0](../actors/Dragonfly-2.0.md)
    
* [FIN4](../actors/FIN4.md)
    
* [OilRig](../actors/OilRig.md)
    
* [Magic Hound](../actors/Magic-Hound.md)
    
* [FIN8](../actors/FIN8.md)
    
* [APT39](../actors/APT39.md)
    
* [Stolen Pencil](../actors/Stolen-Pencil.md)
    
* [TA505](../actors/TA505.md)
    
* [Kimsuky](../actors/Kimsuky.md)
    
* [Machete](../actors/Machete.md)
    
