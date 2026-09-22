## Troubleshooting

### Ошибка `'ascii' codec can't encode characters`
**Что видел:** при запуске со сломанным `GIGACHAT_CREDENTIALS` появилась ошибка:
`'ascii' codec can't encode characters in position 7-15: ordinal not in range(128)`.
**Почему:** в `GIGACHAT_CREDENTIALS` были русские символы (`сломанный_ключ`), которые не удалось передать в HTTP-заголовке авторизации.
**Что сделал:** реализовал fallback через `try/except`. При ошибке GigaChat запрос автоматически отправляется в HuggingFace, поэтому программа не падает и пользователь получает ответ.

### Неверные данные авторизации GigaChat
**Что видел:** сообщение:
`Invalid credentials format. Please use only base64 credentials`.
**Почему:** вместо настоящего `GIGACHAT_CREDENTIALS` был указан намеренно неправильный ключ.
**Что сделал:** после проверки fallback вернул рабочий `GIGACHAT_CREDENTIALS`. После этого запрос снова успешно выполнился через `[GigaChat]`.