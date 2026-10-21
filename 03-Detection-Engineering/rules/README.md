# Правила Wazuh

## Список правил
1. **100200** — DCSync (4662, `Replicating Directory Changes`).
2. **100201** — Pass-the-Hash (4624, Logon Type 3 + NTLM).
3. **100210** — Kerberoasting (4769, RC4).
4. **100400** — Apollo C2 (Sysmon Event ID 1, `OriginalFileName: Apollo.exe`).

### Пример правила (DCSync)
```xml
<rule id="100200" level="12">
  <if_sid>60106</if_sid>
  <field name="win.system.eventID">^4662$</field>
  <field name="win.eventdata.properties">Replicating Directory Changes</field>
  <description>Possible DCSync attack</description>
  <mitre>
    <id>T1003.006</id>
  </mitre>
</rule>
```
