# CODESOFT-
#Rock, paper seijor game 

import tkinter as tk
import random

# Game logic
choices = ["rock", "paper", "scissors"]
user_score = 0
computer_score = 0

def get_computer_choice():
    return random.choice(choices)

def determine_winner(user, computer):
    if user == computer:
        return "It's a tie!"
    elif (user == "rock" and computer == "scissors") or \
         (user == "scissors" and computer == "paper") or \
         (user == "paper" and computer == "rock"):
        return "You win!"
    else:
        return "You lose!"

def play(user_choice):
    global user_score, computer_score
    computer_choice = get_computer_choice()
    result = determine_winner(user_choice, computer_choice)
    if result == "You win!":
        user_score += 1
    elif result == "You lose!":
        computer_score += 1
    result_label.config(
        text=f"Your Choice: {user_choice}\nComputer's Choice: {computer_choice}\n{result}"
    )
    score_label.config(
        text=f"Score - You: {user_score} | Computer: {computer_score}"
    )

def reset_game():
    global user_score, computer_score
    user_score = 0
    computer_score = 0
    result_label.config(text="")
    score_label.config(text=f"Score - You: {user_score} | Computer: {computer_score}")

# GUI setup
window = tk.Tk()
window.title("Rock-Paper-Scissors Game")
window.geometry("400x350")
window.resizable(False, False)

title_label = tk.Label(window, text="Choose Rock, Paper, or Scissors", font=("Arial", 14))
title_label.pack(pady=10)

button_frame = tk.Frame(window)
button_frame.pack(pady=10)

rock_button = tk.Button(button_frame, text="Rock", width=12, command=lambda: play("rock"))
paper_button = tk.Button(button_frame, text="Paper", width=12, command=lambda: play("paper"))
scissors_button = tk.Button(button_frame, text="Scissors", width=12, command=lambda: play("scissors"))

rock_button.grid(row=0, column=0, padx=5)
paper_button.grid(row=0, column=1, padx=5)
scissors_button.grid(row=0, column=2, padx=5)

result_label = tk.Label(window, text="", font=("Arial", 12), fg="blue")
result_label.pack(pady=10)

score_label = tk.Label(window, text=f"Score - You: {user_score} | Computer: {computer_score}", font=("Arial", 12), fg="green")
score_label.pack(pady=5)

play_again_button = tk.Button(window, text="Play Again (Reset Scores)", command=reset_game, bg="lightgray")
play_again_button.pack(pady=5)

exit_button = tk.Button(window, text="Exit", command=window.quit, bg="red", fg="white")
exit_button.pack(pady=10)

window.mainloop()
