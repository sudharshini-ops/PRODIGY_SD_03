# PRODIGY_SD_03
#A Simple Contact Managment System
This is a simple Contact Management System built with Python. The system allows users to add, view, search, and delete contacts, providing a user-friendly command-line interface for managing personal or professional contacts efficiently.

# Contact Management System


contacts = []


def add_contact(name, phone, email):
    contact = {
        'name': name,
        'phone': phone,
        'email': email
    }
    contacts.append(contact)
    print(f"Contact for {name} added.")

def view_contacts():
    if not contacts:
        print("No contacts available.")
    else:
        for idx, contact in enumerate(contacts, start=1):
            print(f"{idx}. Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")

def search_contact(name):
    found_contacts = [contact for contact in contacts if name.lower() in contact['name'].lower()]
    if not found_contacts:
        print(f"No contacts found for {name}.")
    else:
        for contact in found_contacts:
            print(f"Name: {contact['name']}, Phone: {contact['phone']}, Email: {contact['email']}")

def delete_contact(name):
    global contacts
    new_contacts = [contact for contact in contacts if name.lower() not in contact['name'].lower()]
    if len(new_contacts) == len(contacts):
        print(f"No contacts found for {name}.")
    else:
        contacts = new_contacts
        print(f"Contact(s) for {name} deleted.")


def main():
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

if __name__ == "__main__":
    main()

