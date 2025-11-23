# Expense-Manager
# Import module for reading and writing CSV files
import csv
# Import module to interact with operating system (used to check if file exists)
import os
# Import the plotting library for creating charts
import matplotlib.pyplot as plt
# Import datetime module for getting the current date
from datetime import datetime

# File where all expenses will be stored
DATA_FILE = "expenses.csv"

# Check if the expenses CSV file exists; if not, create it
if not os.path.exists(DATA_FILE):
   # Open the file in write mode and create a new CSV
    with open(DATA_FILE, "w", newline="") as f:
        writer = csv.writer(f)  # Create a CSV writer object
        writer.writerow(["date", "category", "amount", "note"])  # Write the CSV headers


def add_expense(category, amount, note=""):
# Adds a single expense entry to the CSV file.

  # Get today's date in YYYY-MM-DD format
    date = datetime.now().strftime("%Y-%m-%d")

  # Open the CSV file in append mode to add a new row
    with open(DATA_FILE, "a", newline="") as f:
        writer = csv.writer(f) 
  # Create CSV writer
        writer.writerow([date, category, amount, note])
  # Write the expense data as a new row

   # Notify the user
    print("Expense added successfully!")


def view_expenses():
   # Reads and prints all expenses from the CSV file.

   # Print heading
    print("--- Expense List ---")

   # Open the CSV file in read mode
    with open(DATA_FILE, "r") as f:
        reader = csv.reader(f)  
  # Create CSV reader
        next(reader)      
  # Skip the header row

   # Loop through each row and print details
        for row in reader:
            print(f"Date: {row[0]}, Category: {row[1]}, Amount: ₹{row[2]}, Note: {row[3]}")

    print()  
  # Print extra line


def plot_expenses():
   # Reads expenses and displays a bar chart showing total amount per category.

   # Dictionary to accumulate totals for each category
    categories = {}

   # Read the CSV file
    with open(DATA_FILE, "r") as f:
        reader = csv.reader(f)  
  # CSV reader
        next(reader) 
  # Skip header

  # Loop through each row (date, category, amount, note)
        for date, category, amount, note in reader:
   # Add the expense amount to the correct category
            categories[category] = categories.get(category, 0) + float(amount)

  # If there are no expenses recorded yet
    if not categories:
        print("No expenses to plot. Add some first!")
        return

   # Extract category names and their total values
    names = list(categories.keys())
    values = list(categories.values())

  # Create and display a bar chart
    plt.figure(figsize=(7, 5))
    plt.bar(names, values) 
    plt.title("Expenses by Category") 
    plt.xlabel("Category")  
    plt.ylabel("Total Amount (₹)") 
    plt.tight_layout() 
    plt.show() 

   # Create and display a pie chart
    plt.figure(figsize=(7, 7)) 
    plt.pie(values, labels=names, autopct='%1.1f%%', startangle=90)
    plt.title("Expenses by Category (Pie Chart)") 
    plt.tight_layout()
    plt.show()

def main():
  # Displays menu and handles user input for the program.

    while True:
        print("Expense Manager")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Plot Expenses")
        print("4. Exit")
  # Display the menu

   # Read user choice
        choice = input("Enter choice: ")

        if choice == "1":
  # Ask user for required expense details
            category = input("Category: ")
            amount = float(input("Amount: ₹"))  
  # Convert entered value to float
            note = input("Note (optional): ")

            add_expense(category, amount, note)
  # Call the function to store the expense

        elif choice == "2":
            view_expenses()
   # Display stored expenses

        elif choice == "3":
            plot_expenses()
   # Generate and show expense chart

        elif choice == "4":
            print("Goodbye!")
            break
 # Exit the program
 
        else:
            print("Invalid choice. Try again.")
 # Handle invalid input

if __name__ == "__main__":
    main()
  # This ensures that main() runs only if the script is executed directly
