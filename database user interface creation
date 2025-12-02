import pyodbc

conn = pyodbc.connect(
    r'DRIVER={ODBC Driver 18 for SQL Server};'
    r'SERVER=DESKTOP-M2HN7DT\SQLEXPRESS;'
    r'DATABASE=master;'
    r'Trusted_Connection=yes;'
    r'TrustServerCertificate=yes;'
)
cursor =conn.cursor()
print("Connected to sql server Successfully")

cursor.execute('''
IF OBJECT_ID('students','U') IS NULL
CREATE TABLE students(
    id INT IDENTITY(1,1) PRIMARY KEY,
    name NVARCHAR(50),
    age INT,
    grade NVARCHAR(10)
)
''')
conn.commit()
print("Table 'students' checked/created successfully")



import tkinter as tk
from tkinter import messagebox

# List to store student records
students = []

# Functions for buttons
def add_student():
    name = entry_name.get()
    age = entry_age.get()
    grade = entry_grade.get()
    if name and age and grade:
        students.append({"name": name, "age": age, "grade": grade})
        messagebox.showinfo("Success", "Student added!")
        clear_entries()
    else:
        messagebox.showwarning("Input Error", "Please fill all fields.")

def view_students():
    if students:
        info = ""
        for i, s in enumerate(students, start=1):
            info += f"{i}. Name: {s['name']}, Age: {s['age']}, Grade: {s['grade']}\n"
        messagebox.showinfo("Students List", info)
    else:
        messagebox.showinfo("Students List", "No students added yet.")

def update_student():
    index = simpledialog.askinteger("Input", "Enter student number to update:")
    if index and 0 < index <= len(students):
        name = entry_name.get()
        age = entry_age.get()
        grade = entry_grade.get()
        if name and age and grade:
            students[index-1] = {"name": name, "age": age, "grade": grade}
            messagebox.showinfo("Success", "Student updated!")
            clear_entries()
        else:
            messagebox.showwarning("Input Error", "Please fill all fields.")
    else:
        messagebox.showerror("Error", "Invalid student number.")

def delete_student():
    index = simpledialog.askinteger("Input", "Enter student number to delete:")
    if index and 0 < index <= len(students):
        students.pop(index-1)
        messagebox.showinfo("Success", "Student deleted!")
    else:
        messagebox.showerror("Error", "Invalid student number.")

def clear_entries():
    entry_name.delete(0, tk.END)
    entry_age.delete(0, tk.END)
    entry_grade.delete(0, tk.END)

# Main window
root = tk.Tk()
root.title("Student Management System")
root.geometry("300x300")

# Name
tk.Label(root, text="Name").pack()
entry_name = tk.Entry(root)
entry_name.pack()

# Age
tk.Label(root, text="Age").pack()
entry_age = tk.Entry(root)
entry_age.pack()

# Grade
tk.Label(root, text="Grade").pack()
entry_grade = tk.Entry(root)
entry_grade.pack()

# Buttons
tk.Button(root, text="Add Student", command=add_student).pack(pady=5)
tk.Button(root, text="View Students", command=view_students).pack(pady=5)
tk.Button(root, text="Update Student", command=update_student).pack(pady=5)
tk.Button(root, text="Delete Student", command=delete_student).pack(pady=5)

root.mainloop()
