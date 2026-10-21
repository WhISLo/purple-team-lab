# Доступ к учетным данным (Credential Access)

## Active Directory атаки

### 1. Kerberoasting
- **Инструмент:** `GetUserSPNs.py` (Impacket).
- **Цель:** Учетная запись `svc_sql` с SPN.
- **Результат:** Получен хеш TGS (`$krb5tgs$...`).

### 2. AS-REP Roasting
- **Инструмент:** `GetNPUsers.py`.
- **Цель:** Пользователь `asrep_user`.
- **Результат:** Получен хеш AS-REP (`$krb5asrep$...`), пароль подобран по словарю.

### 3. DCSync
- **Инструмент:** Mimikatz (в процессе настройки).
- **Цель:** Извлечение хешей из NTDS.dit.

**MITRE ATT&CK:** T1558.003, T1558.004, T1003.006.
