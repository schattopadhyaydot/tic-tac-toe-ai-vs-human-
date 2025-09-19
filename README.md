from tkinter import *
from tkinter import messagebox
import random

# Create main window
root = Tk()
root.title("Tic-Tac-Toe (Human vs Computer)")

count = 0
winner = False

# Function: Human (X) move
def b_clicked(b):
    global count, winner
    if b["text"] == " " and not winner:
        b["text"] = "X"
        count += 1
        check_if_won()
        if not winner and count < 9:
            computer_move()

# Function: Computer (O) move
def computer_move():
    global count, winner
    available = [btn for btn in buttons if btn["text"] == " "]
    if available:
        b = random.choice(available)
        b["text"] = "O"
        count += 1
        check_if_won()

# Function: Check for win/tie
def check_if_won():
    global winner

    combos = [
        [b1, b2, b3], [b4, b5, b6], [b7, b8, b9],  # Rows
        [b1, b4, b7], [b2, b5, b8], [b3, b6, b9],  # Columns
        [b1, b5, b9], [b3, b5, b7]                # Diagonals
    ]

    for combo in combos:
        if combo[0]["text"] == combo[1]["text"] == combo[2]["text"] != " ":
            for b in combo:
                b.config(bg="purple")
            winner = True
            messagebox.showinfo("Tic Tac Toe", f"{combo[0]['text']} wins!")
            disable_all_buttons()
            return

    if count == 9 and not winner:
        messagebox.showinfo("Tic Tac Toe", "It's a Tie!")
        disable_all_buttons()

# Function: Disable all buttons
def disable_all_buttons():
    for b in buttons:
        b.config(state=DISABLED)

# Function: Reset the board
def reset():
    global count, winner
    count = 0
    winner = False
    for b in buttons:
        b.config(text=" ", state=NORMAL, bg="SystemButtonFace")

# --- MANUAL Button creation ---

b1 = Button(root, text=" ", font=("Helvetica", 20), height=4, width=6, bg="SystemButtonFace")
b2 = Button(root, text=" ", font=("Helvetica", 20), height=4, width=6, bg="SystemButtonFace")
b3 = Button(root, text=" ", font=("Helvetica", 20), height=4, width=6, bg="SystemButtonFace")

b4 = Button(root, text=" ", font=("Helvetica", 20), height=4, width=6, bg="SystemButtonFace")
b5 = Button(root, text=" ", font=("Helvetica", 20), height=4, width=6, bg="SystemButtonFace")
b6 = Button(root, text=" ", font=("Helvetica", 20), height=4, width=6, bg="SystemButtonFace")

b7 = Button(root, text=" ", font=("Helvetica", 20), height=4, width=6, bg="SystemButtonFace")
b8 = Button(root, text=" ", font=("Helvetica", 20), height=4, width=6, bg="SystemButtonFace")
b9 = Button(root, text=" ", font=("Helvetica", 20), height=4, width=6, bg="SystemButtonFace")

# Place each button in the grid
b1.grid(row=0, column=0)
b2.grid(row=0, column=1)
b3.grid(row=0, column=2)

b4.grid(row=1, column=0)
b5.grid(row=1, column=1)
b6.grid(row=1, column=2)

b7.grid(row=2, column=0)
b8.grid(row=2, column=1)
b9.grid(row=2, column=2)

# Assign command to each button
b1.config(command=lambda: b_clicked(b1))
b2.config(command=lambda: b_clicked(b2))
b3.config(command=lambda: b_clicked(b3))
b4.config(command=lambda: b_clicked(b4))
b5.config(command=lambda: b_clicked(b5))
b6.config(command=lambda: b_clicked(b6))
b7.config(command=lambda: b_clicked(b7))
b8.config(command=lambda: b_clicked(b8))
b9.config(command=lambda: b_clicked(b9))

# Store buttons in a list (for computer move and reset)
buttons = [b1, b2, b3, b4, b5, b6, b7, b8, b9]

# Add game title and reset button
title = Label(root, text="Tic Tac Toe - Human vs Computer", font=("Helvetica", 14), fg="blue")
title.grid(row=3, column=0, columnspan=3, pady=10)

reset_btn = Button(root, text="Reset Game", font=("Helvetica", 12), command=reset)
reset_btn.grid(row=4, column=0, columnspan=3, pady=10)

# Start the main loop
root.mainloop()
