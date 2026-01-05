# Словник для зберігання інформації про студентів
students_data = {}

def add_student(student_id, group_number, full_name, course, grades):
    """
    Функція додає студента до словника students_data.
    
    student_id - унікальний ідентифікатор студента
    group_number - номер групи
    full_name - ПІБ студента
    course - курс навчання
    grades - словник предметів та оцінок
    """
    students_data[student_id] = {
        "group_number": group_number,
        "full_name": full_name,
        "course": course,
        "grades": grades
    }

def calculate_average_grade(grades):
    """
    Функція обчислює середній бал студента.
    """
    return sum(grades.values()) / len(grades)

def get_students_sorted_by_average():
    """
    Функція повертає список студентів,
    відсортованих за середнім балом у порядку спадання.
    """
    return sorted(
        students_data.items(),
        key=lambda item: calculate_average_grade(item[1]["grades"]),
        reverse=True
    )

def find_student_by_name(name_part):
    """
    Функція виконує пошук студента за частиною ПІБ.
    """
    result = {}
    for student_id, data in students_data.items():
        if name_part.lower() in data["full_name"].lower():
            result[student_id] = data
    return result

# Додавання студентів
add_student(
    1,
    "KN-21",
    "Іваненко Іван Іванович",
    2,
    {
        "Математика": 90,
        "Програмування": 95,
        "Фізика": 88
    }
)

add_student(
    2,
    "KN-21",
    "Петренко Олена Сергіївна",
    2,
    {
        "Математика": 85,
        "Програмування": 92,
        "Фізика": 90
    }
)

add_student(
    3,
    "KN-21",
    "Коваль Андрій Миколайович",
    2,
    {
        "Математика": 78,
        "Програмування": 80,
        "Фізика": 75
    }
)

# Виведення студентів, відсортованих за середнім балом
print("Студенти, відсортовані за середнім балом:")
for student_id, data in get_students_sorted_by_average():
    avg = calculate_average_grade(data["grades"])
    print(f"{data['full_name']} – середній бал: {avg:.2f}")

# Пошук студента за ім'ям
print("\nРезультат пошуку:")
found_students = find_student_by_name("Іван")
for student in found_students.values():
    print(student["full_name"])
