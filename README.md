def main():
    student_names = [
        "Alice Oliva", "Paola Leyco", "Hannah Jane", "Jasmine Insorio", 
        "Evan Wright", "Fiona Gallagher", "George Martin", "Lea May Pinoc", 
        "Ian Marantal", "Jayson Rambac"
    ]
    
    student_grades = [
        85, 92, 78, 96, 88, 72, 91, 83, 79, 95
    ]

    while True:
        print("\n--- Student Record System ---")
        print("1. View All Records")
        print("2. Compute Average Grade")
        print("3. Sort Grades (Ascending)")
        print("4. Search for a Student")
        print("5. Exit")
        
        choice = input("Enter your choice (1-5): ")

        if choice == '1':
            view_records(student_names, student_grades)
        
        elif choice == '2':
            compute_average(student_grades)
        
        elif choice == '3':
            sort_grades(student_names, student_grades)
        
        elif choice == '4':
            search_student(student_names, student_grades)
        
        elif choice == '5':
            print("Exiting system. Goodbye!")
            break
        
        else:
            print("Invalid choice. Please try again.")

def view_records(names, grades):
    """Displays the current state of the arrays."""
    print(f"\n{'Name':<20} | {'Grade':<5}")
    print("-" * 30)
    for i in range(len(names)):
        print(f"{names[i]:<20} | {grades[i]:<5}")

def compute_average(grades):
    """Calculates the sum and divides by the count."""
    if not grades:
        print("No grades to calculate.")
        return

    total = 0
    for grade in grades:
        total += grade
    
    average = total / len(grades)
    print(f"\nTotal Sum: {total}")
    print(f"Number of Students: {len(grades)}")
    print(f"Average Grade: {average:.2f}")

def sort_grades(names, grades):
    """
    Sorts the data. 
    NOTE: Since we have parallel arrays, we cannot just sort 'grades' 
    without breaking the link to 'names'. 
    We zip them together, sort, and then unzip.
    """

    combined = list(zip(names, grades))
    
    combined.sort(key=lambda x: x[1])
    
    names[:], grades[:] = zip(*combined)
    
    print("\nRecords sorted by grade (Low to High):")
    view_records(names, grades)

def search_student(names, grades):
    """Searches for a specific name in the array."""
    target = input("Enter the student's name to search: ").strip()
    
    
    found = False
    for i in range(len(names)):
        if names[i].lower() == target.lower(): 
            print(f"\nFound: {names[i]} has a grade of {grades[i]}")
            found = True
            break
    
    if not found:
        print(f"\nStudent '{target}' not found in the records.")

if __name__ == "__main__":
    main()
