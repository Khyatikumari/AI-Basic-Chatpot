# LLM-Based Interactive Assistant Chatpot in Google Colab
This project is a Large Language Model (LLM)-based interactive assistant implemented in Google Colab. It allows users to input questions and receive real-time responses from OpenAI's GPT-3.5 model (or GPT-4, if available). The project is designed to be simple, user-friendly, and easily deployable.

## Features
Interactive UI: Uses ipywidgets to create a responsive user interface, making it easy to input questions and view answers.

Real-Time Responses: Utilizes the OpenAI API to get instant responses from the GPT model.

Rate-Limit Handling: Includes error handling for OpenAI API rate limits, with automatic retries.

## Technologies Used
Google Colab: For easy execution in the cloud with an interactive notebook environment.

OpenAI GPT-3.5 / GPT-4: For generating responses.

Python: For logic and API interaction.

Ipywidgets: For creating input fields and buttons in Google Colab.

## Getting Started
### 1. Clone or Download the Colab Notebook
You can run the code directly in Google Colab by copying and pasting the provided Python script. Alternatively, you can upload the .ipynb file to Google Colab.
### 2. Install Dependencies
The required dependencies, including openai and ipywidgets, will need to be installed first. You can do this by running the following commands in the Colab notebook:

!pip install openai
### 3. Input Your OpenAI API Key
import getpass

openai_api_key = getpass.getpass('Enter your OpenAI API key:')

openai.api_key = openai_api_key

## Code Overview
The Key Functions

ask_gpt(question): Sends a request to OpenAI's API and returns a response.

on_button_click(b): A callback function that gets executed when the submit button is clicked.

Widgets: Used for the user interface, including:

widgets.Text for user input.

widgets.Button to trigger the API request.

widgets.Textarea to display the response.
## Error Handling
The code includes basic error handling to catch and manage API rate limits. When the rate limit is exceeded, the system waits 10 seconds and retries the request:
'''
import time

def ask_gpt(question):
    try:
        response = openai.ChatCompletion.create(
            model="gpt-3.5-turbo",
            messages=[{"role": "system", "content": "You are a helpful assistant."},
                      {"role": "user", "content": question}],
            max_tokens=150,
            temperature=0.7,
        )
        return response['choices'][0]['message']['content'].strip()
    except openai.error.RateLimitError:
        print("Rate limit exceeded. Waiting for 10 seconds before retrying...")
        time.sleep(10)
        return ask_gpt(question)
        '''
## Rate Limiting
If you encounter a RateLimitError, check your OpenAI quota at the OpenAI Usage Dashboard. You may need to upgrade your plan or reduce the frequency of requests.

## Future Improvements
Add support for context-aware conversations.

Implement logging for conversations.

Allow the user to select models (GPT-3.5 vs GPT-4) if available.
## License
This project is licensed under the MIT License. 
## Author
Khyati kumari
