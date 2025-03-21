# Лабараторная работа №5
### Автоматизация проверки формата файлов при коммите

Пусть файл будет проверять гоночные лицензии гонщиков, в таком случае в файле должно быть словосочетание "Номер гоночной лицензии", буду проверять его наличие. Поместим скрипт в папку .git/hooks в файл pre-commit:

```
#!/bin/bash
if grep -q ""Номер гоночной лицензии" ex.txt
 then echo "Гоночная лицензия проверена"
else
 echo "Ошибка! В файле нет номера гоночной лицензии"
fi
```

Проверяю работу скрипта, все работает отлично.

![image](https://github.com/user-attachments/assets/f8ddfb5c-4cea-48c6-87fd-cfe2b26bc4c8)


### Использование Git Flow в проекте

Выполняем инициализацию Git Flow в корне репозитория:
```
git flow init
```
Создадим ветку для новой функциональности "task-management":
```
git flow feature start task-management
```
Внесу изменения в код файла task_manager.py, чтобы добавить функционал управления задачами:
```
def create_task(title):
    # Логика создания задачи
    print(f"Создана новая задача: {title}")
```
Сделаю коммит для изменения по мере разработки:
```
git add task_manager.py
git commit -m "Добавлен функционал управления задачами"
```
Завершим фичу и объединим ее с основной веткой когда завершим разработку функции:
```
git flow feature finish task-management
Git Flow автоматически переключится на ветку develop и выполнит слияние.
```
Переключимся на ветку "develop" и начнём создание релиза:
```
git checkout develop
git flow release start v1.0.0
```
Обновим версию в файле version.txt:
```
echo "v1.0.0" > version.txt
git add version.txt
git commit -m "Обновлена версия для релиза v1.0.0"
```
В конце, завершаем релиз и объединяем его с двумя ветками "develop" и "main":
```
git flow release finish v1.0.0
```
Создаём файл hotfix для случаев возникновения ошибок, который будет их исправлять:
```
git flow hotfix start hotfix-1.0.1
```
Вносим изменения для исправления ошибки и коммитим эти самые изменения:
```
# Исправление ошибки
git add file_with_error.py
git commit -m "Исправлена критическая ошибка"
```
Завершаем файл hotfix и объединяем его с ветками "develop" и "main":
```
git flow hotfix finish hotfix-1.0.1
```
В конце, завершаем работу и отправляем все изменения на удаленный репозиторий:
```
git push origin develop
git push origin main
```
![image](https://github.com/user-attachments/assets/f79daa99-ffcd-4b77-bab1-b1a4c0dd202c)



