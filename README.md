class Course:
    course_counter = 0

    def __init__(self, course_name, course_level):
        Course.course_counter += 1
        self.course_id = Course.course_counter
        self.course_name = course_name
        self.course_level = course_level


class Student:
    student_counter = 0

    def __init__(self, student_name, student_level):
        Student.student_counter += 1
        self.student_id = Student.student_counter
        self.student_name = student_name
        self.student_level = student_level
        self.student_courses = []

    def add_course(self, course):
        if course.course_level == self.student_level:
            self.student_courses.append(course)
            print(f"Added course '{course.course_name}' to {self.student_name}'s courses.")
        else:
            print(f"Cannot add course '{course.course_name}' as it's not suitable for {self.student_name}.")

    def display_details(self):
        print(f"Student Name: {self.student_name}")
        print(f"Student Level: {self.student_level}")
        if self.student_courses:
            print("Courses Enrolled:")
            for course in self.student_courses:
                print(f"- {course.course_name} (Level: {course.course_level})")
        else:
            print("No courses enrolled.")


class SchoolSystem:
    def __init__(self):
        self.students = []
        self.courses = []

    def add_student(self):
        student_name = input("Enter student name: ")
        student_level = self.get_valid_student_level()
        new_student = Student(student_name, student_level)
        self.students.append(new_student)
        print(f"Student '{student_name}' saved successfully.")

    def remove_student(self):
        student_id = int(input("Enter student ID: "))
        student_to_remove = None
        for student in self.students:
            if student.student_id == student_id:
                student_to_remove = student
                break

        if student_to_remove:
            self.students.remove(student_to_remove)
            print("Student deleted successfully.")
        else:
            print("Student does not exist.")

    def edit_student(self):
        student_id = int(input("Enter student ID: "))
        student_to_edit = None
        for student in self.students:
            if student.student_id == student_id:
                student_to_edit = student
                break

        if student_to_edit:
            new_name = input("Enter new student name: ")
            new_level = self.get_valid_student_level()
            student_to_edit.student_name = new_name
            student_to_edit.student_level = new_level
            print("Student details updated successfully.")
        else:
            print("Student does not exist.")

    def display_students(self):
        for student in self.students:
            student.display_details()
            print()

    def add_course(self):
        course_name = input("Enter course name: ")
        course_level = self.get_valid_course_level()
        new_course = Course(course_name, course_level)
        self.courses.append(new_course)
        print("Course created successfully.")

    def add_course_to_student(self):
        student_id = int(input("Enter student ID: "))
        course_id = int(input("Enter course ID: "))
        student = self.find_student_by_id(student_id)
        course = self.find_course_by_id(2)

        if student and course:
            student.add_course(course)
        else:
            print("Student or course not found.")

    def find_student_by_id(self, student_id):
        for student in self.students:
            if student.student_id == student_id:
                return student
        return None

    def find_course_by_id(self, course_id):
        for course in self.courses:
            if course.course_id == course_id:
                return course
        return None

    @staticmethod
    def get_valid_student_level():
        while True:
            student_level = input("Enter student level (A, B, C): ").upper()
            if student_level in ['A', 'B', 'C']:
                return student_level
            else:
                print("Invalid input. Please select a valid level (A, B, C).")

    @staticmethod
    def get_valid_course_level():
        while True:
            course_level = input("Enter course level (A, B, C): ").upper()
            if course_level in ['A', 'B', 'C']:
                return course_level
            else:
                print("Invalid input. Please select a valid level (A, B, C).")

    def main_menu(self):
        while True:
            print("\nMain Menu:")
            print("1. Add New Student")
            print("2. Remove Student")
            print("3. Edit Student")
            print("4. Display all students")
            print("5. Create new Course")
            print("6. Add Course to Student")
            print("7. Quit")

            choice = input("Enter your choice: ")

            if choice == '1':
                self.add_student()
            elif choice == '2':
                self.remove_student()
            elif choice == '3':
                self.edit_student()
            elif choice == '4':
                self.display_students()
            elif choice == '5':
                self.add_course()
            elif choice == '6':
                self.add_course_to_student()
            elif choice == '7':
                print("see you later!")
                break
            else:
                print("Invalid choice. Please select a valid option.")


if __name__ == "__main__":
    school_system = SchoolSystem()
    school_system.main_menu()
