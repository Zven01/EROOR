# EROOR
import time

class FreeFireFriendBot:
    def __init__(self):
        self.commands = {
            "/help": "عرض جميع الأوامر المتاحة",
            "/spam": "إرسال طلبات إضافة فريق بشكل متكرر",
            "/stop": "إيقاف الأمر الحالي"
        }
        self.is_spamming = False
    
    def handle_command(self, command):
        if command == "/help":
            return self.show_help()
        elif command == "/spam":
            self.is_spamming = True
            return self.start_spam()
        elif command == "/stop":
            self.is_spamming = False
            return "تم إيقاف الأمر الحالي."
        else:
            return "أمر غير معروف. اكتب /help لرؤية الأوامر المتاحة."
    
    def show_help(self):
        help_text = "الأوامر المتاحة:\n"
        for cmd, desc in self.commands.items():
            help_text += f"{cmd}: {desc}\n"
        return help_text
    
    def start_spam(self):
        counter = 0
        while self.is_spamming and counter < 10:  # الحد الأقصى 10 طلبات لتجنب الحظر
            print("تم إرسال طلب إضافة فريق للاعب")
            time.sleep(1)  # تأخير 1 ثانية بين كل طلب
            counter += 1
        self.is_spamming = False
        return "تم إرسال طلبات إضافة فريق للاعب"

# طريقة الاستخدام
bot = FreeFireFriendBot()

while True:
    user_input = input("أدخل الأمر: ")
    if user_input.lower() == "exit":
        break
    response = bot.handle_command(user_input)
    print(response)
