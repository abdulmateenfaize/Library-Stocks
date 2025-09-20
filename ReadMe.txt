LIBRARY BOOK MANAGEMENT SYSTEM

Introduction

This is a Library Book Management System written in C++. The program reads book records from an input file (books.txt), processes them, and displays the library's inventory with the availability status of each book. It also allows the user to update the number of copies of a book by its ID.

Key features:

- Reads data (Book ID, Title, Copies Available) from books.txt.
- Displays each book's status: Available or Out of Stock.
- Shows:
  - Book with the most copies.
  - Total number of books in stock.
  - Percentage of out-of-stock books.
- Allows the user to update book copies interactively.

How It Works

1. File Reading:
   - Reads each book's ID, Title, and number of copies.

2. Availability Check:
   - If copies > 0: "Available"
   - If copies ≤ 0: "Out of Stock"

3. Display:
   - Prints all books with their status and copy count.
   - Identifies the book with the highest copies.
   - Calculates the total copies in stock.
   - Shows the percentage of out-of-stock books.

4. Update Functionality:
   - The user can update the number of copies for a book using its ID.
   - Input validation ensures only valid integers are accepted.
   - After each update, the full updated inventory is displayed.






User Guide

This program is designed to enable users to view and update book records within a small library system.

1. Program Start

When executed, the program automatically loads eight book records from the input file and displays them on the screen. For each book, the following information is shown:

- Book ID
- Title
- Availability status (Available or Out of Stock)
- Number of copies currently in stock

2. Library Statistics

Along with the list of books, the program also calculates and displays:

- The book with the highest number of copies
- The total number of copies across all books
- The percentage of books that are out of stock

3. Updating Records

After the initial display, the program will prompt the user:
"Press 'y' or 'Y' to update the number of copies for a book."

- If the user chooses not to update (by pressing any other key), the program ends.
- If the user presses y or Y, the following sequence occurs:

  1. The program requests the Book ID of the record to be updated.
     - If the entered ID does not exist, the program notifies the user ("Book not found!") and allows another attempt.

  2. The program then requests the new number of copies.
     - Invalid input (such as negative numbers or non-numeric values) is rejected, and the user is asked to re-enter a valid number.

  3. Once a valid entry is provided, the book record is updated and displayed, and the updated statistics are shown again.

4. Repeating Updates

The system allows multiple updates within a single session. After each update, the user is again prompted to continue or exit. Choosing y repeats the process; any other key will end the program.

5. Program End

The program closes when the user decides not to perform further updates.

6. Important Notes

- Updates made during execution are temporary. They are not saved to the original file and will be lost once the program terminates.
- The program is currently limited to eight books, as defined in the code.






Variables Explanation:

Global Constants
- SIZE: Represents the fixed number of books the system can handle. In this assignment, it's set to 8.

Struct: Book
The Book structure stores details of each book. It has three fields:
- Book_ID: A unique integer assigned to each book.
- Book_Title: A string storing the title of the book.
- Copies_Available: An integer showing how many copies of the book are available in stock.

Arrays
- book1[SIZE]: An array of Book objects that stores all the library's books read from the file.
- num_copies[SIZE]: A string array storing the availability status of each book (either "Available" or "Out of Stock").

Input / File Handling
- in_file: The input file stream object that reads data from books.txt.
- comma: A character variable used to temporarily capture commas in the input file, which ensures book IDs, titles, and copies are correctly separated.

Display Function Variables
- most_copy: An integer that keeps the position of the book with the highest number of copies.
- total_copies: An integer that counts the total number of book copies.
- out_of_stock: An integer that counts how many books have zero copies available.
- Out_Of_Stock_Percentage: A double value representing the percentage of books that are out of stock.

Update Function Variables
- choice: A string that stores the user's decision on whether they want to update book data (expected values: "y" or "Y" for yes).
- bookID: An integer storing the user's input for the ID of the book they want to update.
- Updated_copies: An integer storing the new number of copies provided by the user for the selected book.
- found: A boolean flag used to check if the entered book ID exists in the system.

Utility Function Variables
- x (pointer in Check_Entry): A pointer to an integer that captures user input. The function ensures the input is valid (non-negative integer).

