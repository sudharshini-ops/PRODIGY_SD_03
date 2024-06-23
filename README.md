# PRODIGY_SD_03
#A Simple Contact Managment System
This is a simple Contact Management System built with Python. The system allows users to add, view, search, and delete contacts, providing a user-friendly command-line interface for managing personal or professional contacts efficiently.

#Contact Management System

import sqlite3

# Database file
DATABASE = 'contacts.db'

# Create table if it doesn't exist
def create_table():
    conn = sqlite3.connect(DATABASE)
    cursor = conn.cursor()
    cursor.execute('''
        CREATE TABLE IF NOT EXISTS contacts (
            id INTEGER PRIMARY KEY AUTOINCREMENT,
            name TEXT NOT NULL,
            phone TEXT NOT NULL,
            email TEXT NOT NULL
        )
    ''')
    conn.commit()
    conn.close()

# Add a contact
def add_contact(name, phone, email):
    conn = sqlite3.connect(DATABASE)
    cursor = conn.cursor()
    cursor.execute('''
        INSERT INTO contacts (name, phone, email)
        VALUES (?, ?, ?)
    ''', (name, phone, email))
    conn.commit()
    conn.close()
    print(f"Contact for {name} added.")

# View all contacts
def view_contacts():
    conn = sqlite3.connect(DATABASE)
    cursor = conn.cursor()
    cursor.execute('SELECT * FROM contacts')
    contacts = cursor.fetchall()
    conn.close()
    if not contacts:
        print("No contacts available.")
    else:
        for contact in contacts:
            print(f"ID: {contact[0]}, Name: {contact[1]}, Phone: {contact[2]}, Email: {contact[3]}")

# Search for a contact by name
def search_contact(name):
    conn = sqlite3.connect(DATABASE)
    cursor = conn.cursor()
    cursor.execute('SELECT * FROM contacts WHERE name LIKE ?', ('%' + name + '%',))
    contacts = cursor.fetchall()
    conn.close()
    if not contacts:
        print(f"No contacts found for {name}.")
    else:
        for contact in contacts:
            print(f"ID: {contact[0]}, Name: {contact[1]}, Phone: {contact[2]}, Email: {contact[3]}")

# Delete a contact by name
def delete_contact(name):
    conn = sqlite3.connect(DATABASE)
    cursor = conn.cursor()
    cursor.execute('DELETE FROM contacts WHERE name LIKE ?', ('%' + name + '%',))
    conn.commit()
    deleted = cursor.rowcount
    conn.close()
    if deleted == 0:
        print(f"No contacts found for {name}.")
    else:
        print(f"Contact(s) for {name} deleted.")

# Main program loop
def main():
    create_table()
    while True:
        print("\nContact Management System")
        print("1. Add Contact")
        print("2. View Contacts")
        print("3. Search Contact")
        print("4. Delete Contact")
        print("5. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            name = input("Enter name: ")
            phone = input("Enter phone: ")
            email = input("Enter email: ")
            add_contact(name, phone, email)
        elif choice == '2':
            view_contacts()
        elif choice == '3':
            name = input("Enter name to search: ")
            search_contact(name)
        elif choice == '4':
            name = input("Enter name to delete: ")
            delete_contact(name)
        elif choice == '5':
            print("Exiting Contact Management System. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

# Run the main program loop
if __name__ == "__main__":
    main()



    
        
        
