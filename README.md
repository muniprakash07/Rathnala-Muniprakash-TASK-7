

#  Task 1: Use super() properly


class User:
    username = None
    userid   = None


    def __init__(self, name, id):
        self.name =name
        self.id   = id

    def register(self):
        print("register")

    def login(self):
        print("login")

class Student(User):
    def __init__(self, name, id, dept, fees):
        
        super().__init__(name, id)
        self.dept = dept
        self.fees = fees

class Faculty(User):
    def __init__(self, name, id, salary):
        super().__init__(name, id)
        self.salary = salary

class TempFaculty(User):
    def __init__(self, name, id, duration):
        super().__init__(name, id)
        self.duration = duration


# execution

s = Student("bunty", 1, "CS", 50000)
f = Faculty("vamshi", 2, 90000)
tf = TempFaculty("uday", 3, "12 months")

print(f"Student: {s.name}, ID: {s.id}, Dept: {s.dept}, Fees: {s.fees}")
print(f"Faculty: {f.name}, ID: {f.id}, Salary: {f.salary}")
print(f"TempFaculty: {tf.name}, ID: {tf.id}, Duration: {tf.duration}")




# Task 2: Apply Abstraction


from abc import ABC, abstractmethod

class AbstractUser(ABC):
    @abstractmethod
    def get_details(self):
        pass

class Customer(AbstractUser):
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def get_details(self):
        return f"Customer: {self.name} ({self.email})"

# execution


cust1 = Customer("sai", "sai@example.com")
print(cust1.get_details())

cust2 = Customer("micky", "micky@example.com")
print(cust2.get_details())




# Task 3: Sorting using key



# Sample student data
students = [
    {'name': 'Alice', 'fees': 5000},
    {'name': 'Bob', 'fees': 3000},
    {'name': 'Charlie', 'fees': 4500}
]

students.sort(key=lambda x: x['fees'])

print( students)


faculty = [
    {'name': 'Dr. Smith', 'salary': 80000},
    {'name': 'Dr. Jones', 'salary': 95000},
    {'name': 'Dr. Williams', 'salary': 85000}
]

faculty.sort(key=lambda x: x['salary'], reverse=True)

print( faculty)




# Task 4: Use map()

students = [
    {'name': 'Alice', 'fees': 5000},
    {'name': 'Bob', 'fees': 3000},
    {'name': 'Charlie', 'fees': 4500}
]

names = list(map(lambda s: s['name'], students))

print(names)



# Task 5: Use filter()


students = [
    {'name': 'Alice', 'fees': 50000},
    {'name': 'Bob', 'fees': 60000},
    {'name': 'Charlie', 'fees': 70000}
]

high_fee_students = list(filter(lambda s: s['fees'] > 50000, students))

print(high_fee_students)


faculty = [
    {'name': 'Dr. Smith', 'salary': 25000},
    {'name': 'Dr. Jones', 'salary': 40000},
    {'name': 'Dr. Williams', 'salary': 36000}
]

high_salary_faculty = list(filter(lambda f: f['salary'] > 30000, faculty))

print(high_salary_faculty)


#  Task 6: Use reduce()


from functools import reduce

students = [
    {'name': 'Alice', 'fees': 50000},
    {'name': 'Bob', 'fees': 30000},
    {'name': 'Charlie', 'fees': 45000}
]

faculty = [
    {'name': 'Dr. Smith', 'salary': 25000},
    {'name': 'Dr. Jones', 'salary': 40000},
    {'name': 'Dr. Williams', 'salary': 35000}
]

total_fees = reduce(lambda acc, s: acc + s['fees'], students, 0)

total_salary = reduce(lambda acc, f: acc + f['salary'], faculty, 0)

print(total_salary)

print(total_fees)



#  Task 7: Higher Order Function

def process_users(users, func):
    return list(map(func, users))

users = [
    {'name': 'ajay', 'age': 22},
    {'name': 'srinu', 'age': 25},
    {'name': 'chandu', 'age': 20}
]

names = process_users(users, lambda u: u['name'])

print(names)

def process_users(users, func, operation='map'):
    if operation == 'map':
        return list(map(func, users))
    elif operation == 'filter':
        return list(filter(func, users))
    
users = process_users(users, lambda u: u['age'] > 21, 'filter')

print(users)



# TASK-8: Final Challenge (Important)

from functools import reduce

# ------ Data ------
students = [
    {'name': 'Alice', 'fees': 5000},
    {'name': 'Bob', 'fees': 3000},
    {'name': 'Charlie', 'fees': 4500}
]

faculty = [
    {'name': 'Prof. A', 'salary': 25000},
    {'name': 'Prof. B', 'salary': 40000},
    {'name': 'Prof. C', 'salary': 35000}
]

# ------ Higher Order Function ------

def process_data(data, func, operation='map'):
    if operation == 'map':
        return list(map(func, data))
    elif operation == 'filter':
        return list(filter(func, data))

# ------ Get Details ------

def get_details(data, role):
    if role == 'student':
        return process_data(data, lambda s: f"{s['name']} pays {s['fees']}")
    elif role == 'faculty':
        return process_data(data, lambda f: f"{f['name']} earns {f['salary']}")

# ------ Sorted Data ------

def sort_data(data, key):
    return sorted(data, key=lambda x: x[key])

# ------ Filtered Data ------

def filter_students(data):
    return process_data(data, lambda s: s['fees'] > 4000, 'filter')

def filter_faculty(data):
    return process_data(data, lambda f: f['salary'] > 30000, 'filter')

# ------ reduce ------

def total_fees(data):
    return reduce(lambda acc, s: acc + s['fees'], data, 0)

def total_salary(data):
    return reduce(lambda acc, f: acc + f['salary'], data, 0)

# ------ Execution ------

print("---- All Details ----")
print(get_details(students, 'student'))
print(get_details(faculty, 'faculty'))

print("\n---- Sorted Data ----")
print(sort_data(students, 'fees'))
print(sort_data(faculty, 'salary'))

print("\n---- Filtered Data ----")
print(filter_students(students))
print(filter_faculty(faculty))

print("\n---- Totals ----")
print("Total Fees:", total_fees(students))
print("Total Salary:", total_salary(faculty))
