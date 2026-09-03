# Student Records Sorting Using Insertion Sort
# Google Colab Ready

import random
import time

# ---------------------------------------------------------
# Insertion Sort Function
# ---------------------------------------------------------
def insertion_sort(students):
    for i in range(1, len(students)):
        key = students[i]
        j = i - 1

        # Compare CGPA
        while j >= 0 and students[j]["CGPA"] > key["CGPA"]:
            students[j + 1] = students[j]
            j -= 1

        students[j + 1] = key

    return students


# ---------------------------------------------------------
# Display Student Records
# ---------------------------------------------------------
def display_students(students):
    print("------------------------------------------------")
    print(f"{'Register No.':<15}{'Name':<15}{'CGPA':<10}")
    print("------------------------------------------------")

    for student in students:
        print(f"{student['Register No.']:<15}"
              f"{student['Name']:<15}"
              f"{student['CGPA']:<10.2f}")

    print("------------------------------------------------")


# ---------------------------------------------------------
# Create Student Records
# ---------------------------------------------------------
students = [
    {"Register No.": "REG001", "Name": "Arun", "CGPA": 8.2},
    {"Register No.": "REG002", "Name": "Priya", "CGPA": 9.1},
    {"Register No.": "REG003", "Name": "Karthik", "CGPA": 7.5},
    {"Register No.": "REG004", "Name": "Divya", "CGPA": 8.8},
    {"Register No.": "REG005", "Name": "Rahul", "CGPA": 6.9},
    {"Register No.": "REG006", "Name": "Meena", "CGPA": 9.5},
    {"Register No.": "REG007", "Name": "Vijay", "CGPA": 7.8},
    {"Register No.": "REG008", "Name": "Anitha", "CGPA": 8.6}
]

# ---------------------------------------------------------
# Original Records
# ---------------------------------------------------------
print("\nORIGINAL STUDENT RECORDS")
display_students(students)

# ---------------------------------------------------------
# Insertion Sort
# ---------------------------------------------------------
start_time = time.perf_counter()

sorted_students = insertion_sort(students.copy())

end_time = time.perf_counter()

# ---------------------------------------------------------
# Sorted Records
# ---------------------------------------------------------
print("\nSTUDENT RECORDS SORTED BY CGPA")
display_students(sorted_students)

print(f"Execution Time: {(end_time - start_time) * 1000000:.2f} microseconds")


# =========================================================
# PERFORMANCE EVALUATION
# =========================================================

def generate_students(n):
    students = []

    for i in range(n):
        students.append({
            "Register No.": f"REG{i+1:04d}",
            "Name": f"Student{i+1}",
            "CGPA": round(random.uniform(5.0, 10.0), 2)
        })

    return students


def measure_time(data):
    start = time.perf_counter()
    insertion_sort(data.copy())
    end = time.perf_counter()

    return (end - start) * 1000   # milliseconds


# ---------------------------------------------------------
# Dataset Sizes
# ---------------------------------------------------------
sizes = [10, 50, 100, 500, 1000]

print("\nPERFORMANCE ANALYSIS")
print("=" * 75)
print(f"{'N':<10}{'Sorted (ms)':<20}"
      f"{'Reverse Sorted (ms)':<25}{'Random (ms)':<15}")
print("=" * 75)

for n in sizes:

    # Generate random data
    random_data = generate_students(n)

    # Sorted dataset
    sorted_data = sorted(
        random_data,
        key=lambda x: x["CGPA"]
    )

    # Reverse-sorted dataset
    reverse_data = sorted(
        random_data,
        key=lambda x: x["CGPA"],
        reverse=True
    )

    # Measure execution time
    sorted_time = measure_time(sorted_data)
    reverse_time = measure_time(reverse_data)
    random_time = measure_time(random_data)

    print(f"{n:<10}{sorted_time:<20.6f}"
          f"{reverse_time:<25.6f}{random_time:<15.6f}")

print("=" * 75)


# ---------------------------------------------------------
# Complexity Information
# ---------------------------------------------------------
print("\nALGORITHM COMPLEXITY")
print("------------------------------")
print("Best Case    : O(N)")
print("Average Case : O(N^2)")
print("Worst Case   : O(N^2)")
print("Space        : O(1) auxiliary space")
