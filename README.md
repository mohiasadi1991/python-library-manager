import json
import os

FILE_NAME = "library.json"

def load_books():
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r", encoding="utf-8") as file:
            return json.load(file)
    return []

def save_books(books):
    with open(FILE_NAME, "w", encoding="utf-8") as fil:
        json.dump(books, file, indent=4, ensure_ascii=False)

def add_book(books):
    title = input("Book title: ").strip()
    author = input("Author: ").strip()

    if not title or not author:
        print("Title and author cannot be empty.")
        return

    books.append({"title": title, "author": author})
    save_books(books)
    print("Book added successfully!")

def show_books(books):
    if not books:
        print("Your library is empty.")
        return

    for number, book in enumerate(books, 1):
        print(f"{number}. {book['title']} - {book['author']}")

def search_book(books):
    keyword = input("Search title: ").strip().lower()
    results = [
        book for book in books
        if keyword in book["title"].lower()
    ]

    if results:
        for book in results:
            print(f"{book['title']} - {book['author']}")
    else:
        print("No matching books found.")

def remove_book(books):
    show_books(books)

    try:
        number = int(input("Book number to remove: "))
        if 1 <= number <= len(books):
            removed = books.pop(number - 1)
            save_books(books)
            print(f"Removed: {removed['title']}")
        else:
            print("Invalid book number.")
    except ValueError:
        print("Please enter a valid number.")

def main():
    books = load_books()

    while True:
        print("\n===== MY LIBRARY =====")
        print("1. Add book")
        print("2. Show books")
        print("3. Search book")
        print("4. Remove book")
        print("5. Exit")

        choice = input("Choose an option: ")

        if choice == "1":
            add_book(books)
        elif choice == "2":
            show_books(books)
        elif choice == "3":
            search_book(books)
        elif choice == "4":
            remove_book(books)
        elif choice == "5":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Try again.")

if __name__ == "__main__":
    main()
