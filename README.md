# Antimalware Engine

Экспериментальный Rust-движок для triage файлов. Библиотека собирает объяснимый score от 0 до 100 из независимых findings: энтропия, базовый статический анализ, эвристические признаки и YARA. Это не доказательство безопасности и не замена sandbox/антивирусу.

## Вердикты

`0–14` safe, `15–39` suspicious, `40–69` likely malicious, `70–100` malicious.

## Запуск

```bash
cargo run --release --bin antimalware -- ./sample.bin
cargo run --release --bin antimalware -- ./sample.bin --yara ./rules/reversinglabs --json
cargo run --release --bin antimalware -- ./sample.bin --yara ./rules/bartblaze --json
```

Новые наборы можно передавать каталогом: движок рекурсивно собирает все `.yar`/`.yara`. ReversingLabs подключён как detection-набор. BartBlaze также поддерживается, но generic/hacktools/PUA-совпадения получают меньший вес. Старый `no-public/rules` по умолчанию не используется: это отдельный архив с устаревшими правилами и несовместимыми с YARA-X конструкциями. Безопасные fixtures находятся в `samples/`.

Архитектура намеренно разделена: `antimalware-engine` можно встроить в daemon, REST-сервис или GUI, а CLI остаётся тонкой оболочкой. Следующие естественные шаги — ограничение размера/времени сканирования, парсеры PE/ELF, allowlist и тестовый корпус с калибровкой весов.
