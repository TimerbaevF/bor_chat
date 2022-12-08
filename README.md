import telebot
from telebot import types

token = "5584516928:AAGzyN8wC2jt8unDKmS4h6qXNhqlvbdQ8Hs"

bot = telebot.TeleBot(token)

@bot.message_handler(content_types=["text"])
def any_msg(message):
    markup = types.InlineKeyboardMarkup(row_width=2)
    first_button = types.InlineKeyboardButton(text="Запись на прием", callback_data="question1")
    second_button = types.InlineKeyboardButton(text="Запись на прием", callback_data="question2")
  	first_button = types.InlineKeyboardButton(text="Запись на прием", callback_data="question1")
		first_button = types.InlineKeyboardButton(text="Запись на прием", callback_data="question1")
		first_button = types.InlineKeyboardButton(text="Запись на прием", callback_data="question1")
		first_button = types.InlineKeyboardButton(text="Запись на прием", callback_data="question1")
    markup.add(first_button, second_button)
    bot.send_message(message.chat.id, "/content/drive/MyDrive/Colab Notebooks/dialogues.txt", reply_markup=markup)

@bot.callback_query_handler(func=lambda call:True)
def callback(call):
    if call.data == "question1":
        markup = types.InlineKeyboardMarkup(row_width=2)
        first_button = types.InlineKeyboardButton(text="1button", callback_data="first")
        second_button = types.InlineKeyboardButton(text="2button", callback_data="second")
        markup.add(first_button, second_button)
        bot.edit_message_text(chat_id=call.message.chat.id,message_id=call.message.message_id, text="menu",reply_markup=markup)

    if call.data == "first":
        keyboard = types.InlineKeyboardMarkup()
        rele1 = types.InlineKeyboardButton(text="1t", callback_data="1")
        rele2 = types.InlineKeyboardButton(text="2t", callback_data="2")
        rele3 = types.InlineKeyboardButton(text="3t", callback_data="3")
        backbutton = types.InlineKeyboardButton(text="back", callback_data="mainmenu")
        keyboard.add(rele1, rele2, rele3, backbutton)
        bot.edit_message_text(chat_id=call.message.chat.id,message_id=call.message.message_id, text="replaced text",reply_markup=keyboard)

    elif call.data == "second":
        keyboard = types.InlineKeyboardMarkup()
        rele1 = types.InlineKeyboardButton(text="another layer", callback_data="gg")
        backbutton = types.InlineKeyboardButton(text="back", callback_data="mainmenu")
        keyboard.add(rele1,backbutton)
        bot.edit_message_text(chat_id=call.message.chat.id,message_id=call.message.message_id, text="replaced text",reply_markup=keyboard)

    elif call.data == "1" or call.data == "2" or call.data == "3":
        bot.answer_callback_query(callback_query_id=call.id, show_alert=True, text="alert")
        keyboard3 = types.InlineKeyboardMarkup()
        button = types.InlineKeyboardButton(text="lastlayer", callback_data="ll")
        keyboard3.add(button)
        bot.edit_message_text(chat_id=call.message.chat.id,message_id=call.message.message_id, text="last layer",reply_markup=keyboard3)



bot.polling(none_stop=True)
