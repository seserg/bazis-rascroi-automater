### Модуль для автоматизации работы с Базис-Раскрой 8

---

*Скрипт разработан для интеграции программы приёма заказа распила с программой по формированию раскроя плит.*

---
Для того чтобы сделать карту кроя в Базис-Раскрое 8 необходиммо ввести размеры и количество (спецификацию) в самом Базисе. Данную спецификацию можно сохранить в текстовом виде в файле с раширением *.bpl. Список обрезков которые можно использовать хранятся в файле SkladObrezkov.dat, в текстовом виде(название материала должно 100% совпадать с названием в списке обпезков для того чтобы быть использован). При просчёте карт кроя Базис записывает информацию по рассположению деталей на листах и новых обрезков в файл PartnerSoft.dat. Там не много информации, но её достаточно для сохранения некоторых данных в цифровом виде.




Скрипт используется следующим образом:

1. Создаём объект BazisLink с необходимой конфигурацией.
2. Запускаем метод run передавая ему объект с наименованием файла и текстом файла *.bpl в base64 кодировке.
3. Опционльно можно выполнить метод watchFile передав ему в параметр колбэк для выполнения когда произойдут изменения в файле карт.
4. метод parse разбирает файл карт и создаёт объект с представлением данных карт кроя.
5. также есть метод end который закрывает базис и отключает слежение за файлом карт кроя.


```javascript
const Rascroi = require("./index");
let ras = new Rascroi(cfg);
ras.init();

ras.run(file);
ras.watchFile(saveDataOnEveryMapSave);
let maps = ras.parse();

ras.end();
```

