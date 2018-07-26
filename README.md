After getting some help on Stackoverflow, I decided to completely redo it. Right now, it works mostly as I want it to. The only problem is that I can't have more than one user/pass/amount block in the file. If I make a deposit, it will wipe out the rest. I'll explain the part in the code.

	#U-Bank
	#user logs in
	#reads user/pass/amount from txt file

	def openFile():
	    '''opens file, parses txt file into dictionary'''
	    data = {}
	    fileName = "D:/PythonProjects/banking.txt"
	    with open(fileName, "r") as fh:
		lines = [line.strip() for line in fh.readlines()]
		for i in range(0, len(lines), 3):
		    data.setdefault(lines[i], {})[lines[i+1]] = lines[i+2]   
	    return data

	def login(data):
	    '''user logs in, checks if matches password in data'''
	    inputName = input("Username: ")
	    inputPassword = input("Password: ")
	    if inputName in data and inputPassword in data[inputName]:
		print("Amount: ", data[inputName][inputPassword])
	    else:
		print("User not found or password incorrect.")
	    return inputName, inputPassword

	def displayTotal(inputName, inputPassword, data):
	    '''displays total for user'''
	    if inputName in data and inputPassword in data[inputName]:
		print("Amount: ", data[inputName][inputPassword])

	def deposit(inputName, inputPassword, data):
	    '''user adds to account'''
	    fileName = "D:/PythonProjects/banking.txt"
	    oldAmount = data[inputName][inputPassword]
	    with open(fileName, "r") as fh:
		if inputName in data and inputPassword in data[inputName]:          
		    depAmount = input("How much do you want to deposit?: ")
		    newAmount = float(oldAmount) + float(depAmount)
		    data[inputName][inputPassword] = newAmount
		    with open(fileName, "w") as wf:
			#Originally, I tried to write both blocks of user/pass/amount to the file,
			#but it would change both blocks to the same name, passord, amount
			wf.write(str(inputName) + "\n" + str(inputPassword) + "\n" + str(newAmount))
	    return newAmount

	def withdraw(inputName, inputPassword, data):
	    '''user subtracts from account'''
	    fileName = "D:/PythonProjects/banking.txt"
	    oldAmount = data[inputName][inputPassword]
	    with open(fileName, "r") as fh:
		if inputName in data and inputPassword in data[inputName]:          
		    depAmount = input("How much do you want to deposit?: ")
		    newAmount = float(oldAmount) - float(depAmount)
		    data[inputName][inputPassword] = newAmount
		    with open(fileName, "w") as wf:
			wf.write(str(inputName) + "\n" + str(inputPassword) + "\n" + str(newAmount))
	    return newAmount

	def menu():
	    '''Display menu, calls function depending on input'''   
	    print('''
		       U-Bank
                
		    Menu
		    1 - Change user
		    2 - Display total
		    3 - Make deposit
		    4 - Make withdrawal
		    5 - Exit
		  ''')
	    choice = int(input("What would you like to do?: (Enter 1 - 5) "))
	    return choice

	def main():
	    data = openFile()
	    user, pword = login(data)
	    while True:
		choice = menu()
		if choice == 1:
		    user, pword = login(data)
		elif choice == 2:
		    total = displayTotal(user, pword, data)
		elif choice == 3:
		    dep = deposit(user, pword, data)
		elif choice == 4:
		    withdr = withdraw(user, pword, data)
		elif choice == 5:
		    print("Good-bye")
		    break


	main()  


	input("\n\nPress enter to exit")
