# ParallelComputingLab2
 
## Отчёт по лабораторной работе №2   

по дисциплине "Параллельные вычисления"   
студента группы ПА-18-2   
Рябова Андрея Дмитриевича   

### Постановка задачи:   

Инструкции:
1. Установить MPICH
2. Выучить правила вызова программы mpiexec
3. Скомпилировать программу с разным количеством процессов на одном компьютере
4. Описать процесс установки программного обеспечения

### Выполнение:   

#### 1. Установка MPICH

Будем работать с этой утилитой на Visual Studio 2019. Вот сама ссылка на VS2019 - [link](https://visualstudio.microsoft.com/ru/downloads/?rr=%20https%3A%2F%2Fdocs.microsoft.com%2Fruru%2Fvisualstudio%2Fide%2F%20whats-new-visual-studio-2019%3Fview%3Dvs-2019).

Теперь с [сайта](https://www.microsoft.com/en-us/download/details.aspx?id=100593) этой утилиты скачаем два файла:
* msmpisetup.exe
* msmpisdk.msi

И установим их. После этого проверим наличие установленных утилит в cmd при помощи данной команды `set MSMPI`:

![image](https://user-images.githubusercontent.com/43186510/109494146-2aff7580-7a96-11eb-8724-c8991ba0077e.png)

Если у нас всё установлено, то можно двигаться дальше.   
Теперь можно установить всё необходимое для работы с утилитой в наше решение VS и уже напсать код.

Для начала создаем пустой проект С++ в VS и заполняем его данным кодом:
```
#include <stdio.h>
#include "mpi.h"

using namespace std;

int main(int argc, char* argv[])
{
    int numtasks, rank;

    MPI_Init(&argc, &argv);

    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    MPI_Comm_size(MPI_COMM_WORLD, &numtasks);

    printf("Hello MPI From process = %d, total number of processes: %d\n", rank, numtasks);

    MPI_Finalize();
}
```

Теперь укажем путь к подключаемым каталогам MSMPI:

![image](https://user-images.githubusercontent.com/43186510/109494885-28e9e680-7a97-11eb-8051-8c5eef474f1e.png)
![image](https://user-images.githubusercontent.com/43186510/109494917-33a47b80-7a97-11eb-8055-9b3bf1fc8332.png)

После:

![image](https://user-images.githubusercontent.com/43186510/109495002-56cf2b00-7a97-11eb-9022-768f2f8d1bc6.png)
![image](https://user-images.githubusercontent.com/43186510/109495016-5d5da280-7a97-11eb-8c74-98cfe14f99de.png)

Далее:

![image](https://user-images.githubusercontent.com/43186510/109495102-78c8ad80-7a97-11eb-8685-fc9a012a8bf9.png)
![image](https://user-images.githubusercontent.com/43186510/109495129-82eaac00-7a97-11eb-915a-547bfecfd157.png)

Примечание: **Указанные пути могут не совпадать из-за другого имени пользователя**.

#### 2. Вызовем программу и 3. Скомпилируем с произвольным количеством процессов

Перейдем в папку с нашим решением и запустим данную команду `mpiexec -n 16 ParallelComputingLab2.exe`.   
Здесь мы указали количество процессов и исполняемый файл.

![image](https://user-images.githubusercontent.com/43186510/109495659-3e134500-7a98-11eb-94f8-d16b7719845c.png)

#### 4. Процесс запуска не через консоль cmd, а через Локальный отладчик VS

Добавим запуск нашей программы с доп параметрами командной строки:   
Средства -> Внешние инструменты... -> Добавить, а теперь добавим следующие параметры, которые указаны в инструкции:

![image](https://user-images.githubusercontent.com/43186510/109496143-ee814900-7a98-11eb-8d3a-f0a9378294e1.png)
![image](https://user-images.githubusercontent.com/43186510/109496172-fa6d0b00-7a98-11eb-9336-369298dc80ab.png)

Теперь запустим нашу программу через Локальный отладчик VS.

![image](https://user-images.githubusercontent.com/43186510/109496314-2be5d680-7a99-11eb-8d28-cfe07d31290f.png)

Итак, мы установили утилиту и запустили программу с произольным количеством процессов.


