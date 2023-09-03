import telebot
import math
import re
from fractions import Fraction
from telebot import types, TeleBot
from telebot import custom_filters
from telebot.handler_backends import State, StatesGroup
from telebot.storage import StateMemoryStorage

state_storage = StateMemoryStorage()
bot = telebot.TeleBot('telegram token', state_storage=state_storage)


# KeyBoard
markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
item1 = types.KeyboardButton("Привет")
markup.add(item1)

markup1 = types.ReplyKeyboardMarkup(resize_keyboard=True)
item1 = types.KeyboardButton("Уравнения")
item3 = types.KeyboardButton("Неравенство")
item4 = types.KeyboardButton("Горнер")
markup1.add(item1,item3,item4)

markup2 = types.ReplyKeyboardMarkup(resize_keyboard=True)
item1 = types.KeyboardButton("Квадратное")
item2 = types.KeyboardButton("Кубическое")
item3 = types.KeyboardButton("Биквадратное")
item4 = types.KeyboardButton("Возвратное 4 степени")
item5 = types.KeyboardButton("Вернуться назад")
markup2.add(item1,item2,item3,item4,item5)

markup3 = types.ReplyKeyboardMarkup(resize_keyboard=True)
item1 = types.KeyboardButton("Квадратное")
item2 = types.KeyboardButton("Кубическое")
item3 = types.KeyboardButton("Вернуться назад")
markup3.add(item1,item2,item3)

class MainStates(StatesGroup):
    scheme_gorner = State()
    problem_types = State()
    equation_subtypes = State()
    equation_system_subtypes = State()
    inequation_subtypes = State()
    start_state = State()


class Equation_Substypes(StatesGroup):
    Quadratic_equation = State()
    Сubic_equation = State()
    Biquadratic_equation = State()
    Return_equation = State()
class InEquation_Substypes(StatesGroup):
    Quadratic_inequation = State()
    Сubic_inequation = State()

@bot.message_handler(commands=['start'])
def start_message(message):


    bot.send_message(message.from_user.id,
                     "Привет!Я универсальный бот для решения алгебраических задач. "
                     ,reply_markup=markup)
    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)



@bot.message_handler(state=MainStates.start_state)
def first_message(message):

    if message.text == "Привет":
        bot.send_message(message.from_user.id, "Выберите,что решить из списка:\n"
                                               "1. Уравнения\n"
                                               "2. Неравенство\n"
                                               "3. Схема Горнера\n",reply_markup=markup1)
        bot.set_state(message.from_user.id, MainStates.problem_types, message.chat.id)
    else:
        bot.send_message(message.from_user.id, "Я вас не понимаю. Для работы напишите 'Привет'")


@bot.message_handler(state=MainStates.problem_types)
def problem_types(message):
    if message.text== "Уравнения":
        bot.send_message(message.from_user.id, "Выберите нужную категорию:\n""1.1 Квадратное уравнение\n"

                                               "1.2 Кубическое уравнение\n"

                                               "1.3 Биквадратное уравнение\n"

                                               "1.4 Возвратное уравнение 4 степени\n"

                                               "0.Вернуться назад\n",reply_markup=markup2)
        bot.set_state(message.from_user.id, MainStates.equation_subtypes, message.chat.id)


    elif message.text =="Неравенство" :
        bot.send_message(message.from_user.id, "Выберите нужную категорию:\n""1.1 Квадратное неравенство\n"

                                               "1.2 Кубическое неравенство\n"

                                               "0.Вернуться назад\n",reply_markup = markup3)
        bot.set_state(message.from_user.id, MainStates.inequation_subtypes, message.chat.id)

    elif message.text == "Горнер":
        bot.send_photo(message.chat.id, photo=open('/home/opc/pyth/photos/item7.jpg', 'rb'))
        bot.send_message(message.from_user.id, "Введите коэффициенты через пробел:")
        bot.set_state(message.from_user.id, MainStates.scheme_gorner, message.chat.id)

    else:
        bot.send_message(message.from_user.id, "Напишите один из предложенных вам вариантов")
        bot.set_state(message.from_user.id, MainStates.problem_types, message.chat.id)

def fraction(n):
    for i in range(len(n)):
        if bool(n[i].find('/')) == True:
            n[i] = float(sum(Fraction(s) for s in n[i].split()))
        else:
            n[i] = int(n[i])
    return n

@bot.message_handler(state=MainStates.scheme_gorner)
def scheme_gorner(message):
    dellist = []
    answers_list = []

    def get_all_divisors_brute(n):
        if n < 0:
            n = n * -1
        for i in range(1, int(n / 2) + 1):
            if n % i == 0:
                yield i
        yield n

    def apply_divisors(n):

        for i in get_all_divisors_brute(n):
            dellist.append(i)
        for i in range(len(dellist)):
            if 1 / dellist[i] not in dellist:
                dellist.append(1 / dellist[i])
        for i in range(len(dellist)):
            dellist.append(dellist[i] * -1)
        print(dellist)



    def gorner(koeff):
        for i in range(len(dellist)):
            new_koeff = []
            number = 0
            print('проверяем', dellist[i])
            for j in range(len(koeff) - 1):
                if number == 0 and (len(new_koeff) == 0):
                    number = dellist[i] * koeff[j] + koeff[j + 1]
                else:
                    number = dellist[i] * number + koeff[j + 1]

                new_koeff.append(number)
                print(number)
                print(new_koeff, 'Новые коэффициенты')
                if (number == 0) and (len(new_koeff) == len(koeff2) - 1):
                    answers_list.append(dellist[i])
                    global last_koeff
                    last_koeff = new_koeff
                    print(answers_list, 'Поиск коэффициентов')
                    if (len(answers_list) == len(koeff2) - 1):
                        return answers_list

    koeff2 = message.text.split(' ')
    fraction(koeff2)
    apply_divisors(koeff2[-1])
    gorner(koeff2)
    answer = ''
    new_koeff = []
    if len(koeff2) - 1 == len(answers_list):
        for i in range(len(answers_list)):
            answer = answer + '(x-' + str(answers_list[i]) + ') '

        answer = answer.replace('--', '+')
        bot.send_message(message.from_user.id,'Ответ: '+answer+' = 0')

    else:
        try:

            bot.send_message(message.from_user.id,'Уравнение не раскладывается на целые числа.')
            answer = ''
            last_koeff.pop(-1)
            for i in range(len(answers_list)):
                answer = answer + '(x-' + str(answers_list[i]) + ') '
            answer = answer + '(' + str(koeff2[0])
            for j in range(len(last_koeff)):
                answer = answer + 'x^' + str((len(last_koeff) - j)) + ' + ' + str(last_koeff[j])
            answer = answer + ')'
            answer = answer.replace('--', '+')
            answer = answer.replace('+ -', '-')
            answer = re.sub('\D 0x\D\d ', '', answer)
            bot.send_message(message.from_user.id,'Ответ: '+answer+' = 0')


        except NameError:
            bot.send_message(message.from_user.id,'x ∉ R')
    bot.send_message(message.from_user.id,"Для продолжения работы бота отправьте слово 'Привет' ", reply_markup=markup)
    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

@bot.message_handler(state=MainStates.inequation_subtypes)
def maininequation_subtypes(message):
    if message.text =="Квадратное":
        bot.send_photo(message.chat.id, photo=open('/home/opc/pyth/photos/item5.jpg', 'rb'))
        bot.send_message(message.from_user.id, "Введите коэффициенты A B C и знак(>,<,>=,=<) через пробел")
        bot.set_state(message.from_user.id, InEquation_Substypes.Quadratic_inequation, message.chat.id)
    elif message.text =="Кубическое":
        bot.send_photo(message.chat.id, photo=open('/home/opc/pyth/photos/item6.jpg', 'rb'))
        bot.send_message(message.from_user.id, "Введите коэффициенты A B C D и знак(>,<,>=,=<) через пробел")
        bot.set_state(message.from_user.id, InEquation_Substypes.Сubic_inequation, message.chat.id)
    elif message.text == "Вернуться назад":
        bot.send_message(message.from_user.id, "Выберите,что решить из списка:\n" " 1.Уравнения\n"
                                               " 2.Неравенство\n"
                         "3. Схема Горнера\n",reply_markup=markup1)
        bot.set_state(message.from_user.id,MainStates.problem_types , message.chat.id)
    else:
        bot.send_message(message.from_user.id, "Напишите один из предложенных вам вариантов")
        bot.set_state(message.from_user.id, MainStates.inequation_subtypes, message.chat.id)
@bot.message_handler(state=InEquation_Substypes.Сubic_inequation)
def Сubic_inequation_get_coifecents(message):
    message.text = message.text.split(' ')
    znak = str(message.text[4])
    message.text.pop(4)
    fraction(message.text)
    message.text.append(znak)
    if len(message.text) == 5:
        a = message.text[0]  # первый элемент списка
        b = message.text[1]  # второй элемент списка
        c = message.text[2]  # третий элемент списка
        d = message.text[3]  # четвёртый элемент списка
        p = (3 * a * c - b * 2) / (3 * a * 2)
        q = (2 * b * 3 - 9 * a * b * c + 27 * a *2*d) / (27 * a * 3)
        D = (p / 3) *3 + (q / 2) * 2
        if D > 0.000000000000000001:
            n = ((-q / 2) + ((D)*  0.5)) * (1 / 3)
            m = ((-q / 2) - ((D) * 0.5)) * (1 / 3)
            y1 = n + m
            y2 = -(n + m) / (2) - ((n - m) / (2)) * math.sqrt(3)
            y3 = -(n + m) / (2) + ((n - m) / (2)) * math.sqrt(3)
            x1 = y1 - (b) / (3 * a)
            x2 = y2 - (b) / (3 * a)
            x3 = y3 - (b) / (3 * a)
            x1,x2,x3 = sorted([x1,x2,x3])
            if znak == '>':
                bot.send_message(message.from_user.id,'x ∈ ('+str(x1)+';'+str(x2)+') ∪ ('+str(x3)+'; + ∞ )')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)
            elif znak == '>=':
                bot.send_message(message.from_user.id,'x ∈ ['+str(x1)+ ';'+str(x2)+ '] ∪ ['+str(x3)+ '; + ∞ )')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)
            elif znak == '<':
                bot.send_message(message.from_user.id,'x ∈ (- ∞ ;'+str(x1)+') ∪ ('+str(x2)+';'+str(x3)+')')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)
            elif znak == '<=':
                bot.send_message(message.from_user.id,'x ∈ (- ∞ ;'+str(x1)+ '] ∪ ['+str(x2)+ ';'+str(x3)+ ']')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)

        elif D==0:
            n = m = ((q / 2) * (1 / 3)) * (-1)
            y1 = n + m
            y2 = -(n + m) / (2) - ((n - m) / (2)) * math.sqrt(3)
            y3 = -(n + m) / (2) + ((n - m) / (2)) * math.sqrt(3)
            x1 = y1 - (b) / (3 * a)
            x2 = y2 - (b) / (3 * a)
            x3 = y3 - (b) / (3 * a)
            x1,x2,x3 = sorted([x1, x2, x3])
            if znak == '>':
                bot.send_message(message.from_user.id,'x ∈ ('+str(x1)+';'+str(x2)+') ∪ ('+str(x3)+'; + ∞ )')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)
            elif znak == '>=':
                bot.send_message(message.from_user.id,'x ∈ ['+str(x1)+ ';'+str(x2)+ '] ∪ ['+str(x3)+ '; + ∞ )')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)
            elif znak == '<':
                bot.send_message(message.from_user.id,'x ∈ (- ∞ ;'+str(x1)+') ∪ ('+str(x2)+';'+str(x3)+')')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)
            elif znak == '<=':
                bot.send_message(message.from_user.id,'x ∈ (- ∞ ;'+str(x1)+ '] ∪ ['+str(x2)+ ';'+str(x3)+ ']')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)


        elif D < 0 :
            n = ((-q / 2) - ((D) * 0.5)) * (1 / 3)
            m = ((-q / 2) + ((D)  *0.5))  *(1 / 3)
            y1 = n + m
            y2 = -(n + m) / (2) - ((n - m) / (2)) * math.sqrt(3)
            y3 = -(n + m) / (2) + ((n - m) / (2)) * math.sqrt(3)
            x1 = y1 - (b) / (3 * a)
            x2 = y2 - (b) / (3 * a)
            x3 = y3 - (b) / (3 * a)
            x1, x2, x3 =sorted([x1, x2, x3])

            if znak == '>':
                bot.send_message(message.from_user.id,'x ∈ ('+str(x1)+';'+str(x2)+') ∪ ('+str(x3)+'; + ∞ )')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)
            elif znak == '>=':
                bot.send_message(message.from_user.id,'x ∈ ['+str(x1)+ ';'+str(x2)+ '] ∪ ['+str(x3)+ '; + ∞ )')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)
            elif znak == '<':
                bot.send_message(message.from_user.id,'x ∈ (- ∞ ;'+str(x1)+') ∪ ('+str(x2)+';'+str(x3)+')')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)
            elif znak == '<=':
                bot.send_message(message.from_user.id,'x ∈ (- ∞ ;'+str(x1)+ '] ∪ ['+str(x2)+ ';'+str(x3)+ ']')
                bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                bot.send_message(message.from_user.id,
                                 "Для продолжения работы бота отправьте слово 'Привет' "
                                 , reply_markup=markup)
    elif len(message.text) < 5:
        bot.send_message(message.from_user.id, "Введите запрашиваемое количество переменных")
        bot.set_state(message.from_user.id, InEquation_Substypes.Сubic_inequation, message.chat.id)
    else:
        bot.send_message(message.from_user.id, "Введите коэффициенты по условию")
        bot.set_state(message.from_user.id, InEquation_Substypes.Сubic_inequation, message.chat.id)



@bot.message_handler(state=MainStates.equation_subtypes)
def equation_subtypes(message):
    if message.text =="Квадратное":
        bot.send_photo(message.chat.id, photo=open('/home/opc/pyth/photos/item1.jpg', 'rb'))
        bot.send_message(message.from_user.id, "Введите коэффициенты A B C через пробел")
        bot.set_state(message.from_user.id, Equation_Substypes.Quadratic_equation, message.chat.id)
    elif message.text == "Кубическое":
        bot.send_photo(message.chat.id, photo=open('/home/opc/pyth/photos/item2.jpg', 'rb'))
        bot.send_message(message.from_user.id, "Введите коэффициенты A B C D через пробел")
        bot.set_state(message.from_user.id, Equation_Substypes.Сubic_equation, message.chat.id)
    elif message.text == "Биквадратное":
        bot.send_photo(message.chat.id, photo=open('/home/opc/pyth/photos/item3.jpg', 'rb'))
        bot.send_message(message.from_user.id, "Введите коэффициенты A B C через пробел")
        bot.set_state(message.from_user.id, Equation_Substypes.Biquadratic_equation, message.chat.id)
    elif message.text == "Возвратное 4 степени":
        bot.send_photo(message.chat.id, photo=open('/home/opc/pyth/photos/item4.jpg', 'rb'))
        bot.send_message(message.from_user.id, "Введите коэффициенты A B C через пробел")
        bot.set_state(message.from_user.id, Equation_Substypes.Return_equation, message.chat.id)
    elif message.text == "Вернуться назад":
        bot.send_message(message.from_user.id, "Выберите,что решить из списка:\n" " 1.Уравнения\n"
                                               " 2.Неравенство\n"
                         "3. Схема Горнера\n",reply_markup=markup1)
        bot.set_state(message.from_user.id, MainStates.problem_types, message.chat.id)
    else:
        bot.send_message(message.from_user.id, "Напишите один из предложенных вам вариантов")
        bot.set_state(message.from_user.id, MainStates.equation_subtypes, message.chat.id)
@bot.message_handler(state=Equation_Substypes.Return_equation)
def Equation_Substypes_Return_equation(message):
 message.text = message.text.split(' ')
 fraction(message.text)
 if len(message.text) == 3:
     a = message.text[0]  # первый элемент списка
     b = message.text[1]  # второй элемент списка
     c = message.text[2]  # третий элемент списка
     c1 = c - (2 * a)
     D = b ** 2 - 4 * a * c1
     if D >= 0:
         t1 = (-b - math.sqrt(D)) / (2 * a)
         t2 = (-b + math.sqrt(D)) / (2 * a)
         D1 = t1 ** 2 - 4
         D2 = t2 ** 2 - 4
         if (D1 >= 0) and (D2 >= 0):
             x1 = (-t1 - math.sqrt(D1)) / (2)
             x2 = (-t1 + math.sqrt(D1)) / (2)
             x3 = (-t2 - math.sqrt(D2)) / (2)
             x4 = (-t2 + math.sqrt(D2)) / (2)
             bot.send_message(message.from_user.id,
                              "Первый корень равен: " + str(x1.real) + "\nВторой корень равен: " + str(x2)
                              + "\nТретий корень равен: " + str(x3) + "\nЧетвёртый корень равен: " + str(x4))
             bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

             bot.send_message(message.from_user.id,
                              "Для продолжения работы бота отправьте слово 'Привет' "
                              , reply_markup=markup)
         elif (D1 < 0) and (D2 < 0):
             bot.send_message(message.from_user.id, "Нет действительных корней")
             bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

             bot.send_message(message.from_user.id,
                              "Для продолжения работы бота отправьте слово 'Привет' "
                              , reply_markup=markup)
         elif (D1 >= 0) and (D2 < 0):
             x1 = (-t1 - math.sqrt(D1)) / (2)
             x2 = (-t1 + math.sqrt(D1)) / (2)
             bot.send_message(message.from_user.id,
                              "Первый корень равен: " + str(x1.real) + "\nВторой корень равен: " + str(x2))
             bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

             bot.send_message(message.from_user.id,
                              "Для продолжения работы бота отправьте слово 'Привет' "
                              , reply_markup=markup)
         elif (D2 >= 0) and (D1 < 0):
             x3 = (t2 - math.sqrt(D2)) / (2)
             x4 = (t2 + math.sqrt(D2)) / (2)
             bot.send_message(message.from_user.id,
                               "Третий корень равен: " + str(x3) + "\nЧетвёртый корень равен: " + str(x4))
             bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

             bot.send_message(message.from_user.id,
                              "Для продолжения работы бота отправьте слово 'Привет' "
                              , reply_markup=markup)
         elif D < 0:
             bot.send_message(message.from_user.id, "Нет действительных корней")
             bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

             bot.send_message(message.from_user.id,
                              "Для продолжения работы бота отправьте слово 'Привет' "
                              , reply_markup=markup)
     else:
         bot.send_message(message.from_user.id,
                          'Дискриминант меньше 0\n'"Выберите,что решить из списка:\n" " 1.Уравнения\n"
                          " 2.Неравенство\n"
                          "3. Схема Горнера\n",reply_markup=markup1)
         bot.set_state(message.from_user.id, MainStates.problem_types, message.chat.id)
 elif len(message.text) < 3:
     bot.send_message(message.from_user.id, "Введите запрашиваемое количество переменных")
     bot.set_state(message.from_user.id, Equation_Substypes.Return_equation, message.chat.id)
 else:
     bot.send_message(message.from_user.id, "Введите коэффициенты по условию")
     bot.set_state(message.from_user.id, Equation_Substypes.Return_equation, message.chat.id)







@bot.message_handler(state=Equation_Substypes.Biquadratic_equation)
def Equation_Substypes_Biquadratic_equation(message):
 message.text = message.text.split(' ')
 fraction(message.text)
 if len(message.text) == 3:
    a = message.text[0]  # первый элемент списка
    b = message.text[1]  # второй элемент списка
    c = message.text[2]  # третий элемент списка
    D = b ** 2 - 4 * a * c
    if D >= 0:
        t1 = (-b - math.sqrt(D)) / (2 * a)
        t2 = (-b + math.sqrt(D)) / (2 * a)
        print(t1,t2)
        if (t1 >= 0) and (t2 < 0):
            x1 = math.sqrt(t1)
            x3 = -(math.sqrt(t1))
            bot.send_message(message.from_user.id,
                             "Первый корень равен: " + str(x1)
                             + "\nТретий корень равен: " + str(x3))
            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

            bot.send_message(message.from_user.id,
                             "Для продолжения работы бота отправьте слово 'Привет' "
                             , reply_markup=markup)
        elif (t2 >= 0) and (t1 < 0):
            x2 = math.sqrt(t2)
            x4 = -(math.sqrt(t2))
            bot.send_message(message.from_user.id,
                              "Второй корень равен: " + str(x2)
                             + "\nЧетвёртый корень равен: " + str(x4))
            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

            bot.send_message(message.from_user.id,
                             "Для продолжения работы бота отправьте слово 'Привет' "
                             , reply_markup=markup)
        elif (t1 >= 0) and (t2 >= 0):
            x1 = math.sqrt(t1)
            x2 = math.sqrt(t2)
            x3 = -(math.sqrt(t1))
            x4 = -(math.sqrt(t2))
            bot.send_message(message.from_user.id,
                             "Первый корень равен: " + str(x1) + "\nВторой корень равен: " + str(x2)
                             + "\nТретий корень равен: " + str(x3)+ "\nЧетвёртый корень равен: " + str(x4))
            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

            bot.send_message(message.from_user.id,
                             "Для продолжения работы бота отправьте слово 'Привет' "
                             , reply_markup=markup)
        else:
            bot.send_message(message.from_user.id,"Левая часть всегда положительна,утверждение ложно для любого значения x")
            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

            bot.send_message(message.from_user.id,
                             "Для продолжения работы бота отправьте слово 'Привет' "
                             , reply_markup=markup)

    else:
        bot.send_message(message.from_user.id,
                         'Дискриминант меньше 0\n'"Выберите,что решить из списка:\n" " 1.Уравнения\n"
                         " 2.Неравенство\n"
                         "3. Схема Горнера\n",reply_markup=markup1)
        bot.set_state(message.from_user.id, MainStates.problem_types, message.chat.id)
 elif len(message.text) < 3:
     bot.send_message(message.from_user.id, "Введите запрашиваемое количество переменных")
     bot.set_state(message.from_user.id, Equation_Substypes.Biquadratic_equation, message.chat.id)
 else:
     bot.send_message(message.from_user.id, "Введите коэффициенты по условию")
     bot.set_state(message.from_user.id, Equation_Substypes.Biquadratic_equation, message.chat.id)



@bot.message_handler(state=Equation_Substypes.Quadratic_equation)
def Quadratic_equation_get_coifecents(message):
    message.text = message.text.split(' ')
    fraction(message.text)
    if len(message.text) == 3:
        A = message.text[0]  # первый элемент списка
        B = message.text[1]  # второй элемент списка
        C = message.text[2]  # третий элемент списка
        D = B ** 2 - 4 * A * C
        if D >= 0:
            x1 = (-B - math.sqrt(D)) / (2 * A)
            x2 = (-B + math.sqrt(D)) / (2 * A)
            bot.send_message(message.from_user.id,
                             "Первый корень равен: " + str(x1) + "\nВторой корень равен: " + str(x2))
            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)

            bot.send_message(message.from_user.id,
                             "Для продолжения работы бота отправьте слово 'Привет' "
                             , reply_markup=markup)
        elif D < 0:
            bot.send_message(message.from_user.id, "Дискриминант меньше 0\n" "Выберите,что решить из списка:\n" " 1.Уравнения\n"
                                                   " 2.Неравенство\n"
                             "3. Схема Горнера\n",reply_markup=markup1)
            bot.set_state(message.from_user.id, MainStates.problem_types, message.chat.id)
    elif len(message.text) < 3:
        bot.send_message(message.from_user.id, "Введите запрашиваемое количество переменных")
        bot.set_state(message.from_user.id, Equation_Substypes.Quadratic_equation, message.chat.id)
    else:
        bot.send_message(message.from_user.id, "Введите коэффициенты по условию")
        bot.set_state(message.from_user.id, Equation_Substypes.Quadratic_equation, message.chat.id)


@bot.message_handler(state=Equation_Substypes.Сubic_equation)
def Сubic_equation_get_coifecents(message):
    message.text = message.text.split(' ')
    fraction(message.text)
    if len(message.text) == 4:
        a = message.text[0]  # первый элемент списка
        b = message.text[1]  # второй элемент списка
        c = message.text[2]  # третий элемент списка
        d = message.text[3]   # четвёртый элемент списка
        p = (3 * a * c - b ** 2) / (3 * a ** 2)
        q = (2 * b ** 3 - 9 * a * b * c + 27 * a ** 2 * d) / (27 * a ** 3)
        D = (p / 3) ** 3 + (q / 2) ** 2
        if D > 0.000000000000000001:
            n = ((-q / 2) + ((D) ** 0.5)) ** (1 / 3)
            m = ((-q / 2) - ((D) ** 0.5)) ** (1 / 3)
            y1 = n + m
            y2 = -(n + m) / (2) - ((n - m) / (2)) * math.sqrt(3)
            y3 = -(n + m) / (2) + ((n - m) / (2)) * math.sqrt(3)
            x1 = y1 - (b) / (3 * a)
            x2 = y2 - (b) / (3 * a)
            x3 = y3 - (b) / (3 * a)
            bot.send_message(message.from_user.id,
                             "Первый корень равен: " + str(x1) + "\nВторой корень равен: " + str(x2)
                             + "\nТретий корень равен: " + str(x3))
            bot.send_message(message.from_user.id,
                             "Примечание: Чаще всего в ответе вы будете видеть сумму или разность обычного числа с "
                             "комплексным, "
                             "\nв этом случае вы должны ,не смотря на на j сделать нужное вычисление и тогда вы "
                             "получите ваши корни.")
            bot.send_message(message.from_user.id,
                             "Для продолжения работы бота отправьте слово 'Привет' "
                             , reply_markup=markup)
            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)


        elif (D >= 0) and (D <= 0.000000000000000001):
            n = m = ((q / 2) ** (1 / 3)) * (-1)
            y1 = n + m
            y2 = -(n + m) / (2) - ((n - m) / (2)) * math.sqrt(3)
            y3 = -(n + m) / (2) + ((n - m) / (2)) * math.sqrt(3)
            x1 = y1 - (b) / (3 * a)
            x2 = y2 - (b) / (3 * a)
            x3 = y3 - (b) / (3 * a)
            bot.send_message(message.from_user.id,
                             "Первый корень равен: " + str(x1) + "\nВторой корень равен: " + str(x2)
                             + "\nТретий корень равен: " + str(x3))
            bot.send_message(message.from_user.id,
                             "Примечание: Чаще всего в ответе вы будете видеть сумму или разность обычного числа с "
                             "комплексным, "
                             "\nв этом случае вы должны ,не смотря на на j сделать нужное вычисление и тогда вы "
                             "получите ваши корни.")
            bot.send_message(message.from_user.id,
                             "Для продолжения работы бота отправьте слово 'Привет' "
                             , reply_markup=markup)

            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)




        elif D < 0:
            n = ((-q / 2) - ((D) ** 0.5)) ** (1 / 3)
            m = ((-q / 2) + ((D) ** 0.5)) ** (1 / 3)
            y1 = n + m
            y2 = -(n + m) / (2) - ((n - m) / (2)) * math.sqrt(3)
            y3 = -(n + m) / (2) + ((n - m) / (2)) * math.sqrt(3)
            x1 = y1 - (b) / (3 * a)
            x2 = y2 - (b) / (3 * a)
            x3 = y3 - (b) / (3 * a)
            bot.send_message(message.from_user.id,
                             "Первый корень равен: " + str(x1.real) + "\nВторой корень равен: " + str(x2)
                             + "\nТретий корень равен: " + str(x3))
            bot.send_message(message.from_user.id,
                             "Примечание: Чаще всего в ответе вы будете видеть сумму или разность обычного числа с "
                             "комплексным, "
                             "\nв этом случае вы должны ,не смотря на на j сделать нужное вычисление и тогда вы "
                             "получите ваши корни.")
            bot.send_message(message.from_user.id,
                             "Для продолжения работы бота отправьте слово 'Привет' "
                             , reply_markup=markup)
            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)



            bot.set_state(message.from_user.id, MainStates.problem_types, message.chat.id)
    elif len(message.text) < 4:
        bot.send_message(message.from_user.id, "Введите запрашиваемое количество переменных")
        bot.set_state(message.from_user.id, Equation_Substypes.Сubic_equation, message.chat.id)
    else:
        bot.send_message(message.from_user.id, "Введите коэффициенты по условию")
        bot.set_state(message.from_user.id, Equation_Substypes.Сubic_equation, message.chat.id)


@bot.message_handler(state=InEquation_Substypes.Quadratic_inequation)
def inequation_subtypes_get_coifecents(message):
    message.text = message.text.split(' ')
    znak = str(message.text[3])
    message.text.pop(3)
    fraction(message.text)
    message.text.append(znak)
    if len(message.text) == 4:
        a = message.text[0]  # первый элемент списка
        b = message.text[1]  # второй элемент списка
        c = message.text[2]  # третий элемент списка

        if a == 0:
            c = -c
            if znak == '>' or znak == '>=':
                if b == 0 and c < 0:
                    bot.send_message(message.from_user.id, '(-∞ ; + ∞)')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                else:
                    if b == 0 and c >= 0:
                        bot.send_message(message.from_user.id, 'нет решений')
                        bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                        bot.send_message(message.from_user.id,
                                         "Для продолжения работы бота отправьте слово 'Привет' "
                                         , reply_markup=markup)
                    else:
                        x0 = c / b
                        if b > 0 and znak == '>':
                            bot.send_message(message.from_user.id, '('+ str(x0)+ ' ;+ ∞)')
                            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                            bot.send_message(message.from_user.id,
                                             "Для продолжения работы бота отправьте слово 'Привет' "
                                             , reply_markup=markup)
                        elif b > 0 and znak == '>=':
                            bot.send_message(message.from_user.id, '['+ str(x0)+ ' ;+ ∞)')
                            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                            bot.send_message(message.from_user.id,
                                             "Для продолжения работы бота отправьте слово 'Привет' "
                                             , reply_markup=markup)
                        elif b < 0 and znak == '>':
                            bot.send_message(message.from_user.id, '( - ∞;'+ str(x0) + ')')
                            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                            bot.send_message(message.from_user.id,
                                             "Для продолжения работы бота отправьте слово 'Привет' "
                                             , reply_markup=markup)
                        elif b < 0 and znak == '>=':
                            bot.send_message(message.from_user.id, '( - ∞;'+ str(x0) +']')
                            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                            bot.send_message(message.from_user.id,
                                             "Для продолжения работы бота отправьте слово 'Привет' "
                                             , reply_markup=markup)
            else:
                if b == 0 and c < 0:
                    bot.send_message(message.from_user.id, 'нет решений')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                else:
                    if b == 0 and c >= 0:
                        bot.send_message(message.from_user.id, '(-∞ ; + ∞)')
                        bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                        bot.send_message(message.from_user.id,
                                         "Для продолжения работы бота отправьте слово 'Привет' "
                                         , reply_markup=markup)
                    else:
                        x0 = c / b
                        if b > 0 and znak == '<':
                            bot.send_message(message.from_user.id, '( - ∞;'+ str(x0)+ ')')
                            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                            bot.send_message(message.from_user.id,
                                             "Для продолжения работы бота отправьте слово 'Привет' "
                                             , reply_markup=markup)
                        elif b > 0 and znak == '<=':
                            bot.send_message(message.from_user.id, '( - ∞;'+ str(x0)+ ']')
                            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                            bot.send_message(message.from_user.id,
                                             "Для продолжения работы бота отправьте слово 'Привет' "
                                             , reply_markup=markup)
                        elif b < 0 and znak == '>':
                            bot.send_message(message.from_user.id, '('+str(x0)+ ' ;+ ∞)')
                            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                            bot.send_message(message.from_user.id,
                                             "Для продолжения работы бота отправьте слово 'Привет' "
                                             , reply_markup=markup)
                        elif b < 0 and znak == '<=':
                            bot.send_message(message.from_user.id, '['+ str(x0)+ ' ;+ ∞)')
                            bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                            bot.send_message(message.from_user.id,
                                             "Для продолжения работы бота отправьте слово 'Привет' "
                                             , reply_markup=markup)
        else:
            D = b ** 2 - 4 * a * c
            if D > 0:
                x1 = (-b + (D ** 0.5)) / (2 * a)
                x2 = (-b - (D ** 0.5)) / (2 * a)
                x01 = min(x1, x2)
                x02 = max(x1, x2)
                if a < 0 and znak == '>':
                    znak = '<'
                elif a < 0 and znak == '>=':
                    znak = '<='
                elif a < 0 and znak == '<':
                    znak = '>'
                elif a < 0 and znak == '<=':
                    znak = '>='
                if znak == '>':
                    bot.send_message(message.from_user.id, '(- ∞;'+ str(x01)+ ') ∪ ('+str(x02)+ '; + ∞)')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                elif znak == '>=':
                    bot.send_message(message.from_user.id, '(- ∞;'+ str(x01)+ '] ∪ ['+ str(x02)+ '; + ∞)')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                elif znak == '<':
                    bot.send_message(message.from_user.id, '('+ str(x01)+ ';'+ str(x02)+ ')')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                elif znak == '<=':
                    bot.send_message(message.from_user.id, '['+ str(x01)+ ';'+str(x02)+ ']')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
            elif D == 0:
                x0 = -b / 2 * a
                if znak == '>':
                    bot.send_message(message.from_user.id, '(- ∞;'+ str(x0)+ ') ∪ ('+ str(x0)+ ' ;+ ∞)')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                elif znak == '>=':
                    bot.send_message(message.from_user.id, '(-∞ ; + ∞)')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                elif znak == '<':
                    bot.send_message(message.from_user.id, 'решений  нет')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                elif znak == '<=':
                    bot.send_message(message.from_user.id, 'x ='+ str(x0))
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
            else:
                if a > 0 and (znak == '>' or znak == '>='):
                    bot.send_message(message.from_user.id, '(-∞ ; + ∞)')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                elif a > 0 and (znak == '<' or znak == '<='):
                    bot.send_message(message.from_user.id, 'нет решений')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                elif a < 0 and (znak == '<' or znak == '<='):
                    bot.send_message(message.from_user.id, '(-∞ ; + ∞)')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
                elif a < 0 and (znak == '>' or znak == '>='):
                    bot.send_message(message.from_user.id, 'нет решений')
                    bot.set_state(message.from_user.id, MainStates.start_state, message.chat.id)
                    bot.send_message(message.from_user.id,
                                     "Для продолжения работы бота отправьте слово 'Привет' "
                                     , reply_markup=markup)
    elif len(message.text) < 4:
        bot.send_message(message.from_user.id, "Введите запрашиваемое количество переменных")
        bot.set_state(message.from_user.id, MainStates.inequation_subtypes, message.chat.id)
    else:
        bot.send_message(message.from_user.id, "Введите коэффициенты по условию")
        bot.set_state(message.from_user.id, MainStates.inequation_subtypes, message.chat.id)



bot.add_custom_filter(custom_filters.StateFilter(bot))
bot.infinity_polling(skip_pending=True)
