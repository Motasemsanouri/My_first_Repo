# My_first_Repo
book_collection = []

def add_book():
    title = input("Enter book title: ")
    author = input("Enter book author: ")
    book = {"title": title, "author": author}
    book_collection.append(book)
    print("Book added!")
add_book()
def list_books():
  for book in book_collection:
    print(f"{book['title']} by {book['author']}")
list_books()
def search_books():
    search_title = input("Enter book title to search: ").lower()
    search_results = [book for book in book_collection if search_title in book['title'].lower()]
    if search_results:
        print("Search Results:")
        for index, book in enumerate(search_results, start=1):
            print(f"{index}. Title: {book['title']}, Author: {book['author']}")
    else:
        print("No books found.")
search_books()
while True:
        print("\nWhat would you like to do?")
        print("- Add a book (add)")
        print("- List all books (list)")
        print("- Search for a book (search)")
        print("- Quit (quit)")

        choice = input("Choice: ").lower()

        if choice == "add":
            add_book()
        elif choice == "list":
            list_books()
        elif choice == "search":
            search_books()
        elif choice == "quit":
            print("Goodbye!")
            break
        else:
            print("Invalid choice, please try again.")
