
# Automated Collection

## Description

### MITRE Description

> Once established within a system or network, an adversary may use automated techniques for collecting internal data. Methods for performing this technique could include use of [Scripting](https://attack.mitre.org/techniques/T1064) to search for and copy information fitting set criteria such as file type, location, or name at specific time intervals. This functionality could also be built into remote access tools. 

This technique may incorporate use of other techniques such as [File and Directory Discovery](https://attack.mitre.org/techniques/T1083) and [Remote File Copy](https://attack.mitre.org/techniques/T1105) to identify and move files.

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: intentionally left blank
* Permissions: ['User']
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: intentionally left blank
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1119

## Potential Commands

```
mkdir %temp%\T1119_command_prompt_collection >nul 2>&1
dir c: /b /s .docx | findstr /e .docx
for /R c: %f in (*.docx) do copy %f %temp%\T1119_command_prompt_collection

New-Item -Path $env:TEMP\T1119_powershell_collection -ItemType Directory -Force | Out-Null
Get-ChildItem -Recurse -Include *.doc | % {Copy-Item $_.FullName -destination $env:TEMP\T1119_powershell_collection}

Get-Service > $env:TEMP\T1119_1.txt
Get-ChildItem Env: > $env:TEMP\T1119_2.txt
Get-Process > $env:TEMP\T1119_3.txt

sc query type=service > %TEMP%\T1119_1.txt
doskey /history > %TEMP%\T1119_2.txt
wmic process list > %TEMP%\T1119_3.txt
tree C:\AtomicRedTeam\atomics > %TEMP%\T1119_4.txt

cmd.exe dir c: /b /s .docx | findstr /e .docx
```

## Commands Dataset

```
[{'command': 'mkdir %temp%\\T1119_command_prompt_collection >nul 2>&1\n'
             'dir c: /b /s .docx | findstr /e .docx\n'
             'for /R c: %f in (*.docx) do copy %f '
             '%temp%\\T1119_command_prompt_collection\n',
  'name': None,
  'source': 'atomics/T1119/T1119.yaml'},
 {'command': 'New-Item -Path $env:TEMP\\T1119_powershell_collection -ItemType '
             'Directory -Force | Out-Null\n'
             'Get-ChildItem -Recurse -Include *.doc | % {Copy-Item $_.FullName '
             '-destination $env:TEMP\\T1119_powershell_collection}\n',
  'name': None,
  'source': 'atomics/T1119/T1119.yaml'},
 {'command': 'Get-Service > $env:TEMP\\T1119_1.txt\n'
             'Get-ChildItem Env: > $env:TEMP\\T1119_2.txt\n'
             'Get-Process > $env:TEMP\\T1119_3.txt\n',
  'name': None,
  'source': 'atomics/T1119/T1119.yaml'},
 {'command': 'sc query type=service > %TEMP%\\T1119_1.txt\n'
             'doskey /history > %TEMP%\\T1119_2.txt\n'
             'wmic process list > %TEMP%\\T1119_3.txt\n'
             'tree C:\\AtomicRedTeam\\atomics > %TEMP%\\T1119_4.txt\n',
  'name': None,
  'source': 'atomics/T1119/T1119.yaml'},
 {'command': 'cmd.exe dir c: /b /s .docx | findstr /e .docx',
  'name': None,
  'source': 'Threat Hunting Tables'}]
```

## Potential Detections

```json

```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - Automated Collection': {'atomic_tests': [{'description': 'Automated '
                                                                                   'Collection. '
                                                                                   'Upon '
                                                                                   'execution, '
                                                                                   'check '
                                                                                   'the '
                                                                                   'users '
                                                                                   'temp '
                                                                                   'directory '
                                                                                   '(%temp%) '
                                                                                   'for '
                                                                                   'the '
                                                                                   'folder '
                                                                                   'T1119_command_prompt_collection\n'
                                                                                   'to '
                                                                                   'see '
                                                                                   'what '
                                                                                   'was '
                                                                                   'collected.\n',
                                                                    'executor': {'cleanup_command': 'del '
                                                                                                    '%temp%\\T1119_command_prompt_collection '
                                                                                                    '/F '
                                                                                                    '/Q '
                                                                                                    '>null '
                                                                                                    '2>&1\n',
                                                                                 'command': 'mkdir '
                                                                                            '%temp%\\T1119_command_prompt_collection '
                                                                                            '>nul '
                                                                                            '2>&1\n'
                                                                                            'dir '
                                                                                            'c: '
                                                                                            '/b '
                                                                                            '/s '
                                                                                            '.docx '
                                                                                            '| '
                                                                                            'findstr '
                                                                                            '/e '
                                                                                            '.docx\n'
                                                                                            'for '
                                                                                            '/R '
                                                                                            'c: '
                                                                                            '%f '
                                                                                            'in '
                                                                                            '(*.docx) '
                                                                                            'do '
                                                                                            'copy '
                                                                                            '%f '
                                                                                            '%temp%\\T1119_command_prompt_collection\n',
                                                                                 'name': 'command_prompt'},
                                                                    'name': 'Automated '
                                                                            'Collection '
                                                                            'Command '
                                                                            'Prompt',
                                                                    'supported_platforms': ['windows']},
                                                                   {'description': 'Automated '
                                                                                   'Collection. '
                                                                                   'Upon '
                                                                                   'execution, '
                                                                                   'check '
                                                                                   'the '
                                                                                   'users '
                                                                                   'temp '
                                                                                   'directory '
                                                                                   '(%temp%) '
                                                                                   'for '
                                                                                   'the '
                                                                                   'folder '
                                                                                   'T1119_powershell_collection\n'
                                                                                   'to '
                                                                                   'see '
                                                                                   'what '
                                                                                   'was '
                                                                                   'collected.\n',
                                                                    'executor': {'cleanup_command': 'Remove-Item '
                                                                                                    '$env:TEMP\\T1119_powershell_collection '
                                                                                                    '-Force '
                                                                                                    '| '
                                                                                                    'Out-Null\n',
                                                                                 'command': 'New-Item '
                                                                                            '-Path '
                                                                                            '$env:TEMP\\T1119_powershell_collection '
                                                                                            '-ItemType '
                                                                                            'Directory '
                                                                                            '-Force '
                                                                                            '| '
                                                                                            'Out-Null\n'
                                                                                            'Get-ChildItem '
                                                                                            '-Recurse '
                                                                                            '-Include '
                                                                                            '*.doc '
                                                                                            '| '
                                                                                            '% '
                                                                                            '{Copy-Item '
                                                                                            '$_.FullName '
                                                                                            '-destination '
                                                                                            '$env:TEMP\\T1119_powershell_collection}\n',
                                                                                 'elevation_required': False,
                                                                                 'name': 'powershell'},
                                                                    'name': 'Automated '
                                                                            'Collection '
                                                                            'PowerShell',
                                                                    'supported_platforms': ['windows']},
                                                                   {'description': 'collect '
                                                                                   'information '
                                                                                   'for '
                                                                                   'exfiltration. '
                                                                                   'Upon '
                                                                                   'execution, '
                                                                                   'check '
                                                                                   'the '
                                                                                   'users '
                                                                                   'temp '
                                                                                   'directory '
                                                                                   '(%temp%) '
                                                                                   'for '
                                                                                   'files '
                                                                                   'T1119_*.txt\n'
                                                                                   'to '
                                                                                   'see '
                                                                                   'what '
                                                                                   'was '
                                                                                   'collected.\n',
                                                                    'executor': {'cleanup_command': 'Remove-Item '
                                                                                                    '$env:TEMP\\T1119_1.txt '
                                                                                                    '-ErrorAction '
                                                                                                    'Ignore\n'
                                                                                                    'Remove-Item '
                                                                                                    '$env:TEMP\\T1119_2.txt '
                                                                                                    '-ErrorAction '
                                                                                                    'Ignore\n'
                                                                                                    'Remove-Item '
                                                                                                    '$env:TEMP\\T1119_3.txt '
                                                                                                    '-ErrorAction '
                                                                                                    'Ignore\n',
                                                                                 'command': 'Get-Service '
                                                                                            '> '
                                                                                            '$env:TEMP\\T1119_1.txt\n'
                                                                                            'Get-ChildItem '
                                                                                            'Env: '
                                                                                            '> '
                                                                                            '$env:TEMP\\T1119_2.txt\n'
                                                                                            'Get-Process '
                                                                                            '> '
                                                                                            '$env:TEMP\\T1119_3.txt\n',
                                                                                 'elevation_required': False,
                                                                                 'name': 'powershell'},
                                                                    'name': 'Recon '
                                                                            'information '
                                                                            'for '
                                                                            'export '
                                                                            'with '
                                                                            'PowerShell',
                                                                    'supported_platforms': ['windows']},
                                                                   {'description': 'collect '
                                                                                   'information '
                                                                                   'for '
                                                                                   'exfiltration. '
                                                                                   'Upon '
                                                                                   'execution, '
                                                                                   'check '
                                                                                   'the '
                                                                                   'users '
                                                                                   'temp '
                                                                                   'directory '
                                                                                   '(%temp%) '
                                                                                   'for '
                                                                                   'files '
                                                                                   'T1119_*.txt\n'
                                                                                   'to '
                                                                                   'see '
                                                                                   'what '
                                                                                   'was '
                                                                                   'collected.\n',
                                                                    'executor': {'cleanup_command': 'del '
                                                                                                    '%TEMP%\\T1119_1.txt '
                                                                                                    '>nul '
                                                                                                    '2>&1\n'
                                                                                                    'del '
                                                                                                    '%TEMP%\\T1119_2.txt '
                                                                                                    '>nul '
                                                                                                    '2>&1\n'
                                                                                                    'del '
                                                                                                    '%TEMP%\\T1119_3.txt '
                                                                                                    '>nul '
                                                                                                    '2>&1\n'
                                                                                                    'del '
                                                                                                    '%TEMP%\\T1119_4.txt '
                                                                                                    '>nul '
                                                                                                    '2>&1\n',
                                                                                 'command': 'sc '
                                                                                            'query '
                                                                                            'type=service '
                                                                                            '> '
                                                                                            '%TEMP%\\T1119_1.txt\n'
                                                                                            'doskey '
                                                                                            '/history '
                                                                                            '> '
                                                                                            '%TEMP%\\T1119_2.txt\n'
                                                                                            'wmic '
                                                                                            'process '
                                                                                            'list '
                                                                                            '> '
                                                                                            '%TEMP%\\T1119_3.txt\n'
                                                                                            'tree '
                                                                                            'C:\\AtomicRedTeam\\atomics '
                                                                                            '> '
                                                                                            '%TEMP%\\T1119_4.txt\n',
                                                                                 'elevation_required': False,
                                                                                 'name': 'command_prompt'},
                                                                    'name': 'Recon '
                                                                            'information '
                                                                            'for '
                                                                            'export '
                                                                            'with '
                                                                            'Command '
                                                                            'Prompt',
                                                                    'supported_platforms': ['windows']}],
                                                  'attack_technique': 'T1119',
                                                  'display_name': 'Automated '
                                                                  'Collection'}},
 {'Threat Hunting Tables': {'chain_id': '100127',
                            'commandline_string': 'dir c: /b /s .docx | '
                                                  'findstr /e .docx',
                            'file_path': '',
                            'file_value': '',
                            'frequency': 'low',
                            'itw_sample': '',
                            'loaded_dll': '',
                            'mitre_attack': 'T1119',
                            'mitre_caption': 'data_collection',
                            'os': 'windows',
                            'parent_process': 'cmd.exe',
                            'registry_path': '',
                            'registry_value': '',
                            'sub_process_1': '',
                            'sub_process_2': ''}}]
```

# Tactics


* [Collection](../tactics/Collection.md)


# Mitigations

None

# Actors


* [OilRig](../actors/OilRig.md)

* [FIN6](../actors/FIN6.md)
    
* [APT28](../actors/APT28.md)
    
* [Patchwork](../actors/Patchwork.md)
    
* [Threat Group-3390](../actors/Threat-Group-3390.md)
    
* [APT1](../actors/APT1.md)
    
* [FIN5](../actors/FIN5.md)
    
