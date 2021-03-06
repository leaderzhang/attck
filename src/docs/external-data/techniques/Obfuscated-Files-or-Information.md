
# Obfuscated Files or Information

## Description

### MITRE Description

> Adversaries may attempt to make an executable or file difficult to discover or analyze by encrypting, encoding, or otherwise obfuscating its contents on the system or in transit. This is common behavior that can be used across different platforms and the network to evade defenses.

Payloads may be compressed, archived, or encrypted in order to avoid detection. These payloads may be used during Initial Access or later to mitigate detection. Sometimes a user's action may be required to open and [Deobfuscate/Decode Files or Information](https://attack.mitre.org/techniques/T1140) for [User Execution](https://attack.mitre.org/techniques/T1204). The user may also be required to input a password to open a password protected compressed/encrypted file that was provided by the adversary. (Citation: Volexity PowerDuke November 2016) Adversaries may also used compressed or archived scripts, such as Javascript.

Portions of files can also be encoded to hide the plain-text strings that would otherwise help defenders with discovery. (Citation: Linux/Cdorked.A We Live Security Analysis) Payloads may also be split into separate, seemingly benign files that only reveal malicious functionality when reassembled. (Citation: Carbon Black Obfuscation Sept 2016)

Adversaries may also obfuscate commands executed from payloads or directly via a [Command-Line Interface](https://attack.mitre.org/techniques/T1059). Environment variables, aliases, characters, and other platform/language specific semantics can be used to evade signature based detections and whitelisting mechanisms. (Citation: FireEye Obfuscation June 2017) (Citation: FireEye Revoke-Obfuscation July 2017) (Citation: PaloAlto EncodedCommand March 2017)

Another example of obfuscation is through the use of steganography, a technique of hiding messages or code in images, audio tracks, video clips, or text files. One of the first known and reported adversaries that used steganography activity surrounding [Invoke-PSImage](https://attack.mitre.org/software/S0231). The Duqu malware encrypted the gathered information from a victim's system and hid it into an image followed by exfiltrating the image to a C2 server. (Citation: Wikipedia Duqu) By the end of 2017, an adversary group used [Invoke-PSImage](https://attack.mitre.org/software/S0231) to hide PowerShell commands in an image file (png) and execute the code on a victim's system. In this particular case the PowerShell code downloaded another obfuscated script to gather intelligence from the victim's machine and communicate it back to the adversary. (Citation: McAfee Malicious Doc Targets Pyeongchang Olympics)

## Additional Attributes

* Bypass: ['Host forensic analysis', 'Signature-based detection', 'Host intrusion prevention systems', 'Application whitelisting', 'Process whitelisting', 'Log analysis', 'Whitelisting by file name or path']
* Effective Permissions: None
* Network: intentionally left blank
* Permissions: None
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: intentionally left blank
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1027

## Potential Commands

```
sh -c "echo ZWNobyBIZWxsbyBmcm9tIHRoZSBBdG9taWMgUmVkIFRlYW0= > /tmp/encoded.dat"
cat /tmp/encoded.dat | base64 -d > /tmp/art.sh
chmod +x /tmp/art.sh
/tmp/art.sh

$OriginalCommand = 'Write-Host "Hey, Atomic!"'
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)
$EncodedCommand =[Convert]::ToBase64String($Bytes)
$EncodedCommand
powershell.exe -EncodedCommand $EncodedCommand

$OriginalCommand = 'Write-Host "Hey, Atomic!"'
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)
$EncodedCommand =[Convert]::ToBase64String($Bytes)
$EncodedCommand

Set-ItemProperty -Force -Path #{registry_key_storage} -Name #{registry_entry_storage} -Value $EncodedCommand
powershell.exe -Command "IEX ([Text.Encoding]::UNICODE.GetString([Convert]::FromBase64String((gp #{registry_key_storage} #{registry_entry_storage}).#{registry_entry_storage})))"

$OriginalCommand = '#{powershell_command}'
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)
$EncodedCommand =[Convert]::ToBase64String($Bytes)
$EncodedCommand

Set-ItemProperty -Force -Path HKCU:Software\Microsoft\Windows\CurrentVersion -Name #{registry_entry_storage} -Value $EncodedCommand
powershell.exe -Command "IEX ([Text.Encoding]::UNICODE.GetString([Convert]::FromBase64String((gp HKCU:Software\Microsoft\Windows\CurrentVersion #{registry_entry_storage}).#{registry_entry_storage})))"

$OriginalCommand = '#{powershell_command}'
$Bytes = [System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)
$EncodedCommand =[Convert]::ToBase64String($Bytes)
$EncodedCommand

Set-ItemProperty -Force -Path #{registry_key_storage} -Name Debug -Value $EncodedCommand
powershell.exe -Command "IEX ([Text.Encoding]::UNICODE.GetString([Convert]::FromBase64String((gp #{registry_key_storage} Debug).Debug)))"

[a-z0-9]{1}.exe
*.exe \*.exe\:Zone.Identifier:$DATA" 
```

## Commands Dataset

```
[{'command': 'sh -c "echo ZWNobyBIZWxsbyBmcm9tIHRoZSBBdG9taWMgUmVkIFRlYW0= > '
             '/tmp/encoded.dat"\n'
             'cat /tmp/encoded.dat | base64 -d > /tmp/art.sh\n'
             'chmod +x /tmp/art.sh\n'
             '/tmp/art.sh\n',
  'name': None,
  'source': 'atomics/T1027/T1027.yaml'},
 {'command': '$OriginalCommand = \'Write-Host "Hey, Atomic!"\'\n'
             '$Bytes = '
             '[System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)\n'
             '$EncodedCommand =[Convert]::ToBase64String($Bytes)\n'
             '$EncodedCommand\n'
             'powershell.exe -EncodedCommand $EncodedCommand\n',
  'name': None,
  'source': 'atomics/T1027/T1027.yaml'},
 {'command': '$OriginalCommand = \'Write-Host "Hey, Atomic!"\'\n'
             '$Bytes = '
             '[System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)\n'
             '$EncodedCommand =[Convert]::ToBase64String($Bytes)\n'
             '$EncodedCommand\n'
             '\n'
             'Set-ItemProperty -Force -Path #{registry_key_storage} -Name '
             '#{registry_entry_storage} -Value $EncodedCommand\n'
             'powershell.exe -Command "IEX '
             '([Text.Encoding]::UNICODE.GetString([Convert]::FromBase64String((gp '
             '#{registry_key_storage} '
             '#{registry_entry_storage}).#{registry_entry_storage})))"\n',
  'name': None,
  'source': 'atomics/T1027/T1027.yaml'},
 {'command': "$OriginalCommand = '#{powershell_command}'\n"
             '$Bytes = '
             '[System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)\n'
             '$EncodedCommand =[Convert]::ToBase64String($Bytes)\n'
             '$EncodedCommand\n'
             '\n'
             'Set-ItemProperty -Force -Path '
             'HKCU:Software\\Microsoft\\Windows\\CurrentVersion -Name '
             '#{registry_entry_storage} -Value $EncodedCommand\n'
             'powershell.exe -Command "IEX '
             '([Text.Encoding]::UNICODE.GetString([Convert]::FromBase64String((gp '
             'HKCU:Software\\Microsoft\\Windows\\CurrentVersion '
             '#{registry_entry_storage}).#{registry_entry_storage})))"\n',
  'name': None,
  'source': 'atomics/T1027/T1027.yaml'},
 {'command': "$OriginalCommand = '#{powershell_command}'\n"
             '$Bytes = '
             '[System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)\n'
             '$EncodedCommand =[Convert]::ToBase64String($Bytes)\n'
             '$EncodedCommand\n'
             '\n'
             'Set-ItemProperty -Force -Path #{registry_key_storage} -Name '
             'Debug -Value $EncodedCommand\n'
             'powershell.exe -Command "IEX '
             '([Text.Encoding]::UNICODE.GetString([Convert]::FromBase64String((gp '
             '#{registry_key_storage} Debug).Debug)))"\n',
  'name': None,
  'source': 'atomics/T1027/T1027.yaml'},
 {'command': '[a-z0-9]{1}.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '*.exe \\*.exe\\:Zone.Identifier:$DATA" ',
  'name': None,
  'source': 'Threat Hunting Tables'}]
```

## Potential Detections

```json

```

## Potential Queries

```json
[{'name': 'Obfuscated Files Or Information',
  'product': 'Azure Sentinel',
  'query': 'Sysmon| where EventID == 1 and (process_path contains '
           '"certutil.exe" and process_command_line contains "encode")or '
           'process_command_line contains "ToBase64String"'},
 {'name': 'Yml',
  'product': 'https://raw.githubusercontent.com/12306Bro/Threathunting-book/master/{}',
  'query': 'Yml\n'
           'title: Ping Hex IP\n'
           'description: win7 simulation test results\n'
           'references:\n'
           '\xa0\xa0\xa0\xa0- '
           'https://github.com/Neo23x0/sigma/blob/master/rules/windows/process_creation/win_susp_ping_hex_ip.yml\n'
           'status: experimental\n'
           'author: 12306Bro\n'
           'logsource:\n'
           'product: windows\n'
           'service: security\n'
           'detection:\n'
           '\xa0\xa0\xa0\xa0selection:\n'
           '\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0CommandLine:\n'
           "\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0- '* \\ ping.exe "
           "0x *'\n"
           "\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0\xa0- '* \\ ping 0x "
           "*'\n"
           '\xa0\xa0\xa0\xa0condition: selection\n'
           'level: high'}]
```

## Raw Dataset

```json
[{'Atomic Red Team Test - Obfuscated Files or Information': {'atomic_tests': [{'description': 'Creates '
                                                                                              'a '
                                                                                              'base64-encoded '
                                                                                              'data '
                                                                                              'file '
                                                                                              'and '
                                                                                              'decodes '
                                                                                              'it '
                                                                                              'into '
                                                                                              'an '
                                                                                              'executable '
                                                                                              'shell '
                                                                                              'script\n'
                                                                                              '\n'
                                                                                              'Upon '
                                                                                              'successful '
                                                                                              'execution, '
                                                                                              'sh '
                                                                                              'will '
                                                                                              'execute '
                                                                                              'art.sh, '
                                                                                              'which '
                                                                                              'is '
                                                                                              'a '
                                                                                              'base64 '
                                                                                              'encoded '
                                                                                              'command, '
                                                                                              'that '
                                                                                              'stdouts '
                                                                                              '`echo '
                                                                                              'Hello '
                                                                                              'from '
                                                                                              'the '
                                                                                              'Atomic '
                                                                                              'Red '
                                                                                              'Team`.\n',
                                                                               'executor': {'command': 'sh '
                                                                                                       '-c '
                                                                                                       '"echo '
                                                                                                       'ZWNobyBIZWxsbyBmcm9tIHRoZSBBdG9taWMgUmVkIFRlYW0= '
                                                                                                       '> '
                                                                                                       '/tmp/encoded.dat"\n'
                                                                                                       'cat '
                                                                                                       '/tmp/encoded.dat '
                                                                                                       '| '
                                                                                                       'base64 '
                                                                                                       '-d '
                                                                                                       '> '
                                                                                                       '/tmp/art.sh\n'
                                                                                                       'chmod '
                                                                                                       '+x '
                                                                                                       '/tmp/art.sh\n'
                                                                                                       '/tmp/art.sh\n',
                                                                                            'elevation_required': False,
                                                                                            'name': 'sh'},
                                                                               'name': 'Decode '
                                                                                       'base64 '
                                                                                       'Data '
                                                                                       'into '
                                                                                       'Script',
                                                                               'supported_platforms': ['macos',
                                                                                                       'linux']},
                                                                              {'description': 'Creates '
                                                                                              'base64-encoded '
                                                                                              'PowerShell '
                                                                                              'code '
                                                                                              'and '
                                                                                              'executes '
                                                                                              'it. '
                                                                                              'This '
                                                                                              'is '
                                                                                              'used '
                                                                                              'by '
                                                                                              'numerous '
                                                                                              'adversaries '
                                                                                              'and '
                                                                                              'malicious '
                                                                                              'tools.\n'
                                                                                              '\n'
                                                                                              'Upon '
                                                                                              'successful '
                                                                                              'execution, '
                                                                                              'powershell '
                                                                                              'will '
                                                                                              'execute '
                                                                                              'an '
                                                                                              'encoded '
                                                                                              'command '
                                                                                              'and '
                                                                                              'stdout '
                                                                                              'default '
                                                                                              'is '
                                                                                              '"Write-Host '
                                                                                              '"Hey, '
                                                                                              'Atomic!"\n',
                                                                               'executor': {'command': '$OriginalCommand '
                                                                                                       '= '
                                                                                                       "'#{powershell_command}'\n"
                                                                                                       '$Bytes '
                                                                                                       '= '
                                                                                                       '[System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)\n'
                                                                                                       '$EncodedCommand '
                                                                                                       '=[Convert]::ToBase64String($Bytes)\n'
                                                                                                       '$EncodedCommand\n'
                                                                                                       'powershell.exe '
                                                                                                       '-EncodedCommand '
                                                                                                       '$EncodedCommand\n',
                                                                                            'elevation_required': False,
                                                                                            'name': 'powershell'},
                                                                               'input_arguments': {'powershell_command': {'default': 'Write-Host '
                                                                                                                                     '"Hey, '
                                                                                                                                     'Atomic!"',
                                                                                                                          'description': 'PowerShell '
                                                                                                                                         'command '
                                                                                                                                         'to '
                                                                                                                                         'encode',
                                                                                                                          'type': 'String'}},
                                                                               'name': 'Execute '
                                                                                       'base64-encoded '
                                                                                       'PowerShell',
                                                                               'supported_platforms': ['windows']},
                                                                              {'description': 'Stores '
                                                                                              'base64-encoded '
                                                                                              'PowerShell '
                                                                                              'code '
                                                                                              'in '
                                                                                              'the '
                                                                                              'Windows '
                                                                                              'Registry '
                                                                                              'and '
                                                                                              'deobfuscates '
                                                                                              'it '
                                                                                              'for '
                                                                                              'execution. '
                                                                                              'This '
                                                                                              'is '
                                                                                              'used '
                                                                                              'by '
                                                                                              'numerous '
                                                                                              'adversaries '
                                                                                              'and '
                                                                                              'malicious '
                                                                                              'tools.\n'
                                                                                              '\n'
                                                                                              'Upon '
                                                                                              'successful '
                                                                                              'execution, '
                                                                                              'powershell '
                                                                                              'will '
                                                                                              'execute '
                                                                                              'encoded '
                                                                                              'command '
                                                                                              'and '
                                                                                              'read/write '
                                                                                              'from '
                                                                                              'the '
                                                                                              'registry.\n',
                                                                               'executor': {'cleanup_command': 'Remove-ItemProperty '
                                                                                                               '-Force '
                                                                                                               '-ErrorAction '
                                                                                                               'Ignore '
                                                                                                               '-Path '
                                                                                                               '#{registry_key_storage} '
                                                                                                               '-Name '
                                                                                                               '#{registry_entry_storage}\n',
                                                                                            'command': '$OriginalCommand '
                                                                                                       '= '
                                                                                                       "'#{powershell_command}'\n"
                                                                                                       '$Bytes '
                                                                                                       '= '
                                                                                                       '[System.Text.Encoding]::Unicode.GetBytes($OriginalCommand)\n'
                                                                                                       '$EncodedCommand '
                                                                                                       '=[Convert]::ToBase64String($Bytes)\n'
                                                                                                       '$EncodedCommand\n'
                                                                                                       '\n'
                                                                                                       'Set-ItemProperty '
                                                                                                       '-Force '
                                                                                                       '-Path '
                                                                                                       '#{registry_key_storage} '
                                                                                                       '-Name '
                                                                                                       '#{registry_entry_storage} '
                                                                                                       '-Value '
                                                                                                       '$EncodedCommand\n'
                                                                                                       'powershell.exe '
                                                                                                       '-Command '
                                                                                                       '"IEX '
                                                                                                       '([Text.Encoding]::UNICODE.GetString([Convert]::FromBase64String((gp '
                                                                                                       '#{registry_key_storage} '
                                                                                                       '#{registry_entry_storage}).#{registry_entry_storage})))"\n',
                                                                                            'elevation_required': False,
                                                                                            'name': 'powershell'},
                                                                               'input_arguments': {'powershell_command': {'default': 'Write-Host '
                                                                                                                                     '"Hey, '
                                                                                                                                     'Atomic!"',
                                                                                                                          'description': 'PowerShell '
                                                                                                                                         'command '
                                                                                                                                         'to '
                                                                                                                                         'encode',
                                                                                                                          'type': 'String'},
                                                                                                   'registry_entry_storage': {'default': 'Debug',
                                                                                                                              'description': 'Windows '
                                                                                                                                             'Registry '
                                                                                                                                             'entry '
                                                                                                                                             'to '
                                                                                                                                             'store '
                                                                                                                                             'code '
                                                                                                                                             'under '
                                                                                                                                             'key',
                                                                                                                              'type': 'String'},
                                                                                                   'registry_key_storage': {'default': 'HKCU:Software\\Microsoft\\Windows\\CurrentVersion',
                                                                                                                            'description': 'Windows '
                                                                                                                                           'Registry '
                                                                                                                                           'Key '
                                                                                                                                           'to '
                                                                                                                                           'store '
                                                                                                                                           'code',
                                                                                                                            'type': 'String'}},
                                                                               'name': 'Execute '
                                                                                       'base64-encoded '
                                                                                       'PowerShell '
                                                                                       'from '
                                                                                       'Windows '
                                                                                       'Registry',
                                                                               'supported_platforms': ['windows']}],
                                                             'attack_technique': 'T1027',
                                                             'display_name': 'Obfuscated '
                                                                             'Files '
                                                                             'or '
                                                                             'Information'}},
 {'Threat Hunting Tables': {'chain_id': '100001',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'rare',
                            'itw_sample': '3d77bf4f5d40aa7fff1c59058bf89e0349fa14e3260bbc290b836cbb1e1a17b7',
                            'loaded_dll': '',
                            'mitre_attack': 'T1027',
                            'mitre_caption': 'obfuscation',
                            'os': 'windows',
                            'parent_process': '[a-z0-9]{1}.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '',
                            'sub_process_2': ''}},
 {'Threat Hunting Tables': {'chain_id': '100123',
                            'commandline_string': '\\*.exe\\:Zone.Identifier:$DATA" ',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': 'b3c4ae251f8094fa15b510051835c657eaef2a6cea46075d3aec964b14a99f68',
                            'loaded_dll': '',
                            'mitre_attack': 'T1027',
                            'mitre_caption': 'alternate_data_stream',
                            'os': 'windows',
                            'parent_process': '*.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '',
                            'sub_process_2': ''}}]
```

# Tactics


* [Defense Evasion](../tactics/Defense-Evasion.md)


# Mitigations

None

# Actors


* [FIN8](../actors/FIN8.md)

* [BlackOasis](../actors/BlackOasis.md)
    
* [Dust Storm](../actors/Dust-Storm.md)
    
* [menuPass](../actors/menuPass.md)
    
* [Patchwork](../actors/Patchwork.md)
    
* [Elderwood](../actors/Elderwood.md)
    
* [Leafminer](../actors/Leafminer.md)
    
* [Leviathan](../actors/Leviathan.md)
    
* [APT18](../actors/APT18.md)
    
* [Cobalt Group](../actors/Cobalt-Group.md)
    
* [APT32](../actors/APT32.md)
    
* [APT37](../actors/APT37.md)
    
* [Lazarus Group](../actors/Lazarus-Group.md)
    
* [Threat Group-3390](../actors/Threat-Group-3390.md)
    
* [Group5](../actors/Group5.md)
    
* [Magic Hound](../actors/Magic-Hound.md)
    
* [Honeybee](../actors/Honeybee.md)
    
* [MuddyWater](../actors/MuddyWater.md)
    
* [Darkhotel](../actors/Darkhotel.md)
    
* [OilRig](../actors/OilRig.md)
    
* [APT3](../actors/APT3.md)
    
* [APT28](../actors/APT28.md)
    
* [Gallmaker](../actors/Gallmaker.md)
    
* [Tropic Trooper](../actors/Tropic-Trooper.md)
    
* [APT29](../actors/APT29.md)
    
* [Putter Panda](../actors/Putter-Panda.md)
    
* [Night Dragon](../actors/Night-Dragon.md)
    
* [Dark Caracal](../actors/Dark-Caracal.md)
    
* [FIN7](../actors/FIN7.md)
    
* [APT19](../actors/APT19.md)
    
* [APT33](../actors/APT33.md)
    
* [Silence](../actors/Silence.md)
    
* [TA505](../actors/TA505.md)
    
* [Turla](../actors/Turla.md)
    
* [Soft Cell](../actors/Soft-Cell.md)
    
* [Machete](../actors/Machete.md)
    
