# Banking-System-App
A Python app that acts like a bank. You can display total, make deposit, make withdrawal or change user. It writes the information to a file.


	
	#Bank System
	#stores username and passwords in plain text file
	#if user enters correctly, can use the app
	#allows user to make deposits
	#and withdrawals
	#keeps track of total amount

	import sys

	def open_file(file_name, mode):
	    '''Opens a file if exists, if not, exits'''
	    try:
		the_file = open(file_name, mode)
	    except IOError as e:
		print("Unable to open the file", file_name, "Ending program.\n", e)
		input("\n\nPress enter to exit")
		sys.exit()
	    else:
		return the_file

	def next_line(the_file): #added a function that reads the next line and strips it
	    '''Returns the next line from the_file'''
	    line = the_file.readline()
	    line = line.rstrip()
	    return line

	def next_block(the_file): #added a function that gets the next block of user, pass, amount
	    user = next_line(the_file)
	    password = next_line(the_file)
	    amount = next_line(the_file)
	    return user, password, amount

	def entry(the_file):
	    '''Checks if name/pass are in file,
		if not, it adds it'''

	    name = input("What is your name?: ") #stores name/pword into file and variable
	    pword = input("What is your password?: ")

	    tf = open(the_file, "a") #writes name/pword to file
	    tf.write(repr(name))
	    tf.write("\n")
	    tf.write(repr(pword))
	    tf.write("\n")        
	    return name, pword

	def menu():
	    '''Display menu, check user input, calls function depending
		on input'''

	    print('''
			Menu

		    1 - Display total
		    2 - Make deposit
		    3 - Make withdrawal
		    4 - Change user
		  ''')

	    choice = int(input("What would you like to do?: (Enter 1 - 4) "))

	    return choice #returns choice to program 
    
	def deposit(tot_amount, the_file):
	    '''Asks for deposit amount, adds to total,
	       writes total to file, returns total '''
	    dep_amount = float(input("How much would you like to deposit?: "))
	    tot_amount += dep_amount
	    tf = open(the_file, "a")
	    tf.write(repr(tot_amount))
	    tf.write("\n")
	    tf.close()
	    return tot_amount

	def withdraw(tot_amount, the_file):
	    '''Ask for withdrawal amount, returns it, subtract from total'''
	    with_amount = float(input("How much would you like to withdraw?: "))
	    tot_amount -= with_amount
	    tf = open(the_file, "a")
	    tf.write(repr(tot_amount))
	    tf.write("\n")
	    tf.close()    
	    return tot_amount

	#for now, I am not going to write to the file
	#I want to make sure I can read from it and switch blocks properly
	def main():
	    '''Main loop'''
	    print("\t\tWelcome to U-Bank\n")
	    f = open_file("D:/PythonProjects/banking.txt", "r") #open file
	    user, password, amount = next_block(f)
	    #login = entry("D:/PythonProjects/banking.txt") #writes name/pword to file
	    print(user, password, amount)
	    name = input("Username: ")
	    pword = input("Password: ")
	    if name == user and pword == password:
		print(amount)
    
	    again = " "
	    while again != "no":
		choice = menu() #display menu, ask to make choice
		if choice == 1: #display total  
		    print("Your total is: ", amount)
		elif choice == 2:
		    new_amount = deposit(tot_amount, "D:/PythonProjects/banking.txt")
		    print("Your total is: ", amount)
		elif choice == 3:
		    new_amount = withdraw(tot_amount, "D:/PythonProjects/banking.txt")
		    print("Your total is: ", new_amount)
		elif choice == 4: #enter another name/pword to file
		    user, password, amount = next_block(f)
		    print(user, password, amount)
		    name = input("Username: ")
		    pword = input("Password: ")
		    if name == user and pword == password:
			print(amount)
			continue
		else: #doesn't enter 1 - 4
		    print("Not a valid choice...")

        again = input("Would you like to make another transaction?: ")

    print("\nGoodbye")

    
    

	main()
	input("\n\nPress enter to exit")
    


    
    

