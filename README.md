# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил:
- Сажин Егор Алексеевич
- РИ210946
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Познакомиться с программными средствами для организции передачи данных между инструментами google, Python и Unity.

## Задание 1
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity. При выполнении задания используйте видео-материалы и исходные данные, предоставленные преподавателя курса.
Ход работы:

- В облачном сервисе google console подключить API для работы с google sheets и google drive.

![GoogleColab](https://user-images.githubusercontent.com/102538132/194267037-72fec0de-66c0-4c56-b2db-23a0e96bd80e.png)
![Доступ](https://user-images.githubusercontent.com/102538132/194271960-0817146b-68cb-42da-a807-f069a2bd8184.png)


- Реализовать запись данных из скрипта на python в google-таблицу. Данные описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с учётом стоимости игрового объекта в каждый период.

![Python(1)](https://user-images.githubusercontent.com/102538132/194272038-761f1e51-34c2-4e52-a2c6-f697523e9c02.png)
![Python(2)](https://user-images.githubusercontent.com/102538132/194272068-55e72924-ea31-4f58-bb99-96d4ef8f0739.png)
![GoogleSheets](https://user-images.githubusercontent.com/102538132/194272101-2836a799-6456-4d4d-9f18-e285592c6f07.png)


- Создать новый проект на Unity, который будет получать данные из google-таблицы, в которую были записаны данные в предыдущем пункте.

![Unity](https://user-images.githubusercontent.com/102538132/194272366-4a4583b1-97d4-4254-b3b5-1db0804e9708.png)


- Написать функционал на Unity, в котором будет воспризводиться аудио-файл в зависимости от значения данных из таблицы.

![script(1)](https://user-images.githubusercontent.com/102538132/194272482-9214ef36-7d42-446b-b8c5-ff6674ddbae5.png)
![script(2)](https://user-images.githubusercontent.com/102538132/194272500-1de1643c-f1f8-4f49-8a18-f574892703b7.png)
![script(3)](https://user-images.githubusercontent.com/102538132/194272525-5c3cd39c-ec47-413b-8e68-d878bb657fd9.png)


## Задание 2
### Реализовать запись в Google-таблицу набора данных, полученных с помощью линейной регрессии из лабораторной работы № 1



## Задание 3
### Самостоятельно разработать сценарий воспроизведения звукового сопровождения в Unity в зависимости от изменения считанных данных в задании 2

1) Производя итерации во 2 задании, мы каждый раз мы изменяем параметр times функции iterate. При этом loss не претерпевает особых изменений, из этого следует, что изменение исходных данных не влечёт за собой изменений loss, то есть loss стремится к нулю. Пример:
```py

#iterated function, return a and b

def iterate(a,b,x,y,times):
  for i in range(times):
    a,b = optimize(a,b,x,y)
  return a,b

```
Можно увидеть, что количество итераций функции iterate(times) влияет на переменные a и b, а те определяют результат переменной loss. Доказательства что от изменения количества итераций графики не изменялись можно посмотреть на скринах 2 задания:

```py

#For the first iteration, the parameter values, losses, and visualization after the iteration are displayed

a,b = iterate(a,b,x,y,2)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y) 
print(a,b,loss)
plt.scatter(x,y)
plt.plot(x,prediction)

a,b = iterate(a,b,x,y,10000)
prediction=model(a,b,x)
loss = loss_function(a, b, x, y) 
print(a,b,loss)
plt.scatter(x,y)
plt.plot(x,prediction)

```

2) Следуя из кода ниже и двух следующих скринов, можно сказать, что Lr отвечает за линейную регрессию, её направление. При увеличении Lr угол увеличивается.

```py

def optimize(a,b,x,y):
  num = len(x)
  prediction = model(a,b,x)
  #Update the values of A and B by finding the partical derivatives of the loss function on a and b
  da = (1.0/num) * ((prediction - y)*x).sum()
  db = (1.0/num) * ((prediction - y).sum())
  a = a - Lr*da
  b = b - Lr*db
  return a, b

```

![2 2](https://user-images.githubusercontent.com/102538132/191975741-53e6a025-b59f-49ae-9b53-2ce0e9486680.png)
![2 1](https://user-images.githubusercontent.com/102538132/191975749-7d460d69-8fb1-417e-ab88-efe7b22b4648.png)



## Выводы
Выполняя эту лабораторную работу, я впервые познакомился с github, научился оформлять отчёт, поработал с Google Collab, научился писать на Unity и Google Collab писать программы. Поработал с алгоритмом линейной регрессии, учился вникать в код и изучать на очень доскональном уровне, проработал с графиками и научился аннализировать их.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
