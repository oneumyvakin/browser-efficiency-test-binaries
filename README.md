# Тестирование энергоэффективности браузеров

## Методология

[Методология измерения энергопотребления](METHODOLOGY.md)

## Выполнение теста

1. В схеме электропитания Windows, в дополнительных настройках, отключить "Уведомление о низком заряде батареи"("Low battery notification")
1. Установить в систему сертификат `WebPageReplay\ca.crt` в хранилище "Доверенные корневые центры сертификации"("Trusted Root Certification Authorities")
1. Добавить в файл `C:\Windows\System32\drivers\etc\hosts` содержимое файла `WebPageReplay\hosts`
1. Проверить что в системе свободны TCP порты 80, 443, 8080-8090.
1. Открыть CMD.
1. Установить переменные окружения, которые определят путь до исполняемого файла браузера, например:
```
set OPERA_PATH=C:\Program Files (x86)\Opera\launcher.exe
set YB_PATH=C:\Users\%USERNAME%\AppData\Local\Yandex\YandexBrowser\Application\browser.exe
set CHROME_PATH=C:\Program Files (x86)\Google\Chrome\Application\chrome.exe
```

4. Отключить все переферийные устройства от ноутбука: мыши, флешки и другие.
1. Уменьшить яркость матрицы до минимума.
1. Отключить ноутбук от питания

1. Запустить тест:
   1. Чтобы запустить тест Яндекс.Браузер без режима энергосбережения:
`BrowserEfficiencyTest.exe -b yabro -infinite-loop -i 1 -w benchmark_v3_8 -rp .\Results\benchmark_v3_8_yandex_default -broargs "--disable-features=energy-saving --force-fieldtrials=crp/0`

   1. Чтобы запустить тест Яндекс.Браузер в режиме энергосбережения:
`BrowserEfficiencyTest.exe -b yabro -infinite-loop -i 1 -w benchmark_v3_8 -rp .\Results\benchmark_v3_8_yandex_energy_saving -broargs "--enable-features=energy-saving<x,force-energy-saving --force-fieldtrials=crp/0/x/1  --force-fieldtrial-params=x.1:screen_refresh_rate/30/ui_refresh_rate/30/fps_progress_reduce_to/2/loading_progress/true/subresource_filter/false/block_animated_frames/false/active_to_background_tab_time_in_min/1/wake_ups_per_second/0.0/wake_up_duration_ms/0/cpu_budget/0.00/max_budget/300/max_delay/0/initial_budget/0.0/min_budget_level_to_run_sec/0"`

   1. Чтобы запустить тест Chrome: `BrowserEfficiencyTest.exe -b chrome -infinite-loop -i 1 -w benchmark_v3_8 -rp .\Results\benchmark_v3_8_chrome`

   1. Чтобы запустить тест Opera: `BrowserEfficiencyTest.exe -b opera -infinite-loop -i 1 -w benchmark_v3_8 -rp .\Results\benchmark_v3_8_opera`

   1. Чтобы запустить тест Firefox: `BrowserEfficiencyTest.exe -b firefox -infinite-loop -i 1 -w benchmark_v3_8 -rp .\Results\benchmark_v3_8_firefox`

   1. Чтобы запустить тест MS Edge: `BrowserEfficiencyTest.exe -b edge -infinite-loop -i 1 -w benchmark_v3_8 -rp .\Results\benchmark_v3_8_edge`
   
1. Тест идет до полной разрядки батареи и полного выключения ноутбука
1. После разрядки батареи, включить ноутбук
1. Лог времени работы теста будет в файле `.\Results\benchmark_v3_8_<browser>\heartbeat.log`
