# =========================================
# Personal Journal System
# Beginner Friendly Python Project
# =========================================

# Import modules
import os
from datetime import datetime


# =========================================
# Class Creation
# =========================================
class JournalManager:

    # Constructor Method
    # Aa function object create thay tyare automatic call thay che
    def __init__(self):

        # File nu naam store karva mate variable
        self.filename = "journal.txt"

    # =====================================
    # Add Entry Function
    # =====================================
    def add_entry(self):

        try:

            # User pase thi entry levu
            entry = input("\nWrite your journal entry: ")

            # Current date and time levu
            current_time = datetime.now()

            # File ne append mode ma open karvu
            # "a" mode new data add kare che
            file = open(self.filename, "a")

            # File ma data write karvu
            file.write("\n====================\n")

            file.write("Date & Time : ")
            file.write(str(current_time))
            file.write("\n")

            file.write("Entry : ")
            file.write(entry)
            file.write("\n")

            # File close karvu
            file.close()

            print("\nEntry Saved Successfully!")

        # Error handle karva mate
        except Exception as e:
            print("Error:", e)

    # =====================================
    # View All Entries
    # =====================================
    def view_entries(self):

        try:

            # File ne read mode ma open karvu
            # "r" mode file read karva mate use thay che
            file = open(self.filename, "r")

            # Badho data read karvo
            data = file.read()

            # File empty che ke nai check karvu
            if data == "":
                print("\nJournal is Empty!")

            else:
                print("\n===== ALL JOURNAL ENTRIES =====")
                print(data)

            # File close karvu
            file.close()

        # File na hoy to aa error avse
        except FileNotFoundError:
            print("\nJournal File Not Found!")

        except Exception as e:
            print("Error:", e)

    # =====================================
    # Search Entry
    # =====================================
    def search_entry(self):

        try:

            # Search karva mate word levu
            word = input("\nEnter word to search: ")

            # File open karvu
            file = open(self.filename, "r")

            # Badhi lines read karvi
            lines = file.readlines()

            # Match male che ke nai check karva
            found = False

            print("\n===== SEARCH RESULT =====")

            # Loop thi badhi lines check karvi
            for line in lines:

                # Word line ma che ke nai check karvu
                if word.lower() in line.lower():
                    print(line.strip())

                    found = True

            # Koi match na male to
            if found == False:
                print("No matching entry found!")

            # File close karvu
            file.close()

        except FileNotFoundError:
            print("\nJournal File Not Found!")

        except Exception as e:
            print("Error:", e)

    # =====================================
    # Delete Entries
    # =====================================
    def delete_entries(self):

        try:

            # Confirmation levu
            confirm = input(
                "\nDo you want to delete all entries? (yes/no): "
            )

            # User yes lakhse to delete thase
            if confirm.lower() == "yes":

                # File exist kare che ke nai check karvu
                if os.path.exists(self.filename):

                    # File delete karvu
                    os.remove(self.filename)

                    print("\nAll Entries Deleted Successfully!")

                else:
                    print("\nFile does not exist!")

            else:
                print("\nDelete Operation Cancelled!")

        except Exception as e:
            print("Error:", e)

    # =====================================
    # Menu Function
    # =====================================
    def menu(self):

        # Infinite loop
        while True:

            print("\n================================")
            print(" PERSONAL JOURNAL SYSTEM ")
            print("================================")

            print("1. Add New Entry")
            print("2. View All Entries")
            print("3. Search Entry")
            print("4. Delete All Entries")
            print("5. Exit")

            # User input
            choice = input("\nEnter Your Choice: ")

            # Add Entry function call
            if choice == "1":
                self.add_entry()

            # View Entries function call
            elif choice == "2":
                self.view_entries()

            # Search Entry function call
            elif choice == "3":
                self.search_entry()

            # Delete Entry function call
            elif choice == "4":
                self.delete_entries()

            # Program exit
            elif choice == "5":
                print("\nThank You For Using Journal System")
                break

            # Invalid choice
            else:
                print("\nInvalid Choice! Please Try Again.")


# =========================================
# Object Creation
# =========================================

# Class nu object banavyu
obj = JournalManager()

# Menu function call karyu
obj.menu()
