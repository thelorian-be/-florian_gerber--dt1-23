# DT1 2023 : Enabling Technologies, Assignment 1 Florian Gerber

I started the DT 1 Assignment with the following setup:

	•	Git installed
	•	Docker installed
	•	Bubble setup 
	•	Huggingface account created

## 1. General installation
The first steps included to get an initial overview of the project by understanding the goal and drawing the architecture diagram (can be seen in architecture-diagramm.pdf). Further i cloned the Github locally and generated the Docker image and pushed it. Then i created the API Key with Huggingface. No Problem so far.

## 2. Create UI
Next I created the UI with the Bubble no-code software. I took the Chatbot from Josh’s tutorial as a template, from there on it was very easy to get this prepared. (Link:  https://youtu.be/ZMmG3HKvSS8?si=ln-IPfM7y9OLO-L7)

## 3. Get the VM to run
This was by far the most challenging part. I first created my GCP Account and followed the steps using this tutorial (Link: https://www.pascallandau.com/blog/gcp-compute-instance-vm-docker/). There are different ways to access the created VM and i wanted to test the access via. terminal using my own created ssh-keys, you can find them in the repository. Installing Docker and running the image did not lead to any issues. 

## 4. Firewall
The firewall settings were difficult. In the end i had to continue without implementing them correctly.

## 5. Code generation
To generate the code with ChatGPT i used the prompt in the repository. Unfortunately, the outcome could not be used successfully and a friend (who used the same prompt for chatGTP to generate) provided me with his code which then worked.

## 6. Solution
The final Solution can be found here Link: https://dt-assignment1.bubbleapps.io/version-test
While accessing, make sure to enable unsafe content in your browser.

