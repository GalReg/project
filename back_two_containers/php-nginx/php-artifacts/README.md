# Веб-апи с гугл-авторизацией

## Апи для Classroom

- GET classroom/hc – проверка, что апи работает
- POST classroom/post/data – залить данные на сервер

    Формат: https://docs.google.com/document/d/12w99lv_1UuuznvZAp6XwqvljOAuBY7_akp4OM-ZPCEc/edit?ts=5e3a8f8d
    
- GET api/сlassroom/student/courseworks – задания студента

    Формат:
    
    ```json
    {
      "message": "success",
      "code": 20000,
      "data": [
        {
          "date": "2019-10-30T15:14:20+00:00",
          "subject": "2019 Компьютерная графика",
          "task": "VR / AR устройства",
          "teacher": "Анастасия Вильгельм",
          "deadline": "2019-10-17T20:59:00+00:00",
          "status": "возвращено",
          "maxReached": 3,
          "maxPossible": 3
        },
        {
          "date": "2019-10-06T20:14:48+00:00",
          "subject": "2019 Компьютерная графика",
          "task": "Практические занятия",
          "teacher": "Classroom Сервисный аккаунт",
          "deadline": "2019-10-17T20:59:00+00:00",
          "status": "сдано",
          "maxReached": 0,
          "maxPossible": 53
        }
      ]
    }
    ```
  
  - GET api/сlassroom/student/progress – успеваемость студента
  
    Формат:  
  
    ```json
    {
      "message": "success",
      "code": 20000,
      "data": {
        "firstCourse": {
          "firstCourse": {
            "firstModule": [],
            "secondModule": [],
            "thirdModule": [],
            "fourthModule": []
          }
        },
        "secondCourse": {
          "secondCourse": {
            "firstModule": [],
            "secondModule": [],
            "thirdModule": [],
            "fourthModule": []
          }
        },
        "thirdCourse": {
          "thirdCourse": {
            "firstModule": [],
            "secondModule": [],
            "thirdModule": [
              {
                "course": "2019 Компьютерная графика",
                "passed": "38.2022",
                "unknown": "61.7978",
                "failed": "0.0000"
              }
            ],
            "fourthModule": []
          }
        },
        "fourthCourse": {
          "fourthCourse": {
            "firstModule": [],
            "secondModule": [],
            "thirdModule": [],
            "fourthModule": []
          }
        }
      }
    }
    ```

## Апи для клиента

#### Private api (auth user only)
- api/project/header/{id} – name_rus, name_eng и тд
- api/project/body/{id} – все остальное по проекту
- api/vacancies/project/{projectId} - вакансии проекта
- api/students/project/{projectId} - студенты в проекте
- api/statistics/trello/task/{projectId} – статистика по проекту
- api/statistics/trello/hours/{projectId} – статистика для графиков по накопленным часам trello
- api/projects – каталог проектов
- GET api/student/projects/my – активные проекты зарегестрированного студента (мои проекты)
- GET api/student/applications/my/{approved} – активные заявки на проекты зарегистрированного студента. Параметр approved – подтверждена или нет заявка руководителем (0 – ожидание или отклонена, 1 – одобрена)
- POST api/leader/application/confirm – изменение статуса заявки для руководителя
- POST api/student/application/confirm – изменение статуса заявки для студента
- POST api/leader/project/update – обновить информацию о проекте.
- GET api/student/projects/and/applications/my
- POST api/student/application/add
- POST api/office/project/add

#### Public-api
- GET public-api/reference/addprojectform получить данные для формы добавления проекта

### Форматы данных

- api/statistics/trello/hours/{projectId} – статистика для графиков по накопленным часам trello

```json
{
  "byWeeks": [
    "01.11",
    "08.11",
    "15.11",
    "22.11",
    "29.11"
  ],
  "byMonths": [
    "1 цикл",
    "2 цикл",
    "3 цикл",
    "4 цикл",
    "5 цикл",
    "6 цикл",
    "7 цикл",
    "8 цикл"
  ],
  "studentsByMonths": [
    {
      "hours": [
        10,
        7,
        7,
        0,
        0,
        0,
        0,
        0
      ],
      "name": "Поздняков Филипп Олегович"
    },
    {
      "hours": [
        0,
        15,
        15,
        0,
        0,
        0,
        0,
        0
      ],
      "name": "Ракина Анна Сергеевна"
    },
    {
      "hours": [
        5,
        11.0,
        11.0,
        0,
        0,
        0,
        0,
        0
      ],
      "name": "Среднее"
    }
  ],
  "studentsByWeeks": [
    {
      "hours": [
        0,
        7,
        0,
        0,
        0
      ],
      "name": "Поздняков Филипп Олегович"
    },
    {
      "hours": [
        0,
        0,
        0,
        15,
        0
      ],
      "name": "Ракина Анна Сергеевна"
    },
    {
      "hours": [
        0,
        3.5,
        0,
        7.5,
        0
      ],
      "name": "Среднее"
    }
  ],
  "all": 54,
  "period": 22,
  "studentsAll": [
    {
      "hours": 24,
      "name": "Поздняков Филипп Олегович"
    },
    {
      "hours": 30,
      "name": "Ракина Анна Сергеевна"
    }
  ],
  "studentsPeriod": [
    {
      "hours": 7,
      "name": "Поздняков Филипп Олегович"
    },
    {
      "hours": 15,
      "name": "Ракина Анна Сергеевна"
    }
  ]
}
```

- POST api/leader/application/confirm – изменение статуса заявки для руководителя

leader_confirm = {0, 1, 2}

Запрос:
```json
{
	"leader_confirm": 1,
	"application_id": 16
}
```

Ответ:
```json
{
  "message": "Leader confirmation successful",
  "code": 20000
}
```

- POST api/student/application/confirm – изменение статуса заявки для студента

student_confirm = {0, 1, 2}

Запрос:
```json
{
	"application_id": 17,
	"student_confirm": 2
}
```

Ответ:
```json
{
  "message": "Student confirmation successful",
  "code": 20000
}
```

- POST api/leader/project/update – обновить информацию о проекте.

Обязательное поле project_id
```json
{
	"project_id": 72,
	"target": "to win",
	"annotation": "annotation",
	"result_exp": "result",
	"competency": "competency",
	"resource": "resource",
	"control": "control",
	"result_form": "result"
}
```

- GET api/student/projects/and/applications/my

Формат ответа:
```json
{
  "data": {
    "projects": {
      "data": [
        {
          "project_id": 72,
          "project_name": "Сервисы интегрированной цифровой среды",
          "role": "Backend",
          "type": "Прогр.",
          "leader": "Башун Владимир Владимирович",
          "team": [
            "Backend"
          ],
          "state": "Рабочий",
          "approved": 0,
          "accumulated": 24.0
        }
      ],
      "code": 20000
    },
    "applications": {
      "data": [
        {
          "id": 17,
          "status": 0,
          "role": "Инженер",
          "leader": "Королев Денис Александрович",
          "project_name": "Мобильный управлятор PTZ",
          "type": "Прогр.",
          "team": [
            "Инженер"
          ]
        }
      ],
      "code": 20000
    },
    "approved_applications": {
      "message": "No applications found",
      "code": 40400
    }
  },
  "code": 20000
}
```

- POST api/student/application/add

```json
{
	"vacancy_id": 5,
	"about_me": "I'm a good engineer."
}
```

- POST api/office/project/add

```json
{
    "direction_leader_email": "arolich@miem.hse.ru",
    "direction_leader_name": "Ролич Алексей",
    "project_leader_email": "sslastnikov@miem.hse.ru",
    "project_leader_name": "Сластников Сергей",
    "project_name": "Unit tests",
    "team": "209 Команда Сергеева",
    "teamVal": 209,
    "source": "ВШЭ/МИЭМ",
    "sourceVal": 2,
    "type": "Программный",
    "typeVal": 2
}
```

## Апи для trello

### Адреса

- GET /trello/acum/student/{trelloId} – запись из таблицы TrelloAcum для студента с заданным trelloId;
- GET /trello/acum/project/{projectNumber} – записи из таблицы TrelloAcum с заданным projectNumber;
- POST /trello/add/acums – Добавить новые записи в таблицу TrelloAcum.
- DELETE /trello/acum – удалить одну запись из таблицы TrelloAcum (накоп).
- GET /trello/status/student/{studentId} – trello-статусы по id студента;
- GET /trello/status/project/{projectNumber} – trello-статусы по номеру проекта;
- POST /trello/add/status – добавить новые записи в таблицу TrelloStatus
- POST /trello/update/status – обновить одну запись в таблице TrelloStatus (по project number и cycle)
- POST /trello/add/logs – добавить логи
- POST /trello/check/occupation – проверить должность юзера по trello_id
- POST /trello/add/reviews – добавить отзывы руководителей об исполнителях
- POST /trello/update/review – обновить отзыв. Тело запроса должно содержать поле "id"
- DELETE /trello/delete/review/{card_id} – удалить отзыв по card_id.
- GET /trello/reviews – выбрать все отзывы
- POST /trello/reviews/filter – выбрать отзывы, удовлетворяющие заданным условиям
- POST /trello/user/update/{userId} - обновить данные пользователя (по ID)
- POST /trello/user/updateByEmail - обновить данные пользователя (по email)

### Форматы входных данных 
- POST /trello/add/acums – Добавить новые записи в таблицу TrelloAcum
```json
[
	{
		"student_trello_id": 15,
		"project_number": 2,
		"cycle": 3,
		"hours": 4.5,
		"card_id": 5,
		"date": "2019-10-28T20:15:40.571Z"
	},
	{
		"student_trello_id": 16,
		"project_number": 2,
		"cycle": 3,
		"hours": 4.2,
		"card_id": 5,
		"date": "2019-10-28T20:15:40.571Z"
	}
]
```

- POST /trello/add/status – добавить новые записи в таблицу TrelloStatus
```json
[
    {
    "project_number": 19112,
    "cycle": 3,
    "status": true,
    "comment": "all targets achieved!",
    "reporter_email": "vbashun@miem.hse.ru"
    },
    {
    "project_number": 19112,
    "cycle": 4,
    "status": true,
    "comment": "all targets achieved!",
    "reporter_email": "vbashun@miem.hse.ru"
    }
]
```
- POST /trello/update/status – обновить одну запись в таблице TrelloStatus (по project number и cycle)
```json
{
"project_number": 19112,
"cycle": 4,
"status": true,
"comment": "all targets achieved! - fixed",
"reporter_email": "vvbashun@miem.hse.ru"
}
```

- POST /trello/add/logs – добавить логи
```json
[
	{
		"title": "Ожидание",
		"status": true,
		"card_title": "Дизайн страницы",
		"card_id": "12345cardId",
		"hours": 5.5,
		"members": [
			"id1",
			"id2",
			"id3"
		],
		"marked_by": "id2",
		"mark_date": "2019-10-28T20:15:40.571Z"
	},
	{
		"title": "Отклонено",
		"status": false,
		"card_title": "Написание апи",
		"card_id": "12345cardId",
		"hours": 5.5,
		"members": [
			"id1",
			"id2",
			"id3"
		],
		"marked_by": "id2",
		"deadline": "2019-10-28T20:15:40.571Z",
		"mark_date": "2019-10-28T20:15:40.571Z"
	}
]
```
- POST /trello/check/occupation – проверить должность юзера по trello_id
```json
{
	"trello_id": "some_id"
}
```

- POST /trello/add/reviews – добавить отзывы руководителей об исполнителях
```json
[
    {
        "worker_email": "worker@mail.ru",
        "student_email": "student@mail.ru",
        "project_number": 19112,
        "review": null,
        "cycle": 5,
        "work_together": true,
        "review_date": "08.11.1998",
        "card_id": "5db966e6462e881616e48ab8",
          "type": 1
    },
    {
        "worker_email": "worker1@mail.ru",
        "student_email": "student2@mail.ru",
        "project_number": 19112,
        "review": null,
        "cycle": 5,
        "work_together": true,
        "review_date": "08.11.1996",
          "type": 1,
          "card_id": "111116e6462e881616e48ab8" 
    }
]
```

- POST /trello/update/review – обновить отзыв. Тело запроса должно содержать поле "id"
```json
{
	"card_id": "5db966e6462e881616e48ab8", 
	"review": "This was so great to work with him3333"
} 
```

- POST /trello/reviews/filter – выбрать отзывы, удовлетворяющие заданным условиям.
Можно указать одно или несколько условий
```json
{
	"worker_email": "dkorolev@miem.hse.ru",
	"student_email": "aavilgelm@miem.hse.ru",
	"project_number": 0,
	"cycle": 2,
    "type": 1,
	"work_together": true,
    "card_id": "777776e6462e881616e48ab8"
}
```

- DELETE /trello/acum – удалить одну запись из таблицы TrelloAcum (накоп).
```json
{
	"student_trello_id": "5d7e7c8c20ec375f10188684", 
	"card_id": "5db966e6462e881616e48ab8"
}
```

- POST /trello/user/update/{userId} - обновить данные пользователя (по ID).
Возможные поля запроса (в формате JSON) приведены ниже (может быть передано одно или несколько полей)
```json
{
	"fullName": "Тетсовое имя",
	"trello_id": "1111111",
	"trello_name": "My trello name!",
	"phone": "234-45-45"
}
```

- POST /trello/user/updateByEmail - обновить данные пользователя (по email). 
Возможные поля запроса (в формате JSON) приведены ниже (может быть передано одно или несколько полей). 
Поле email является обязательным. 
```json
{
	"email": "lbarash@miem.hse.ru",
	"fullName": "Новое тестовое имя",
	"trello_id": "1212121",
	"trello_name": "My newtrello name!",
	"phone": "1234-45-451"
}
```


Запрос на авторизацию через vue делается по адресу /vue/google. В хедере запроса необходимо передавать токен, приходящий с сервера {'X-AUTH-TOKEN': token}

Ссылка на документацию:
https://drive.google.com/drive/folders/1qfcjatH3J7wAdABi4dTznBOuTN4qkKQP?usp=sharing
