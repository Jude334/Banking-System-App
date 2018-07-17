# Banking-System-App
A Python app that acts like a bank. You can display total, make deposit, make withdrawal or change user. It writes the information to a file, but currently it is not pulling information from the file; it only stores it in RAM.

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

	def entry(the_file):
		'''Checks if name/pass are in file,
			if not, it adds it'''
    
		name = input("What is your name?: ") #stores name/pword into file and variable
		pword = input("What is your password?: ")

		tf = open(the_file, "a") #writes name/pword to file
		tf.write(repr(name))
		tf.write("\n")
		tf.write(repr(pword))

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

	def main():
		'''Main loop'''
		print("\t\tWelcome to U-Bank\n")
		f = open_file("D:/PythonProjects/banking.txt", "a") #open file
		login = entry("D:/PythonProjects/banking.txt") #writes name/pword to file
		tot_amount = 0
		new_amount = 0

		again = " "
		while again != "no":
			choice = menu() #display menu, ask to make choice
			if choice == 1: #display total
					print("Your total is: ", tot_amount)
			elif choice == 2:
				new_amount = deposit(tot_amount, "D:/PythonProjects/banking.txt")
				print("Your total is: ", new_amount)
			elif choice == 3:
				new_amount = withdraw(tot_amount, "D:/PythonProjects/banking.txt")
				print("Your total is: ", new_amount)
			elif choice == 4: #enter another name/pword to file
				login = entry("D:/PythonProjects/banking.txt")
				tot_amount = 0
				new_amount = 0
				continue #goes back to top of while loop
			else: #doesn't enter 1 - 4
				print("Not a valid choice...")

			tot_amount = new_amount

			again = input("Would you like to make another transaction?: ")

		print("\nGoodbye")

    
    

	main()
	input("\n\nPress enter to exit")
