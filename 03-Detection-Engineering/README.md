# Detection Engineering (Blue Team)

В этом разделе описано, как Wazuh детектирует активность, и какие правила были написаны.

## Сбор логов
- На Windows Server и Win10 установлены агенты Wazuh.
- В `ossec.conf` добавлены локации для журналов Security и Sysmon.

## Написанные правила
- **DCSync (Event ID 4662):** Правило `100200`.
- **Pass-the-Hash (Event ID 4624, Type 3):** Правило `100201`.
- **Kerberoasting (Event ID 4769, RC4):** Правило `100210`.
- **Apollo C2 (Sysmon Event ID 1):** Правило `100400` (по `OriginalFileName`).
