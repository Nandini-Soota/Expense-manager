# Expense-Manager
#Import module for reading and writing CSV files
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
        writer = csv.writer(f) 
        writer.writerow(["date", "category", "amount", "note"]) 
        
# Adds a single expense entry to the CSV file.
def add_expense(category, amount, note=""):
    
   # Get today's date in YYYY-MM-DD format
    date = datetime.now().strftime("%Y-%m-%d")

   # Open the CSV file in append mode to add a new row
    with open(DATA_FILE, "a", newline="") as f:
        writer = csv.writer(f)  # Create CSV writer
        writer.writerow([date, category, amount, note])  

   # Notify the user
    print("Expense added successfully!")

# Reads and prints all expenses from the CSV file.
def view_expenses():

# Print heading
    print("--- Expense List ---")

  # Open the CSV file in read mode
    with open(DATA_FILE, "r") as f:
        reader = csv.reader(f) 
        next(reader)  

   # Loop through each row and print details
        for row in reader:
            print(f"Date: {row[0]}, Category: {row[1]}, Amount: ₹{row[2]}, Note: {row[3]}")

# Print extra line
    print()  

# Reads expenses and displays a bar chart showing total amount per category.
def plot_expenses():

  # Dictionary to accumulate totals for each category
    categories = {}

  # Read the CSV file
    with open(DATA_FILE, "r") as f:
        reader = csv.reader(f) 
        next(reader) 

   # Loop through each row (date, category, amount, note)
        for date, category, amount, note in reader:
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

 # Create and display apie chart
    plt.figure(figsize=(7, 7)) 
    plt.pie(values, labels=names, autopct='%1.1f%%', startangle=90)
    plt.title("Expenses by Category (Pie Chart)")
    plt.tight_layout() 
    plt.show()

# Displays menu and handles user input for the program.
def main():
   

# Display the menu
    while True:
        print("Expense Manager")
        print("1. Add Expense")
        print("2. View Expenses")
        print("3. Plot Expenses")
        print("4. Exit")

  # Read user choice
        choice = input("Enter choice: ")

        if choice == "1":
  # Ask user for required expense details
            category = input("Category: ")
            amount = float(input("Amount: ₹"))  
            note = input("Note (optional): ")

   # Call the function to store the expense
            add_expense(category, amount, note)

 # Display stored expenses
        elif choice == "2":
            view_expenses()
            
# Generate and show expense chart
        elif choice == "3":
            plot_expenses()
            
  # Exit the program
        elif choice == "4":
            print("Goodbye!")
            break

  # Handle invalid input
        else:
            print("Invalid choice. Try again.")


# This ensures that main() runs only if the script is executed directly
if __name__ == "__main__":
    main()
