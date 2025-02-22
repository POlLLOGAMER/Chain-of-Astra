# Chain-of-Astra
Chain of astra is a type of meta architecture adapted to intensive cognitive reasoning, by analyzing the response of a chain of thought model, improving its response and analyzing it, as many times as you want.

This has a zero point threshold, which will depend on the question, this is the maximum point to which you can improve the question. Once you have passed this point, your reasoning capacity will be so great that it will be incomprehensible to understand it, in addition to telling yourself that you can't do it anymore, and analyze why you can't do it anymore in such a compact and abstract way that no human could understand its complexity of the reason why the last iteration before the threshold point is so perfect of point zero.

Heres the code of Chain of Astra:

```
!pip install -U -q "google-generativeai>=0.8.2"
import os
import google.generativeai as genai
os.environ["API_KEY"] = ""

# Configuration of the API using the newly set variable.
genai.configure(api_key=os.environ["API_KEY"])

# Create the model
generation_config = {
    "temperature": 0.7,
    "top_p": 0.95,
    "top_k": 64,
    "max_output_tokens": 65536,
    "response_mime_type": "text/plain",
}

model = genai.GenerativeModel(
    model_name="gemini-2.0-flash-thinking-exp-01-21",
    generation_config=generation_config,
)

# Function that processes the chat with the "astra convination"
def astra_chat(input_text, astra_number):
    chat_session = model.start_chat(history=[])

    # First message
    response = chat_session.send_message(input_text)
    print("Initial response:", response.text)

    # Process the response multiple times according to the number of astra_number
    for i in range(astra_number):
        input_text = f"Improve this response: {response.text}"
        print(f"\n--- Iteration {i+1} ---")
        response = chat_session.send_message(input_text)
        print(response.text)

# Initial input
input_text = "Enter your initial question here"
# Ask for the number of astra convination (how many times we want the model to process the response)
astra_number = int(input("How many times do you want to improve the response?"))

# Call the function with the input and the number of times
astra_chat(input_text, astra_number)

```
## Instructions
In os.environ["API_KEY"] = "" You have to put your API. And in input_text = "Enter your initial question here" your question
