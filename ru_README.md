# БУКВ

для теста какой-либо текст

Пример: " {gender_of_host, select, female { {num_guests, plural, =0 {{host} не празднует свой день рождения!} one {{host} приглашает одного гостя на день рождения.} other {{host} приглашает # гостей на свой день рождения!} } } male { {num_guests, plural, =0 {{host} Не празднует свой день рождения!} one {{host} Приглашает одного гостя на его день рождения!} other {{host} Приглашает # гостей на день рождения} } } other { {num_guests, plural, =0 {{host} не отмечаю свой день рождения.} one {{host} пригласить одного гостя в день рождения.} other {{host} приглашаем # гостей до их рождения.} } } } "