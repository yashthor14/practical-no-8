# practical-no-8

```python
import tkinter as tk
from tkinter.scrolledtext import ScrolledText
from nltk.chat.util import Chat, reflections

# Define chatbot responses
pairs = [
    [
        r"hi|hello|hey",
        ["Hello! How can I assist you today?", "Hi there! How can I help?"]
    ],
    [
        r"how are you\??",
        ["I'm just a bot, but I'm doing fine! How about you?", "I'm always good! How can I assist?"]
    ],
    [
        r"(.*)your name\??",
        ["I'm a chatbot, here to assist you."]
    ],
    [
        r"bye|goodbye",
        ["Goodbye! Have a great day!", "Bye! Take care!"]
    ],
    [
        r"(.*)",
        ["I'm not sure how to respond to that. Could you rephrase?"]
    ]
]

# Create chatbot
chatbot = Chat(pairs, reflections)

# Function to send messages
def send_message():
    user_input = user_entry.get().strip()
    if not user_input:
        return
    chat_history.insert(tk.END, "You: " + user_input + "\n")
    response = chatbot.respond(user_input)
    chat_history.insert(tk.END, "Bot: " + (response or "Please try again.") + "\n\n")
    chat_history.see(tk.END)
    user_entry.delete(0, tk.END)

# GUI setup
root = tk.Tk()
root.title("Simple Chatbot")
root.geometry("500x500")

# Chat history
chat_history = ScrolledText(root, wrap=tk.WORD, width=50, height=15)
chat_history.pack(padx=10, pady=10, fill=tk.BOTH, expand=True)

# User input
user_entry = tk.Entry(root, width=40)
user_entry.pack(padx=10, pady=5)

# Send button
send_button = tk.Button(
    root,
    text="Send",
    command=send_message
)
send_button.pack(pady=5)

# Press Enter to send message
root.bind("<Return>", lambda event: send_message())

# Run application
root.mainloop()
