#!/usr/bin/python
#project - contact data with python
#use :%s/echo/print to replace def

#reset # clear screen
import os.path
import sys

#show menu function
def print_menu():
    print("1. Search")
    print("2. Add")
    print("3. Delete")
    print("4. Modify")
    print("5. Exit")

#search function
def search_record():
    name = input("Enter name: ")
    with open("hospital_records.txt", "r") as file:
        results = file.readlines()
        matches = [record for record in results if re.search(rf"^{name}", record, re.IGNORECASE)]
        if not matches:
            print("Contact not found")
        else:
            print("Contact found")
            print("".join(matches))

def show_record():
    with open("hospital_records.txt", "r") as file:
        print(file.read())

#add record to file
def add_record():
    medical_id = input("Please enter medical id: ")
    name = input("Please enter full name: ")
    phone_number = input("Please enter phone number: ")
    email = input("Please enter email: ")
    address = input("Please enter address: ")
    dr = input("Please enter dr: ")

    record = f"{medical_id} {name} {phone_number} {email} {address} {dr}\n"
    with open("hospital_records.txt", "a") as file:        
    file.write(record)
    print("Record added! Displaying records:")
    show_record()

def delete_record():
    name = input("Enter record name: ")
    with open("hospital_records.txt", "r") as file:
        records = file.readlines()
    matches = [record for record in records if re.search(rf"^{name}", record, re.IGNORECASE)]
    if not matches:
        print("Record not found")
    else:
        print("Record found")
        print("".join(matches))
        confirm = input(f"Confirm to delete {name}? (Y/N): ")
        if confirm.lower() == "y":
            with open("hospital_records.txt", "w") as file:
                for record in records:
                    if not re.search(rf"^{name}", record, re.IGNORECASE):
                        file.write(record)
            print("Record deleted successfully")
            show_record()

def modify_record():
    name = input("Please enter record name: ")
    with open("hospital_records.txt", "r") as file:
        records = file.readlines()
    matches = [record for record in records if re.search(rf"^{name}", record, re.IGNORECASE)]
    if not matches:
        print("Record not found")
          else:
        print("Record found")
        print("".join(matches))
        new_info = input("Enter new information: ")
        with open("hospital_records.txt", "w") as file:
            for record in records:
                if re.search(rf"^{name}", record, re.IGNORECASE):
                    file.write(new_info + "\n")
                else:
                    file.write(record)
        print("Record modified successfully")
        show_record()
        print_menu() #call show menu function
        choice = eval(input("Enter your choice: ")) #read choice

while True:  #loop as ;pmg as choice is not equal to 5
    print_menu()
    choice = input("Enter your choice: ")
    if choice == "1":
        search_record()

    elif choice == "2":
        add_record()

    elif choice == "3":
        delete_record()

    elif choice == "4":
        modify_record()

    elif choice == "5":
        print("Goodbye!")
        break
    else:
        print("Invalid choice. Please try again.")
        choice = int(input("what else would you like to do, make a choice -> "))

