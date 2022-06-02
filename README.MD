# NEWTemplate v3+

Данный шаблон полностью новый, отлично подходит для [`aiogram v3.0+`](https://github.com/aiogram/aiogram/tree/dev-3.x).

### Приведем шаблон к рабочему виду :
1. Скопируем файл `.env.dist`, и переименуем его `.env` (.env это рабочий файл, .env.dist это файл просто для примера)
2. Создадим новые хендлеры.
3. **Docker:**
   1. Шаблон полностью готов к работе с  Docker, информация по контейнерам и докеру [жми бля](https://docs.docker.com/get-docker/).
   2. Запускаем проект консольной командой `docker-compose up`
4. **Без Docker(Локально):**
   1. Создадим  [venv](https://docs.python.org/3/library/venv.html)
   2. Далее установим зависимости, которые прописаны в файле requirements.txt: `pip3 install -r requirements.txt`
   3. Запуск проекта консольной командой: `python3 bot.py`


### Как работать и подгружать хендлеры:
Создайте модуль `модуль.py` в папке `handlers`.

Пропишем в файле  `модуль.py`.
```python
from aiogram import Router
user_router = Router()
```
Можно производить несколько роутеров в одном модуле, и на каждый из них скреплять(вешать) хендлеры.
Можно регистрировать хендлеры декораторами:
```python
@user_router.message(commands=["start"])
async def user_start(message):
    await message.reply("Ответик на команду!")
```

Заходим в файл `bot.py` и прописываем все роутеры в файл:
```python
from tgbot.handlers.admin import admin_router
from tgbot.handlers.echo import echo_router
from tgbot.handlers.user import user_router

...

async def main():
   
   ...

    for router in [
        admin_router,
        user_router,
        ...,
        echo_router,

    ]:
        dp.include_router(router)
```

### Тутор aiogram v3
Пока примеров по данному шаблону мало, но @Groosha уже работает над своей [Библией](https://groosha.2038.io/telegram-tutorial-2/).