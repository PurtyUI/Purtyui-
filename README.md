
# 🎓 ระบบลงทะเบียนนักศึกษา (Student Registration System)

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## 📋 สารบัญ
- [📌 ภาพรวมโครงการ](#-ภาพรวมโครงการ)
- [✨ คุณสมบัติหลัก](#-คุณสมบัติหลัก)
- [🛠 เทคโนโลยีที่ใช้](#-เทคโนโลยีที่ใช้)
- [📦 ความต้องการของระบบ](#-ความต้องการของระบบ)
- [🚀 การติดตั้งและใช้งาน (Step-by-step)](#-การติดตั้งและใช้งาน-step-by-step)
- [📁 โครงสร้างโปรเจกต์](#-โครงสร้างโปรเจกต์)
- [📑 คำอธิบายโค้ดหลัก (สำคัญ)](#-คำอธิบายโค้ดหลัก-สำคัญ)
- [💡 อธิบายเทมเพลต HTML ทั้งหมด](#-อธิบายเทมเพลต-html-ทั้งหมด)
- [🔧 Dev Tools แนะนำสำหรับพัฒนา](#-dev-tools-แนะนำสำหรับพัฒนา)
- [🎯 ตัวอย่างการใช้งานจริง (Use Case)](#-ตัวอย่างการใช้งานจริง-use-case)
- [🧩 การปรับแต่งและขยาย](#-การปรับแต่งและขยาย)
- [🚧 การดูแลรักษาและการสนับสนุน](#-การดูแลรักษาและการสนับสนุน)
- [🤝 การมีส่วนร่วมในโครงการ](#-การมีส่วนร่วมในโครงการ)
- [📄 ใบอนุญาต](#-ใบอนุญาต)
- [📞 ติดต่อ](#-ติดต่อ)

---

## 📌 ภาพรวมโครงการ
ระบบนี้พัฒนาเพื่อให้การจัดการข้อมูลนักศึกษาในสถานศึกษาเป็นไปอย่างสะดวกผ่านเว็บแอปพลิเคชัน  
สามารถลงทะเบียน, อัปโหลดรูป, ค้นหา, แก้ไข และลบนักศึกษาได้

## ตัวอย่างหน้าเว็ปไซต์
### หน้าแรก (Home page)
![หน้าแรก](image/หน้าหลักเว็บ.png.png)
### เเสดงรายชื่อนักศึกษา (Student list)
![เเสดงรายชื่อนักศึกษา](image/เเสดงรายชื่อนักศึกษา.png)
### เเก้ไขลบ(Edit/Delete)
![เเก้ไขลบ](image/เเก้ไขลบ.png.png)
### ยืนยันการลบ(Confirm Delete)
![ยืนยันการลบ](image/ยืนยันการลบ.png.png)

---

## ✨ คุณสมบัติหลัก
- ระบบ CRUD (Create, Read, Update, Delete)
- ฟอร์มรับข้อมูลแบบทันสมัย
- รองรับการอัปโหลดรูปภาพและแสดงภาพ
- ระบบค้นหาแบบ partial matching
- ใช้ Bootstrap 5 UI/UX

---

## 🛠 เทคโนโลยีที่ใช้
- Django 4.x (Python Web Framework)
- SQLite3 (ฐานข้อมูลในตัว)
- Bootstrap 5 (ออกแบบหน้าเว็บ)
- HTML5, CSS3, JavaScript (พื้นฐาน)
- VS Code / GitHub (แนะนำ)

---

## 📦 ความต้องการของระบบ
- Python >= 3.10
- Django >= 4.2
- pip (Python package manager)
- ระบบปฏิบัติการ: Windows / macOS / Linux

---

## 🚀 การติดตั้งและใช้งาน (Step-by-step)

### 1. ดาวน์โหลดหรือโคลนโปรเจกต์
```bash
git clone https://github.com/yourusername/student_register.git
cd student_register
```

### 2. สร้าง virtual environment
```bash
python -m venv venv
venv\Scripts\activate  # Windows
# หรือ
source venv/bin/activate  # Mac/Linux
```

### 3. ติดตั้ง Django
```bash
pip install django
```

### 4. รัน migration และ server
```bash
python manage.py migrate
python manage.py runserver
```

---

## 📁 โครงสร้างโปรเจกต์
```plaintext
student_register/
├── manage.py
├── db.sqlite3
├── student_register/
│   ├── settings.py
│   ├── urls.py
│   └── ...
├── students/
│   ├── models.py
│   ├── views.py
│   ├── forms.py
│   ├── urls.py
├── templates/
│   ├── base.html
│   ├── student_form.html
│   └── student_list.html
└── media/
    └── student_images/
```

---

## 📑 คำอธิบายโค้ดหลัก (สำคัญ)

### `models.py`
```python
class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    image = models.ImageField(upload_to='student_images/')
```
- ใช้สร้างตารางข้อมูลนักศึกษาในฐานข้อมูล
- `image` จะถูกเก็บไว้ในโฟลเดอร์ `media/student_images`

---

### `forms.py`
```python
class StudentForm(forms.ModelForm):
    class Meta:
        model = Student
        fields = ['name', 'email', 'image']
```
- ฟอร์มสำหรับรับค่าจากผู้ใช้ในหน้าเว็บ
- ผูกกับ Model โดยอัตโนมัติ

---

### `views.py`
```python
def student_list(request):
    query = request.GET.get('q')
    students = Student.objects.filter(name__icontains=query) if query else Student.objects.all()
    return render(request, 'student_list.html', {'students': students})
```
- แสดงรายการนักศึกษาทั้งหมด
- รองรับการค้นหาชื่อ

---

### `urls.py`
```python
urlpatterns = [
    path('', views.student_list, name='student_list'),
    path('add/', views.student_create, name='student_create'),
    ...
]
```
- กำหนด route สำหรับหน้าเว็บต่าง ๆ

---

## 💡 อธิบายเทมเพลต HTML ทั้งหมด

### `base.html`
- โครงหน้าเว็บหลักที่หน้าอื่น ๆ จะสืบทอด
- มี Navbar และส่วน `block content` สำหรับใส่เนื้อหาจากแต่ละหน้า

### `student_form.html`
- ฟอร์ม HTML สำหรับกรอกข้อมูลนักศึกษา
- ใช้ Bootstrap ทำให้ UI สวยงาม

### `student_list.html`
- แสดงตารางข้อมูลนักศึกษา
- มีช่องค้นหา และปุ่มแก้ไข/ลบ

---

## 🔧 Dev Tools แนะนำสำหรับพัฒนา
- ✅ [VS Code](https://code.visualstudio.com/)
- ✅ [GitHub Desktop](https://desktop.github.com/)
- ✅ [Postman](https://www.postman.com/) (หากขยายไปใช้ API)
- ✅ [SQLite Browser](https://sqlitebrowser.org/) (ดูฐานข้อมูล)

---

## 🎯 ตัวอย่างการใช้งานจริง (Use Case)
- โครงการนักศึกษา
- เว็บระบบหลังบ้านโรงเรียน
- ระบบรับสมัครนักศึกษาใหม่
- ใช้ฝึกงานด้าน Django/Full Stack

---

## 🧩 การปรับแต่งและขยาย
- เพิ่มระบบ login/logout
- ใช้ PostgreSQL แทน SQLite
- อัปเกรด Bootstrap เป็นเวอร์ชันล่าสุด
- เพิ่ม pagination, export PDF หรือ Excel

---

## 🚧 การดูแลรักษาและการสนับสนุน
- อัปเดต Django เวอร์ชันล่าสุดเสมอ
- สำรองฐานข้อมูลหากใช้งานจริง
- ปรับปรุง UI ให้เหมาะกับมือถือ (responsive)

---

## 🤝 การมีส่วนร่วมในโครงการ
- Fork Repo และสร้าง Branch ของคุณเอง
- Pull Request ยินดีต้อนรับ!
- เปิด Issue หากพบปัญหา

---

## 📄 ใบอนุญาต
เผยแพร่ภายใต้ MIT License – นำไปใช้ต่อ/ดัดแปลงได้

---

## 📞 ติดต่อ
ผู้พัฒนา: 
- วงศกร หวลมานพ
- อกฤษณ์ นารัง
- สิรฐากร กาญจนเสถียร
  
---   

