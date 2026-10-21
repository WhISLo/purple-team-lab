# Выполнение (Execution)

## Запуск C2-агента Apollo (Mythic)

**Цель:** Получить удаленный доступ к Windows 10.

### Шаги:
1. В Mythic создан payload (Windows, Apollo, HTTP `10.10.10.20:80`).
2. Payload скачан в виде `.exe`.
3. Файл передан на Win10 через HTTP-сервер на Kali (`python3 -m http.server 8000`).
4. Windows Defender блокировал загрузку — добавлены исключения.
5. Запуск `apollo.exe` из `C:\Users\Public\`.
6. В Mythic появился callback.

### Выполненные команды:
- `shell whoami`
- `shell ipconfig`
- `shell dir C:\Users`

**MITRE ATT&CK:** T1071, T1059.
