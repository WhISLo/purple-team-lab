# Инцидент 002: Обход SRP и выполнение Shellcode в памяти (InstallUtil)

**Дата:** 2026-10-22
**Агент:** Win10 (10.10.10.201)
**Цель:** Обойти политику SRP и запустить C2-агент, не оставляя исполняемых файлов на диске.

## Executive Summary
Атакующий использовал технику LOLBins (InstallUtil.exe) для обхода Software Restriction Policies (SRP). Вместо запуска вредоносного .exe файла, был скомпилирован кастомный C# загрузчик (loader.dll), который через InstallUtil загрузил шелл-код Apollo напрямую в оперативную память. Встроенное правило Wazuh (100400) не сработало, так как оно было завязано на имя процесса apollo.exe, которого на диске не было.

## Attack Chain (Red Team)
1. Создан payload `apollo.bin` (Shellcode) в Mythic.
2. Написан C# загрузчик (`loader.cs`), скачивающий и исполняющий шелл-код в памяти.
3. Загрузчик скомпилирован утилитой `csc.exe` в `loader.dll`.
4. Выполнен запуск: `InstallUtil.exe /U C:\Windows\Tasks\loader.dll`.
5. Загрузчик скачал `apollo.bin` с Kali и внедрил в память процесса InstallUtil.

## Detection Failure (Blue Team)
- **Почему SRP не сработал:** `InstallUtil.exe` — доверенный бинарник Microsoft из `C:\Windows\`, политика SRP разрешает его запуск.
- **Почему Defender не сработал:** Защита в реальном времени была временно отключена для лабораторных тестов.
- **Почему Wazuh не сработал:** Sysmon видел запуск `InstallUtil.exe`, но не видел `apollo.exe`, так как вредоносный код исполнялся в памяти (инжект).

## MITRE ATT&CK
- **T1218.004:** System Binary Proxy Execution: InstallUtil
- **T1055:** Process Injection
- **T1071:** Application Layer Protocol

## Recommendations (Actionable)
1. Запретить запуск `InstallUtil.exe` для обычных пользователей через AppLocker/SRP.
2. Включить и настроить Sysmon Event ID 8 (CreateRemoteThread) и Event ID 10 (ProcessAccess) для детекции инжектов в память.
3. Написать кастомные правила Wazuh на аномальную сетевую активность от `InstallUtil.exe`.