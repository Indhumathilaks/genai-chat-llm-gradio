## Development and Deployment of a 'Chat with LLM' Application Using the Gradio Blocks Framework

### AIM:
To design and deploy a "Chat with LLM" application by leveraging the Gradio Blocks UI framework to create an interactive interface for seamless user interaction with a large language model.

### PROBLEM STATEMENT:
Develop a user-friendly chatbot application using a large language model (LLM) to assist users with queries and generate conversational responses. The application should feature a responsive design, real-time text exchange, and customizable settings for response quality.
### DESIGN STEPS:

#### STEP 1: Set Up the Environment
Install the necessary libraries (openai, gradio) and verify API access to the LLM.
#### STEP 2: Create the Chat Functionality
Write a function to interact with the LLM using OpenAI's API (or another preferred LLM provider).
#### STEP 3: Design the Gradio Blocks Interface
Use Gradio Blocks to build a structured, multi-component UI with features like:
A text box for user input.
A chat history display.
A clear button to reset the conversation.
#### STEP 4: Deploy and Test
Host the Gradio app locally or on a server.
Test with diverse inputs to ensure robust performance.
### PROGRAM:
```
import gradio as gr
from transformers import AutoModelForCausalLM, AutoTokenizer

# Load the model and tokenizer
model_name = "gpt2"  # Replace with your LLM
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name)

# Function to interact with the model
def chat_with_llm(user_input):
    inputs = tokenizer.encode(user_input, return_tensors="pt")
    outputs = model.generate(inputs, max_length=150, num_return_sequences=1, pad_token_id=tokenizer.eos_token_id)
    response = tokenizer.decode(outputs[0], skip_special_tokens=True)
    return response

# Gradio interface using Blocks
with gr.Blocks() as chat_interface:
    gr.Markdown("### Chat with LLM")
    with gr.Row():
        with gr.Column():
            user_input = gr.Textbox(placeholder="Type your message here...")
            send_button = gr.Button("Send")
        with gr.Column():
            chatbot = gr.Chatbot()
    
    # Define interaction
    send_button.click(chat_with_llm, inputs=user_input, outputs=chatbot)
    
# Launch the interface
chat_interface.launch()
```
### OUTPUT:
![image](https://github.com/user-attachments/assets/db700c47-2846-4f75-b7f3-4152b1f597a0)

### RESULT:
The "Chat with LLM" application was successfully designed and deployed. The Gradio Blocks framework provided a user-friendly interface, ensuring seamless communication with the large language model.
