# Первичный доступ (Initial Access)

## OWASP Juice Shop
**Цель:** Отработка веб-уязвимостей.

### Выполненные задания:
1. **SQL Injection (Login Admin):** Вход в аккаунт администратора через `'' OR 1=1 --`.
2. **SQL Injection (Database Schema):** Извлечение схемы БД через `UNION SELECT` (payload: `qwert'')) UNION SELECT sql, ''2'', ... FROM sqlite_master--`).
3. **SQL Injection (User Credentials):** Выгрузка email и хешей паролей.
4. **DOM XSS:** Внедрение `<iframe src="javascript:alert(''xss'')">` в поисковую строку.
5. **Bonus Payload XSS:** Использование расширенного payload.
6. **Broken Access Control (Admin Section):** Прямой доступ к `/#/administration`.
7. **IDOR (Basket Access):** Изменение `bid` в JWT-токене для доступа к чужой корзине.
8. **Password Strength:** Брутфорс пароля администратора (пароль `admin123`).
9. **Forged Review:** Подделка отзыва от имени другого пользователя.
10. **Manipulate Basket:** Добавление товара в чужую корзину.
11. **Exposed Metrics:** Доступ к `/metrics`.
12. **Forged Coupon:** Генерация купона на скидку 90% через Z85-кодирование.
13. **Upload Size / Upload Type:** Обход валидации файлов.
14. **Empty/Admin Registration:** Регистрация с пустыми полями и с ролью `admin`.
15. **CSRF:** Изменение имени пользователя.
16. **Unsigned JWT:** Подделка JWT с `alg: none`.
