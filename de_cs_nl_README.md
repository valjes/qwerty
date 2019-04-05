# QWERTY

測試一些文字

example: " {gender_of_host, select, female { {num_guests, plural, =0 {{host} does not celebrate her birthday.} one {{host} invites one guest to her birthday.} other {{host} invites # guests to her birthday.} } } male { {num_guests, plural, =0 {{host} does not celebrate his birthday.} one {{host} invites one guest to his birthday.} other {{host} invites # guests to his birthday.} } } other { {num_guests, plural, =0 {{host} do not celebrate their birthday.} one {{host} invite one guest to their birthday.} other {{host} invite # guests to their birthday.} } } } "