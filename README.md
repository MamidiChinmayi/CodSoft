class Contact:
    def __init__(self, name, phone, email):
        self.name = name
        self.phone = phone
        self.email = email
    def __str__(self):
        return f"Name: {self.name}, Phone: {self.phone}, Email: {self.email}"
class ContactBook:
    def __init__(self):
        self.contacts = []
    def add_contact(self, name, phone, email):
        contact = Contact(name, phone, email)
        self.contacts.append(contact)
        print("Contact added successfully!!!")
    def view_contacts(self):
        if not self.contacts:
            print("Contact list is empty!!!")
        else:
            print("Contact List:")
            for contact in self.contacts:
                print(contact)
    def search_contact(self, name):
        results = [contact for contact in self.contacts if contact.name.lower() == name.lower()]
        if not results:
            print("No contact found with that name.")
        else:
            print("Search Results:")
            for contact in results:
                print(contact)
    def update_contact(self, name):
        found = False
        for contact in self.contacts:
            if contact.name.lower() == name.lower():
                print("Enter new details (leave blank to keep current value):")
                new_name = input(f"New Name ({contact.name}): ").strip() or contact.name
                new_phone = input(f"New Phone ({contact.phone}): ").strip() or contact.phone
                new_email = input(f"New Email ({contact.email}): ").strip() or contact.email
                contact.name = new_name
                contact.phone = new_phone
                contact.email = new_email
                print("Contact updated successfully.")
                found = True
                break
        if not found:
            print("No contact found with that name.")
    def delete_contact(self, name):
        initial_length = len(self.contacts)
        self.contacts = [contact for contact in self.contacts if contact.name.lower() != name.lower()]
        if len(self.contacts) < initial_length:
            print("Contact deleted successfully.")
        else:
            print("No contact found with that name.")
def main():
    contact_book = ContactBook()
    while True:
        print("\n---Contact Book---")
        print("1. Add Contact")
        print("2. View Contact List")
        print("3. Search Contact")
        print("4. Update Contact")
        print("5. Delete Contact")
        print("6. Exit")
        choice = input("Choose an option: ").strip()
        if choice == "1":
            name = input("Enter name: ").strip()
            phone = input("Enter phone number: ").strip()
            email = input("Enter email: ").strip()
            contact_book.add_contact(name, phone, email)
        elif choice == "2":
            contact_book.view_contacts()
        elif choice == "3":
            name = input("Enter name to search: ").strip()
            contact_book.search_contact(name)
        elif choice == "4":
            name = input("Enter name to update: ").strip()
            contact_book.update_contact(name)
        elif choice == "5":
            name = input("Enter name to delete: ").strip()
            contact_book.delete_contact(name)
        elif choice == "6":
            print("Exiting Contact Book. Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")
if __name__ == "__main__":
    main()
