please write me a javascript code to be inserted in the HTML element of my front end in Bubble to do the following: call the hugging face inference API: 

https://api-inference.huggingface.co/models/gpt2 

with the following token “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”.
The input, the user message, comes from an input field in the page which has the ID attribute "chat_input"
The output is to be written in an HTML element which ID is "chat_output", concatenated with the input at the beginning and with a space between them. the message should be sent when the button with ID "chat_submit" is clicked.
All the HTML elements already exist in the front end, don’t' create them 
The IP address of my VM is 34.65.1.120, and the port is 5000. 
I want to make the call to hugging face from the docker container in the VM in google cloud. The main file of the docker contains the following code in python:

from flask import Flask, request as req, jsonify
import requests
import logging
import os

app = Flask(__name__)


def query(payload, model_id, api_token):
    headers = {"Authorization": f"Bearer {api_token}"}
    api_url = f"https://api-inference.huggingface.co/models/{model_id}"
    response = requests.post(api_url, headers=headers, json=payload)
    return response.json()


@app.route("/chat")
def call_huggingface_chat_model():
    model_id = req.args.get("model_id")
    logging.debug(f"The model ID for the Huggingface model is {model_id}")
    huggingface_token = req.args.get("huggingface_token")
    logging.debug(f"Huggingface API Token: {huggingface_token}")
    questions = req.args.get("input")
    data = query(
        {
            "inputs": f'{questions.replace("_"," ")}',
            "options": {"wait_for_model": True},
            "parameters": {"return_full_text": False, "max_time": 30},
        },
        model_id,
        huggingface_token,
    )
    logging.debug(f"Model output: {data}")
    output = jsonify({"ack": data[0]["generated_text"]})
    output.headers.add("Access-Control-Allow-Origin", "*")
    return output


@app.route("/load_model")
def load_huggingface_chat_model():
    model_id = req.args.get("model_id")
    logging.debug(f"The model ID for the Huggingface model is {model_id}")
    huggingface_token = req.args.get("huggingface_token")
    logging.debug(f"Huggingface API Token: {huggingface_token}")
    data = query(
        {
            "inputs": "hello",
            "parameters": {"return_full_text": True},
        },
        model_id,
        huggingface_token,
    )
    logging.debug(f"Model output: {data}")
    output = {}
    if "generated_text" in data[0]:
        output = jsonify({"ack": "model loaded and ready"})
    else:
        output = jsonify({"ack": data[0][list(data[0].keys())[0]]})
    output.headers.add("Access-Control-Allow-Origin", "*")
    return output


@app.route("/ping")
def ping():
    output = jsonify({"ack": "pong"})
    output.headers.add("Access-Control-Allow-Origin", "*")
    return output


if __name__ == "__main__":
    port = int(os.environ.get("PORT", 5000))
    app.run(debug=True, host="0.0.0.0", port=port)
