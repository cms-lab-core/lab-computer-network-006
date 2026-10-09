# Лабораторная 006 · IPv4: адрес, сеть и префикс

Разделяет решение IPv4/FIB о пути и доставку Ethernet/ARP из лабораторных 003–005.

**Практический маршрут:** `ipaddress` → direct `/24` на `pc1↔pc2` → живой ARP/ICMP PCAP → менять только `pc1 /24→/25` → наблюдать отличие `ip route get` на двух хостах и захватить асимметричный обмен → вернуть `/24` → двунаправленный ping и CHECK → отдельная задача VLSM.

Для контролируемой поломки **не нужен доступ к management**: `eth0` не трогаем. В C9s `ip route get` после изменения префикса может выбрать management default через `eth0` (либо стать unreachable); это означает отсутствие direct route по `eth1`, а не исправный lab gateway.

Два настоящих capture:
- `captures/prefix-24-working.pcap` — после настройки /24, запуск ping с pc1;
- `captures/prefix-25-asymmetric.pcap` — после изменения **только pc1**, ping с pc2.

`PcapViewer` выводит настоящие кадры в notebook, включая статический рендер. Все 6 вопросов имеют строго отдельный Markdown ответ `введите ваш ответ` и следующий REVIEW-ONLY AI prompt.

**VLSM:** разбить `192.168.60.0/24` под 70, 35 и 14 устройств. Фиксируем network, broadcast, usable range, отсутствие пересечений; повторно не перенастраиваем стенд. Иллюстрации существуют в `task/assets/prefix.svg` и `task/assets/vlsm.svg`.

CHECK смотрит актуальные IPv4 на `eth1`, connected и direct routes, ICMP в оба направления. Историю отказа или ответы студента он не оценивает.
