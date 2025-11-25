# Alumni-information-and-tracer-system
alumni_list = []
announcements = []

def find_alumni_by_email(email):
for a in alumni_list:
if a["email"] == email:
return a
return None

def alumni_register():
print("\n--- Alumni Registration ---")
name = input("Full Name: ")
email = input("Email: ")
password = input("Password: ")
year = input("Year Graduated: ")
course = input("Course: ")
job = input("Current Job: ")
contact = input("Contact Number: ")

if find_alumni_by_email(email):  
    print("\n[!] Email already exists!")  
    return  

alumni = {  
    "name": name,  
    "email": email,  
    "password": password,  
    "year": year,  
    "course": course,  
    "job": job,  
    "contact": contact,  
    "approved": False  
}  
alumni_list.append(alumni)  
print("\nRegistration successful! Wait for admin approval.")

def alumni_login():
print("\n--- Alumni Log In ---")
email = input("Email: ")
password = input("Password: ")

user = find_alumni_by_email(email)  

if not user:  
    print("\n[!] Account not found.")  
    return  

if user["password"] != password:  
    print("\n[!] Wrong password.")  
    return  

if not user["approved"]:  
    print("\n[!] Account pending approval.")  
    return  

alumni_dashboard(user)

def alumni_dashboard(user):
while True:
print("\n=== Alumni Dashboard ===")
print("1. View Profile")
print("2. Employment Info")
print("3. Survey")
print("4. Announcements")
print("5. Log Out")
choice = input("Choose: ")

if choice == "1":  
        print("\n--- Profile ---")  
        for key, val in user.items():  
            if key != "password":  
                print(f"{key.capitalize()}: {val}")  

    elif choice == "2":  
        print("\nEmployment:", user["job"])  

    elif choice == "3":  
        print("\nSurvey: (Not yet implemented)")  

    elif choice == "4":  
        print("\n--- Announcements ---")  
        if not announcements:  
            print("No announcements.")  
        else:  
            for a in announcements:  
                print("- " + a)  

    elif choice == "5":  
        print("\nLogging out...")  
        return  

    else:  
        print("Invalid choice!")

ADMIN_EMAIL = "admin"
ADMIN_PASS = "admin123"

def admin_login():
print("\n--- Admin Log In ---")
email = input("Admin Username: ")
password = input("Password: ")

if email == ADMIN_EMAIL and password == ADMIN_PASS:  
    admin_dashboard()  
else:  
    print("\n[!] Invalid Admin!")

def admin_dashboard():
while True:
print("\n=== Admin Dashboard ===")
print("1. Approve Alumni")
print("2. View Alumni")
print("3. Post Announcement")
print("4. Log Out")
choice = input("Choose: ")

if choice == "1":  
        approve_alumni()  

    elif choice == "2":  
        view_all_alumni()  

    elif choice == "3":  
        post_announcement()  

    elif choice == "4":  
        print("Logging out...")  
        return  

    else:  
        print("Invalid choice!")

def approve_alumni():
print("\n--- Pending Alumni ---")
pending = [a for a in alumni_list if not a["approved"]]

if not pending:  
    print("No pending accounts.")  
    return  

for i, a in enumerate(pending):  
    print(f"{i+1}. {a['name']} ({a['email']})")  

choice = input("Approve which? (number): ")  

if choice.isdigit():  
    idx = int(choice) - 1  
    if 0 <= idx < len(pending):  
        pending[idx]["approved"] = True  
        print("\nAccount approved!")  
    else:  
        print("Invalid number.")  
else:  
    print("Invalid input.")

def view_all_alumni():
print("\n--- All Alumni ---")
if not alumni_list:
print("No alumni registered.")
return

for a in alumni_list:  
    status = "Approved" if a["approved"] else "Pending"  
    print(f"- {a['name']} | {a['email']} | {status}")

def post_announcement():
print("\n--- Post Announcement ---")
msg = input("Enter announcement: ")
announcements.append(msg)
print("Announcement posted!")

def main_menu():
while True:
print("\n=== MAIN MENU ===")
print("1. Alumni Register")
print("2. Alumni Log In")
print("3. Admin Log In")
print("4. Exit")
choice = input("Choose: ")

if choice == "1":  
        alumni_register()  
    elif choice == "2":  
        alumni_login()  
    elif choice == "3":  
        admin_login()  
    elif choice == "4":  
        print("\nGoodbye!")  
        break  
    else:  
        print("Invalid choice!")

main_menu()
