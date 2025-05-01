🎓 ระบบลงทะเบียนนักศึกษา (Student Registration System)
Version License

📋 สารบัญ
📌 ภาพรวมโครงการ
✨ คุณสมบัติหลัก
🛠 เทคโนโลยีที่ใช้
📦 ความต้องการของระบบ
🚀 การติดตั้งและใช้งาน (Step-by-step)
📁 โครงสร้างโปรเจกต์
📑 คำอธิบายโค้ดหลัก (สำคัญ)
💡 อธิบายเทมเพลต HTML ทั้งหมด
🔧 Dev Tools แนะนำสำหรับพัฒนา
🎯 ตัวอย่างการใช้งานจริง (Use Case)
🧩 การปรับแต่งและขยาย
🚧 การดูแลรักษาและการสนับสนุน
🤝 การมีส่วนร่วมในโครงการ
📄 ใบอนุญาต
📞 ติดต่อ

📌 ภาพรวมโครงการ
ระบบนี้พัฒนาเพื่อให้การจัดการข้อมูลนักศึกษาในสถานศึกษาเป็นไปอย่างสะดวกผ่านเว็บแอปพลิเคชัน
สามารถลงทะเบียน, อัปโหลดรูป, ค้นหา, แก้ไข และลบนักศึกษาได้

ตัวอย่างหน้าเว็ปไซต์
หน้าแรก (Home page)
![17460997645556080343671535997979](https://github.com/user-attachments/assets/1b9add8e-4b93-489d-b925-82953f9d8ae2)

เเสดงรายชื่อนักศึกษา (Student list)
![17460997879675150315442381522596](https://github.com/user-attachments/assets/c82c830c-ee7b-48c4-9bf3-03762b2accc9)

เเก้ไขลบ(Edit/Delete)
![17460998200915031253802595793234](https://github.com/user-attachments/assets/2973b515-01ae-43d0-9aed-89fbffd3b5cb)

ยืนยันการลบ(Confirm Delete)
![17460998398143808096080291099112](https://github.com/user-attachments/assets/8b9e7f57-2bf3-4240-bf38-5822ca0d8341)

✨ คุณสมบัติหลัก
ระบบ CRUD (Create, Read, Update, Delete)
ฟอร์มรับข้อมูลแบบทันสมัย
รองรับการอัปโหลดรูปภาพและแสดงภาพ
ระบบค้นหาแบบ partial matching
ใช้ Bootstrap 5 UI/UX
🛠 เทคโนโลยีที่ใช้
Django 4.x (Python Web Framework)
SQLite3 (ฐานข้อมูลในตัว)
Bootstrap 5 (ออกแบบหน้าเว็บ)
HTML5, CSS3, JavaScript (พื้นฐาน)
VS Code / GitHub (แนะนำ)
📦 ความต้องการของระบบ
Python >= 3.10
Django >= 4.2
pip (Python package manager)
ระบบปฏิบัติการ: Windows / macOS / Linux
🚀 การติดตั้งและใช้งาน (Step-by-step)
1. ดาวน์โหลดหรือโคลนโปรเจกต์
https://github.com/yourusername/student_register.git
2. สร้าง virtual environment
python -m venv venv
venv\Scripts\activate  # Windows
# หรือ
source venv/bin/activate  # Mac/Linux
3. ติดตั้ง Django
pip install django
4. รัน migration และ server
python manage.py migrate
python manage.py runserver
📁 โครงสร้างโปรเจกต์
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
📑 คำอธิบายโค้ดหลัก (สำคัญ)
models.py
class Student(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    image = models.ImageField(upload_to='student_images/')
ใช้สร้างตารางข้อมูลนักศึกษาในฐานข้อมูล
image จะถูกเก็บไว้ในโฟลเดอร์ media/student_images
forms.py
class StudentForm(forms.ModelForm):
    class Meta:
        model = Student
        fields = ['name', 'email', 'image']
ฟอร์มสำหรับรับค่าจากผู้ใช้ในหน้าเว็บ
ผูกกับ Model โดยอัตโนมัติ
views.py
def student_list(request):
    query = request.GET.get('q')
    students = Student.objects.filter(name__icontains=query) if query else Student.objects.all()
    return render(request, 'student_list.html', {'students': students})
แสดงรายการนักศึกษาทั้งหมด
รองรับการค้นหาชื่อ
urls.py
urlpatterns = [
    path('', views.student_list, name='student_list'),
    path('add/', views.student_create, name='student_create'),
    ...
]
กำหนด route สำหรับหน้าเว็บต่าง ๆ
💡 อธิบายเทมเพลต HTML ทั้งหมด
base.html
โครงหน้าเว็บหลักที่หน้าอื่น ๆ จะสืบทอด
มี Navbar และส่วน block content สำหรับใส่เนื้อหาจากแต่ละหน้า
student_form.html
ฟอร์ม HTML สำหรับกรอกข้อมูลนักศึกษา
ใช้ Bootstrap ทำให้ UI สวยงาม
student_list.html
แสดงตารางข้อมูลนักศึกษา
มีช่องค้นหา และปุ่มแก้ไข/ลบ
🔧 Dev Tools แนะนำสำหรับพัฒนา
✅ VS Code
✅ GitHub Desktop
✅ Postman (หากขยายไปใช้ API)
✅ SQLite Browser (ดูฐานข้อมูล)
🎯 ตัวอย่างการใช้งานจริง (Use Case)
โครงการนักศึกษา
เว็บระบบหลังบ้านโรงเรียน
ระบบรับสมัครนักศึกษาใหม่
ใช้ฝึกงานด้าน Django/Full Stack
🧩 การปรับแต่งและขยาย
เพิ่มระบบ login/logout
ใช้ PostgreSQL แทน SQLite
อัปเกรด Bootstrap เป็นเวอร์ชันล่าสุด
เพิ่ม pagination, export PDF หรือ Excel
🚧 การดูแลรักษาและการสนับสนุน
อัปเดต Django เวอร์ชันล่าสุดเสมอ
สำรองฐานข้อมูลหากใช้งานจริง
ปรับปรุง UI ให้เหมาะกับมือถือ (responsive)
🤝 การมีส่วนร่วมในโครงการ
Fork Repo และสร้าง Branch ของคุณเอง
Pull Request ยินดีต้อนรับ!
เปิด Issue หากพบปัญหา
📄 ใบอนุญาต
เผยแพร่ภายใต้ MIT License – นำไปใช้ต่อ/ดัดแปลงได้

📞 ติดต่อ
ผู้พัฒนา:

วงศกร หวลมานพ
อกฤษณ์ นารัง
สิรฐากร กาญจนเสถียร
