# HS+ML: Выучивание на основе алгоритма SaIL
### (Семестровый проект Смолкиной и Горбова МФТИ 2022)
**********

Official repository containing OpenAI Gym environments, agents and ML models for the CoRL paper [Learning Heuristic Search via Imitation](https://arxiv.org/pdf/1707.03034.pdf)
Презентация по проекту - https://docs.google.com/presentation/d/1fLwei7BGBp9R2mv4ZMXZS499SyxUVChI8Ywpfgrbodo/edit?usp=sharing

# Инструкция по установке
## изначально проект написан на python version 2 -> мы переписали его на python 3
One you have installed the required external dependencies (favorably in a virtualenv), you need to execute the following steps in order to get started with the examples.

 - Create a meta folder for the project ``mkdir ~/heuristic_learning `` 
 - Get the 2D planning datasets: ``git clone  https://github.com/SmolkinaJulia/RL_SaIL_project.git
 - Go to the ``examples/`` folder: ``cd ~/heuristic_learning/SaIL/examples``
 - Run ``./run_generate_oracles_xy.sh`` which will generate oracles for all the train, validation and test datasets in the ``motion_planning_datasets`` folder
 - Run ``./run_sail_xy_train.sh`` to train a heuristic for one of the datasets (you can specify the dataset you want inside the script). This runs SaIL for 10 iterations by default. For more information on the rest of the parameters used see the file ``sail_xy_train.py`` 

# Идея и реализация
Нам нужна эвристика которая приведет к минимуму коллизий

Мы хотим вычислить эвристическую policy, которая явно минимизирует expected edge evaluation.
На данный момент достаточно найти достижимый путь в реальном времени.
Может быть расширен для включения стоимости пути в любое время:
Быстро находите возможный путь и уточняйте его с течением времени

 Мы концентрируемся на том - как быстро найти достижимый (feasible) результат


# Идея алгоритма
В Open list - лежат все потенциальные кандидаты
В Closed list -  те что раскрылись
В Invalid - те что не приведут нас к цели (?)

Пока цель не найдена мы выбираем что-то эвристической функцией, раскрываем чтобы получить всех возможных сакссесеров и все невалидные ребра ( сравнивая с конечной целью).
Обновляем наши листы и проделываем эту процедуру пока цель не попадет в open/

Key Insight: Search as sequential decision making under uncertainty(over World map) -Основная идея: поиск как последовательное решение
изготовление в условиях неопределенности (по карте мира)


# Результаты 
![Часть результатов](https://github.com/SmolkinaJulia/RL_SaIL_project/blob/6082e8e945925d7a3d803a44eb474a63f8c918a7/%D1%81%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5%20%D1%81%20%D0%B0%D0%BB%D0%B3%D0%BE%D1%80%D0%B8%D1%82%D0%BC%D0%B0%D0%BC%D0%B8.png)

#### Благодарность mohakbhardwaj его статья - https://mohakbhardwaj.github.io/SaIL/
