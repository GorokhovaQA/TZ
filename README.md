# TZ
## Документация API для коллекции "Переименование Issue"
### Variables:
{{BaseUrl}} = api.github.com, {{Owner}} = GorokhovaQA, {{Repo}} = TZ, {{N_issue}} = issue_number
### Tests and Snippets.
В данной коллекции были использованы скрипты:

1. Проверка статуса кода ответа

   pm.test("Status code is 200", function ()

   {
    pm.response.to.have.status(200);
});

2. Скрипт для присвоения значения переменной issue_number:

   var key = "N_issue"

   var value = pm.response.json().number

   pm.collectionVariables.set(key, value)

### 1. Authorization
Bearer Token:
this folder is using an authorization helper from collection Аттестация GitHub API Горохова Е
### 2. Создание Issue
POST https://{{BaseUrl}}/repos/{{Owner}}/{{Repo}}/issues

Создание Issue с параметрами:

Название: Issue 1, описание: Something went wrong,
Labels: bug, Assignee: GorokhovaQA

Body request (json):

{
 "title": "Issue 1",

 "body": "Something went wrong",

 "assignee": "GorokhovaQA",

 "labels": ["bug"]
}

Status code: 201 (Created)

### 3. Получение списка Issues
GET https://{{BaseUrl}}/repos/{{Owner}}/{{Repo}}/issues

Получение списка Issues для пользователя для проверки создания Issue 1

Status code: 200 (Ok)

### 4. Переименование Issue
PATCH https://{{BaseUrl}}/repos/{{Owner}}/{{Repo}}/issues/{{N_issue}}

Изменение названия с Issue 1 на Issue 2

Body request (json):

{
 "title": "Issue 2"
}

Status code: 200 (Ok)

### 5. Получение списка Issues
GET https://{{BaseUrl}}/repos/{{Owner}}/{{Repo}}/issues

Получение списка Issues для пользователя для проверки переименования Issue 1 на Issue 2

Status code: 200 (Ok)

### 6. Удаление Issue (закрытие Issue)
PATCH https://{{BaseUrl}}/repos/{{Owner}}/{{Repo}}/issues/{{N_issue}}

Закрытие Issue 2

Body request (json):

{
 "state": "closed"
}

Status code: 200 (Ok)
