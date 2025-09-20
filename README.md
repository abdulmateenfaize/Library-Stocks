/*
Title: Library Book Management System
Course: CS112 – Semester 2, 2025
Assignment: 1
Student:
   - Abdul Mateen Faize 

*/

#include <iostream>
#include <fstream>
#include <string>
#include<stdio.h>
using namespace std;

// Global Variable for the size of arrays.
const int SIZE = 8;

// Initialization of function that prints 'Availible' or 'Out of Stock' according to the number of copies a book has.
string check_book_availability(int num_book);

//  Initialization of function checks the entry of the user, in case the usere misbehave.
void Check_Entry(int* x);

struct Book {

	int Book_ID;
	string Book_Title;
	int Copies_Available;
};

// Initialization of function display the output.
void Display(Book book1[SIZE], string num_copies[SIZE]);

//  Initialization of function used for asking the user for an update in the data
void Update_data(Book book1[SIZE], string num_copies[SIZE]);


int main() {

	Book book1[SIZE];
	string num_copies[SIZE];

	ifstream in_file("books.txt");
	if (!in_file.is_open()) {
		cout << "File not found" << endl;
		system("pause");
		return 1;
	}

	// this comma is used to store the "," after the ID number of book in the .txt file.
	char comma;

	for (int count = 0; count < SIZE; count++) {
		// Reads the ID of the book including comma.
		in_file >> book1[count].Book_ID >> comma;
		// Reads the book title despit the spaces until the comma.
		getline(in_file, book1[count].Book_Title, ',');
		// Reads the number of copies a book has.
		in_file >> book1[count].Copies_Available;

		//it stores the status of books as "Avilible" or "out of stock" in the array.
		num_copies[count] = check_book_availability(book1[count].Copies_Available);
	}
	in_file.close();

	cout << "------------------------------------------------------------" << endl;
	cout << "		***Library Book Management System***" << endl;
	cout << "------------------------------------------------------------" << endl;

	// Function used to display the data stored.
	Display(book1, num_copies);

	// Asking the user for an update in the data
	Update_data(book1, num_copies);

	system("pause");
	return 0;
}

// A functions that prints 'Availible' or 'Out of Stock' according to the number of copies a book has.
string check_book_availability(int num_book) {
	string available;
	if (num_book <= 0) {
		available = "Out of Stock";
	}
	else {

		available = "Available";
	}
	return available;
}

//  function checks the entry of the user, in case the usere misbehave.
void Check_Entry(int* x) {
	cin >> *x;
	while (cin.fail() || *x < 0) {
		cout << "Unavilable or wrong entry. Please try again" << endl;
		cin.clear();
		cin.ignore(1000, '\n');
		cin >> *x;
	}

}

// function display the output.
void Display(Book book1[SIZE], string num_copies[SIZE]) {

	int most_copy = 0;
	int total_copies = 0;
	int out_of_stock = 0;
	double Out_Of_Stock_Percentage;

	cout << "\n\n";

	for (int count = 0; count < SIZE; count++) {

		cout << book1[count].Book_ID << ", "
			<< book1[count].Book_Title << ", "
			<< num_copies[count] << "["
			<< book1[count].Copies_Available << "]" << endl;

		total_copies += book1[count].Copies_Available;

		if (book1[most_copy].Copies_Available < book1[count].Copies_Available) {
			most_copy = count;
		}

		if (book1[count].Copies_Available == 0) {
			out_of_stock++;
		}
	}

	Out_Of_Stock_Percentage = (out_of_stock * 100.0) / SIZE;

	cout << "\n\nMost copies is from book:   " << book1[most_copy].Book_ID << ", "
		<< book1[most_copy].Book_Title << ", "
		<< num_copies[most_copy] << "[" << book1[most_copy].Copies_Available << "]" << endl;

	cout << "Number of books in the stock: " << total_copies << endl;

	cout << "Percentage of out of stock books is: " << Out_Of_Stock_Percentage << "%\n\n" << endl;
}

//  function used for asking the user for an update in the data
void Update_data(Book book1[SIZE], string num_copies[SIZE]) {

	string choice;
	int bookID;
	int Updated_copies;
	bool found;

	cout << "Press \' y \'  or \' Y \'to update the number of copies for a book." << endl;
	cin >> choice;

	while (choice == "y" || choice == "Y") {
		cout << "Please enter the book's ID:" << endl;
		// it checks the entry of the user
		Check_Entry(&bookID);
		found = false;

		for (int i = 0; i < SIZE; i++) {
			if (bookID == book1[i].Book_ID) {
				found = true;
				cout << "Enter the Number of copies:" << endl;

				Check_Entry(&Updated_copies);

				// Edit the array according to the update.
				book1[i].Copies_Available = Updated_copies;
				num_copies[i] = check_book_availability(Updated_copies);
				cout << " Updated book: \n" <<
					bookID << ", " << book1[i].Book_Title << ", "
					<< num_copies[i] << "["
					<< book1[i].Copies_Available << "]\n\n" << endl;
				cout << "\n Updated data is: " << endl;
				Display(book1, num_copies);

				break;
			}
		}
		// if the system didn't found the book
		if (!found) {
			cout << "Book not found!" << endl;
		}

		cout << "Press \' y \' or \' Y \' to update the number of copies for a book." << endl;
		cin >> choice;
	}
}
