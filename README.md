# My_first_Repo

import json
import pandas as pd
import matplotlib.pyplot as plt

class Library:
    def __init__(self):
        self.books = []

    def add_book(self):
        title = input("Enter the book title: ")
        author = input("Enter the author's name: ")
        category = input("Enter the book category: ")
        book = {"title": title, "author": author, "category": category}
        self.books.append(book)
        print("Book added successfully!")

    def save_library(self, filename):
        try:
            with open(filename, 'w') as file:
                json.dump(self.books, file, indent=4)
            print(f"Library saved to {filename} successfully!")
        except IOError as e:
            print(f"Error saving library: {e}")

    def load_library(self, filename):
        try:
            with open(filename, 'r') as file:
                self.books = json.load(file)
            print(f"Library loaded from {filename} successfully!")
        except FileNotFoundError:
            print("No library file found. Starting with an empty library.")
        except json.JSONDecodeError:
            print("Error parsing the library file. The file may be corrupted.")

    def visualize_library(self):
        # Convert books list to a pandas DataFrame
        df = pd.DataFrame(self.books)

        category_count = df['category'].value_counts()

        # Plotting the bar chart
        category_count.plot(kind='bar', x="Category",y='Number of Books')
        plt.title('Library Distribution by Category')
        plt.show()


    def display_menu(self):
        print("\nWelcome to Your Personal Library Manager!")
        print("\nWhat would you like to do?")
        print("1. Add a book")
        print("2. Save library to file")
        print("3. Load library from file")
        print("4. Visualize library by category")
        print("5. Quit")

        choice = input("Enter choice (1-5): ")
        return choice

def main():
    library = Library()
    filename = "library.json"

    while True:
        choice = library.display_menu()

        if choice == "1":
            library.add_book()
        elif choice == "2":
            library.save_library(filename)
        elif choice == "3":
            library.load_library(filename)
        elif choice == "4":
            library.visualize_library()
        elif choice == "5":
            print("Exiting the Library Manager. Goodbye!")
            break
        else:
            print("Invalid choice, please enter a number between 1 and 5.")

if __name__ == "__main__":
    main()

