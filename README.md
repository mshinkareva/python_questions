# python_questions

Итератор в Python — объект, реализующий метод __next__, который возвращает следующий элемент последовательности или выбрасывает исключение StopIteration, если не осталось элементов.




__iter__ 


Генератор — это функция, которая умеет возвращать несколько значений по очереди, не храня в памяти весь набор значений. 



Процессы
Процесс — это то, что обычно называют запущенной программой на компьютере. Для запуска процесса операционная система выделяет область памяти.



В Python процессы применяют для распараллеливания тяжёлых вычислительных операций — вычисление хэшей, работа с матрицами, обработка изображений и подобными операциями. Именно в Python использование потоков для такого рода операций только усугубит производительность.


Одна из проблем, которую решает GIL, связана с тем, что в многопоточном приложении одновременно несколько потоков могут изменять значение счётчика ссылок. Это может привести к тому, что память очистится неправильно и удалится тот объект, на который ещё существует ссылка.



Но добавление блокировки к нескольким объектам может привести к появлению другой проблемы — взаимоблокировки или deadlocks, которая получается, если блокировка есть более чем на одном объекте. К тому же эта проблема тоже снижала бы производительность из-за многократной установки блокировки.


Состояние гонки — это ошибка проектирования многопоточного приложения, при которой его работа зависит от того, в каком порядке выполняются части кода. Это может произойти при работе с общими объектами между потоками, несмотря на то что GIL позволяет работать только одному потоку в один момент времени.
Рассмотрим простой пример обновления счётчика в нескольких потоках.


Файл-дескриптор — это уникальный идентификатор открытого файла в операционной системе.


Что нужно запомнить про процессы и потоки
Достоинства процессов в Python:
У каждого процесса своя память.
Позволяют использовать все доступные ядра процессора.
GIL не накладывает ограничения.
Есть возможность прервать процесс.
Подходит для тяжёлых вычислений.
Недостатки процессов в Python:
IPC более сложный и имеет большие накладные расходы.
Большое потребление памяти.
Достоинства потоков в Python:
Более легковесные и требуют меньше памяти.
Общая память между потоками.
Можно запускать в потоках для параллельной работы модули, написанные на C, которые отпускают GIL.
Подходят для операций ввода/вывода.
Недостатки потоков в Python:
GIL не позволяет потокам работать одновременно кроме C модулей, которые отпускают GIL.
Нет возможности прервать выполнение потока.
Необходимо использовать примитивы синхронизации для работы с общей памятью, чтобы предотвратить «гонку».