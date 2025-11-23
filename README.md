Expense Manager

  Overview:
  
    Expense Manager is a simple Python application that
    helps users record, view, and visualize their personal
    spending. The system supports adding expenses with
    categories and notes, viewing all recorded transactions,
    and generating graphical summaries for easier analysis.
    It features a menu-driven interface and stores data in a
    local CSV file for easy tracking and portability.
    
  Features:
  
    • Add Expenses: Quickly log spending with amount,
    category, and optional notes.
    
    • View Expenses: See a clear, formatted list of all
    your transactions.
    
    • Visualize Expenses: Generate bar and pie charts to
    understand your spending habits by category.
    
    • Persistent Storage: All data is safely stored in a
    local CSV file, enabling easy retrieval and analysis.
    
    • User-Friendly Interface: Simple command-line
    menu for easy navigation.
    
    • Error Handling: Notifies users of invalid input and
    missing data gracefully.
    
  Technologies Used:
  
    • Python 3.x
    
    • csv (for reading/writing expense data)
    
    • matplotlib (for charting and data visualization)
    
    • os (for file management)
    
    • datetime (for recording expense dates)
    
  Installation & Setup:
  
    1. Clone this repository to your local machine:
    
      ➔ git clone <repo-url>
      
    2. Ensure you have Python 3.x installed
       and matplotlib library available. You can install
       matplotlib using:
       
      ➔ pip install matplotlib
      
    3. Run the program from your command line:
    
      ➔ python expense-manager.py
      
  Usage Instructions:
  
    • Add Expense: Choose option 1 in the menu and
    enter the required details.
    
    • View Expenses: Select option 2 to display all your
    recorded transactions.
    
    • Plot Expenses: Select option 3 to visualize your
    expenses by category.
    
    • Exit: Choose option 4 when finished.
    
  Testing:
  
    The system is interactive. Add, view, and plot expenses
    to see the program functionalities.
    Edge cases like missing amounts, invalid inputs, or
    empty data will be handled with meaningful prompts.
    
  Project Structure:
  
    expense-manager/
    |
    ├ expense-manager.py
    ├ expenses.csv # Auto-created if not present
    ├ README.md
