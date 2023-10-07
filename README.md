# RuCode.Финал 2023. ИИ
### Всероссийский учебный фестиваль по искусственному интеллекту
## ❓ Задача
Даны записи радара о передвижении марсиан на автомобилях на воздушной подушке. Задача делится на:
#### Задача А:
*Регрессия*: найти долю сигнала в верхней поляризации, метрика R2*70
#### Задача B:
*Бинарная классификация*: классифицировать порядочных марсиан и марсиан-лихачей, метрика F1*30</br>
#### Поля в обучающей выборке:
* № испытания;
* Модуль сигнала;
* Тип_измерения;
* Количество импульсов;
* Фаза Hor;
* Фаза Ver;
* Уровень шума;
* У.М.;
* Секунда;
* Дальность (м);
## :tada: Результат
:chart_with_upwards_trend: Score: **80.99**</br>
Задача А: **51.19**</br>
Задача B: **29.80**</br>
Продвинутый трек: **7 место**</br>
Начинающий трек: **2 место** 🥈</br>
## :memo: Решение
1. Из некоторых данных смогли получить координаты, откуда исходит сигнал:</br>
![image](https://github.com/daniil-dushenev/rucode2023/assets/44606552/97cd7d72-a319-4750-bb98-aa708536bdb3)
2. Убрали шумные фичи:</br>
![image](https://github.com/daniil-dushenev/rucode2023/assets/44606552/0293dd89-350f-4581-8d99-cbf819362153)
3. Использовали данные из задачи B для дообучения модели под задачу А, так как там были те же самые данные, только с фичей таргета из первой задачи.</br>
#### Стэк моделей для задачи А:</br>
![image](https://github.com/daniil-dushenev/rucode2023/assets/44606552/72741c4b-0473-4231-9c4e-7f284a3211ed)
</br>
Результаты каждой из модели мы усредняли и получали итоговую величину.
#### Стэк моделей для задачи B:</br>
![image](https://github.com/daniil-dushenev/rucode2023/assets/44606552/3be04182-d562-4f2e-9ba4-94bfe36997ee)
</br>
Результаты усредняли и округляли до целого (0 или 1)
## :bulb: Идеи
1. Хотели кластеризировать данные по координатам на 10-15 кластеров и к каждому сэмплу добавлять номер его кластера и среднее некоторых признаков, относящихся к этому кластеру
2. Сжали данные с помощью TSNE и увидели, что данные хорошо разбиваются на 3 кластера, после этого внесли номер кластера для каждого сэмпла, но прироста в качестве не было![image](https://github.com/daniil-dushenev/rucode2023/assets/67290783/b1edba3e-496d-42f3-a2de-3d2e0a3c9798)
3. Векторизовали данные через MLP и подавали в ансамбль, ожидаемо, нейросети не дали прироста в качестве, т.к. в этих данных не нужно учитывать пространственную или временную информацию
4. Так же обучили мета-модель, которая выдает финальный ответ, основываясь на выходах ансамбля моделей. По качеству стэкинг и бэггинг одинаковы
   

