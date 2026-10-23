Executive Summary: обход SRP через InstallUtil с последующим запуском C2 в памяти
Attack Chain (Red Team): (загрузка shellcode -> компиляция загрузчика -> запуск через InstallUtil
Detection Failure (Blue Team): Как итог Sysmon не увидел угрозу, так как видел только легитMITRE ATT&CK:

T1218.004 (System Binary Proxy Execution: InstallUtil)

T1055 (Process Injection)

T1071 (Application Layer Protocol)

Recommendations: Пишем новое правило Wazuh
Нам нужно научить Wazuh ловить эту атаку. Поскольку InstallUtil.exe — легитимный процесс, мы будем ловить его подозрительное поведение.

Правило 1 (Сеть): InstallUtil.exe, который лезет в интернет (порт 80/443) или к нашему Kali (10.10.10.203).

Правило 2 (Дочерний процесс): Если InstallUtil.exe запускает powershell.exe или cmd.exe — это красный флаг (обычно он так не делает).
