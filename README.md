# manager_student
sql gui
تسک دوم : 

توسعه برنامه مدیریت دانشجویان
هدف:
ایجاد یک برنامه کاربردی ساده برای مدیریت دانشجویان با استفاده از زبان برنامه‌نویسی پایتون و پایگاه داده SQLite.
مراحل تسک:
طراحی پایگاه داده:

ایجاد یک جدول برای ذخیره اطلاعات دانشجویان (شناسه، نام، نام خانوادگی، سن، و ...).
تعیین یک کلید اصلی برای جلوگیری از تکرار اطلاعات.
اتصال به پایگاه داده:

استفاده از کد جلسه دوم برای ایجاد اتصال به پایگاه داده SQLite.
ایجاد واسط کاربری:

ایجاد یک واسط کاربری ساده با استفاده از کتابخانه‌های موجود (مثل Tkinter یا ipywidgets برای Google Colab).
امکان افزودن دانشجو، ویرایش اطلاعات و نمایش لیست دانشجویان.
نمایش اطلاعات:

نمایش لیست دانشجویان در واسط کاربری.
امکان نمایش جزئیات هر دانشجو به صورت جداگانه.
عملیات CRUD:

ایجاد فرم برای افزودن و ویرایش دانشجویان.
امکان حذف دانشجو از لیست.
آزمون و اصلاح:

انجام آزمون‌های مختلف برنامه.
اصلاح خطاها و بهبود عملکرد.
گزارش:

تهیه یک گزارش کوتاه که شامل توضیحاتی از اهداف برنامه، ساختار پایگاه داده، کد‌های اصلی و تصاویری از واسط کاربری باشد.
ارسال گزارش و کد‌ها به منظور ارزیابی.
جواب:
(برای اجابت به این تسک، می‌توانید از کد ارائه شده در تسک 1 و به تعداد کمی اصلاحات استفاده کنید. )
اطلاعات مدیریت دانشجویان را می‌توانید در یک پایگاه داده SQLite ذخیره کرده و یک واسط کاربری ساده برای نمایش و ویرایش اطلاعات ایجاد کنید.
بله، می‌توانید از کد زیر برای توسعه برنامه مدیریت دانشجویان با استفاده از پایگاه داده SQLite استفاده کنید. این کد به صورت ساده برای ایجاد یک جدول "students" در پایگاه داده و افزودن، نمایش و به‌روزرسانی اطلاعات دانشجویان طراحی شده است.
import sqlite3
# اتصال به پایگاه داده
conn = sqlite3.connect('students.db')
# ایجاد یک جدول برای ذخیره اطلاعات دانشجویان
conn.execute('''
    CREATE TABLE IF NOT EXISTS students (
        id INTEGER PRIMARY KEY,
        first_name TEXT NOT NULL,
        last_name TEXT NOT NULL,
        age INTEGER NOT NULL
    )
''')

# تعریف توابع CRUD

def add_student(first_name, last_name, age):
    conn.execute("INSERT INTO students (first_name, last_name, age) VALUES (?, ?, ?)", (first_name, last_name, age))
    conn.commit()
def get_students():
    cursor = conn.execute("SELECT * FROM students")
    return cursor.fetchall()
def update_student(student_id, first_name, last_name, age):
    conn.execute("UPDATE students SET first_name=?, last_name=?, age=? WHERE id=?", (first_name, last_name, age, student_id))
    conn.commit()
# افزودن چند دانشجو به عنوان نمونه
add_student('John', 'Doe', 22)
add_student('Jane', 'Smith', 25)

# نمایش لیست دانشجویان
students_list = get_students()
for student in students_list:
    print(student)
# به‌روزرسانی اطلاعات یک دانشجو
update_student(1, 'John', 'Updated Doe', 23)
# نمایش لیست دانشجویان پس از به‌روزرسانی
updated_students_list = get_students()
for student in updated_students_list:
    print(student)
# بستن اتصال
conn.close()
لطفاً توجه داشته باشید که این کد به عنوان یک مثال ساده طراحی شده است و می‌توانید آن را بر اساس نیازهای خود تغییر دهید. همچنین، می‌توانید از این کد به عنوان نقطه شروع برای توسعه برنامه مدیریت دانشجویان خود استفاده کنید.

در ادامه، یک کد کامل برای ایجاد جدول جدید و اضافه کردن دانشجوها به آن آورده شده است:
import sqlite3

# اتصال به پایگاه داده
conn = sqlite3.connect('students.db')

# حذف جدول اگر وجود داشته باشد
conn.execute('DROP TABLE IF EXISTS students')

# ایجاد یک جدول برای ذخیره اطلاعات دانشجویان
conn.execute('''
    CREATE TABLE students (
        id INTEGER PRIMARY KEY,
        first_name TEXT NOT NULL,
        last_name TEXT NOT NULL,
        age INTEGER NOT NULL,
        major TEXT NOT NULL
    )
''')

# تعریف توابع CRUD

def add_student(first_name, last_name, age, major):
    conn.execute("INSERT INTO students (first_name, last_name, age, major) VALUES (?, ?, ?, ?)", (first_name, last_name, age, major))
    conn.commit()

def get_students():
    cursor = conn.execute("SELECT * FROM students")
    return cursor.fetchall()

def update_student(student_id, first_name, last_name, age, major):
    conn.execute("UPDATE students SET first_name=?, last_name=?, age=?, major=? WHERE id=?", (first_name, last_name, age, major, student_id))
    conn.commit()

# افزودن چند دانشجو به عنوان نمونه
add_student('John', 'Doe', 22, 'Computer Science')
add_student('Jane', 'Smith', 25, 'Electrical Engineering')

# نمایش لیست دانشجویان
students_list = get_students()
for student in students_list:
    print(student)

# به‌روزرسانی اطلاعات یک دانشجو
update_student(1, 'John', 'Updated Doe', 23, 'Data Science')

# نمایش لیست دانشجویان پس از به‌روزرسانی
updated_students_list = get_students()
for student in updated_students_list:
    print(student)

# بستن اتصال
conn.close()
در اینجا ابتدا جدول را حذف کرده و سپس دوباره ایجاد می‌کنیم. 
 
ایجاد واسط کاربری:

ایجاد یک واسط کاربری ساده با استفاده از کتابخانه‌های موجود (مثل Tkinter یا ipywidgets برای Google Colab).
امکان افزودن دانشجو، ویرایش اطلاعات و نمایش لیست دانشجویان.
!pip install ipywidgets
!jupyter nbextension enable --py widgetsnbextension --sys-prefix
!jupyter nbextension enable --py widgetsnbextension --sys-prefix
!jupyter nbextension enable --py widgetsnbextension --sys-prefix


from ipywidgets import interact, widgets

class StudentManagementApp:
    def __init__(self):
        self.students = []

    def add_student(self, first_name, last_name, age, major):
        student_info = f"{first_name} {last_name}, Age: {age}, Major: {major}"
        self.students.append(student_info)

    def show_students(self):
        for student in self.students:
            print(student)

# ایجاد یک نمونه از کلاس
app = StudentManagementApp()

# تعریف ویجت‌ها
first_name_input = widgets.Text(description="First Name:")
last_name_input = widgets.Text(description="Last Name:")
age_input = widgets.IntText(description="Age:")
major_input = widgets.Text(description="Major:")
add_button = widgets.Button(description="Add Student")
show_button = widgets.Button(description="Show Students")

# تعریف توابع اضافه کردن دانشجو و نمایش دانشجوها
def add_student(event):
    app.add_student(first_name_input.value, last_name_input.value, age_input.value, major_input.value)
    clear_inputs()

def show_students(event):
    app.show_students()

def clear_inputs():
    first_name_input.value = ""
    last_name_input.value = ""
    age_input.value = 0
    major_input.value = ""

# اتصال توابع به دکمه‌ها
add_button.on_click(add_student)
show_button.on_click(show_students)

# نمایش ویجت‌ها
display(first_name_input)
display(last_name_input)
display(age_input)
display(major_input)
display(add_button)
display(show_button)

 


