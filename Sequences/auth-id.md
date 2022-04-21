## Auth by ID

```plantuml
@startuml Auth by ID

title "Аутентификация Пользователя - Войти с помощью ID"

participant "Пользователь" as AuthUser
participant "Frontend" as Frontend
participant "Яндекс.Ключ" as YandexKey
participant "Backend" as Backend
participant "Database" as DB

Frontend -> AuthUser : Введите Ваш ID
AuthUser -> Frontend : ID
Frontend -> Frontend : Проверить ID
alt "ID Корректен"
    Frontend -> Backend : Проверить ID
    Backend -> DB : Предоставь Информацию о Пользователе по ID
    DB -> Backend : Информация о Пользователе по ID
    Backend -> Backend : Проверить ID
    alt "ID Корректен"
        Backend -> Frontend : ID Корректен
        Frontend -> AuthUser : Выберите способ аутентификации
        alt "Вход по Яндекс.Ключ"
            AuthUser -> YandexKey : Подтверди Пользователя
            YandexKey -> Backend : Подтверждаю Пользователя
            Backend -> Frontend : Пользователь Аутентифицирован
            Frontend -> AuthUser : Вы успешно вошли в сервис
        else "Вход по Одноразовому Паролю"
            AuthUser -> Frontend : Вход по Одноразовому Паролю
            Frontend -> AuthUser : Введите Ваш Одноразовый Пароль
            AuthUser -> Frontend : Пароль
            Frontend -> Backend : Проверить ID и одноразовый пароль
            Backend -> DB : Предоставь Информацию о Пользователе по ID
            DB -> Backend : Информация о Пользователе по ID
            Backend -> Backend : Проверить ID и одноразовый пароль
            alt "ID и одноразовый пароль Корректны"
                Backend -> Frontend : Пользователь Аутентифицирован
                Frontend -> AuthUser : Вы успешно вошли в сервис
            else "ID и одноразовый пароль Корректны"
                Backend -> Frontend : ID или одноразовый пароль не Корректены
                Frontend -> AuthUser : Введите Ваш ID
            end
        end
    else "ID не Корректен"
        Backend -> Frontend : ID не Корректен
        Frontend -> AuthUser : Введите Ваш ID
    end
else "ID не Корректен"
    Frontend -> AuthUser : Введите Ваш ID
end
@enduml