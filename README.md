# ResumeRefinerAIAgentusingn8n
Trigger on form submission (collect resume file, job link, and user email).
Grab resume and job data and send a prompt to an OpenAI model to tailor the resume to the job posting.
Email the resume revision suggestions back to the user.

1. Workflow Diagram in Draw.io
<img width="543" height="250" alt="Screen Shot 2025-07-26 at 6 55 32 PM" src="https://github.com/user-attachments/assets/c4a0022a-7903-4d1b-b7eb-12b591e36ab1" />

2. The details page for the node called "On form submission" of type Form Trigger. This is the configuration page for the Form Trigger node. Here, we set up a form that users can fill out, which will then trigger the start of the workflow in n8n. The Form Trigger node creates a web form with fields we define (in this case: Resume, Job, and Email). When someone submits this form, it starts (triggers) the workflow and passes the submitted data into the workflow for further processing. We can use this to collect information, files, or any input from users and automate actions based on their submissions. <br>
<img width="1875" height="884" alt="Collector First Form Submission" src="https://github.com/user-attachments/assets/dc48f4ff-e408-4d47-bfeb-7b240d172a12" />
3.  inside the "Extract from File" node, which is used to extract data from a file (such as a PDF, CSV, Excel, or other formats). In this case, this node is set to extract data from a PDF file found in the binary property named "Resume".The extracted data is converted to JSON.
<img width="1888" height="842" alt="Screen Shot 2025-07-26 at 5 06 35 PM" src="https://github.com/user-attachments/assets/8e7bd7f8-a768-4866-b119-b1844ce0ead6" />
4. UI to upload resume <br>
<img width="624" height="770" alt="Screen Shot 2025-07-26 at 4 51 29 PM" src="https://github.com/user-attachments/assets/816f4e3e-600e-4efd-9abc-e14c97f11f09" />

5. On the details page for the "AI Agent" node in n8n. This page allows you to configure the "AI Agent" node. The "AI Agent" node is used to interact with AI models (like GPT) to perform advanced tasks. In this current setup, the node is configured to help refine resumes based on a specific job opportunity by: <br>
- Reviewing the applicant’s resume and the job description. <br>
- Summarizing the company and role.<br>
- Analyzing the resume for strengths and missing skills.<br>
- Suggesting targeted improvements for the resume. <br>
<img width="1445" height="703" alt="Screen Shot 2025-07-26 at 7 14 38 PM" src="https://github.com/user-attachments/assets/723dc06a-cd2b-4ae6-925c-50a696b48a6c" />

6. The details page for the node called "OpenAI Chat Model". This is the configuration page for the "OpenAI Chat Model" node, on this page, we set up how the "OpenAI Chat Model" node will interact with OpenAI's GPT models (like gpt-3.5-turbo). We can choose which model to use and configure options for how the AI should respond. <br>
<img width="1105" height="442" alt="Screen Shot 2025-07-26 at 7 22 17 PM" src="https://github.com/user-attachments/assets/fa4ad020-a25d-4562-9c7b-88ff16226e9e" />

7. This is the details page for the node called "Structured Output Parser" which is the configuration page for the "Structured Output Parser" node. It is used to take the output from an AI model (such as OpenAI or other language models) and convert it into a structured JSON format based on a schema we define. In our current setup, the node is configured to: <br>
- Parse AI output into a JSON object that contains: <br>
- An array called resumeCorrections, where each item includes details like the section of the resume, the original and corrected text, an explanation, and the type of correction. <br>
- A summary string for recommendations or a brief overview.<br>
<img width="1129" height="617" alt="Screen Shot 2025-07-26 at 7 26 26 PM" src="https://github.com/user-attachments/assets/611c3169-da9f-4871-b603-566210fc9f24" />

8. This is the configuration page for the "Send a message" Gmail node. Here, you set up how n8n will send an email using the connected Gmail account. The purpose of this page is to: <br>
- Allow you to specify the details of the email you want to send (such as recipient, subject, and message body).
- Configure options for sending emails as part of your automated workflow. <br>
<br>
(The workflow isn’t running because the Gmail node’s authentication token is no longer valid. This means n8n can’t connect to Gmail to send emails.)<br> 
<img width="1026" height="590" alt="Screen Shot 2025-07-26 at 7 31 31 PM" src="https://github.com/user-attachments/assets/857fd44b-9fd3-4786-89aa-983fa01c678c" />
(The workflow isn’t running because the Gmail node’s authentication token is no longer valid. This means n8n can’t connect to Gmail to send emails.)<br> 
<img width="1217" height="555" alt="Screen Shot 2025-07-26 at 7 41 02 PM" src="https://github.com/user-attachments/assets/ab1d6d23-6efd-48f1-936f-d539a6878ed1" />

----------------------------------------------------------------------------------
1. What approach did you take to design your agent?
I started with a Form Trigger node to collect user input (resume, job description, and email).
The workflow then uses an AI Agent node to analyze the resume against the job description, following a structured prompt to ensure the AI’s output is relevant and actionable.
I included a Structured Output Parser node, which converts the AI’s response into a predictable JSON format.
Finally, the workflow sends the results via email using the Gmail node.

2. What challenges did you face in parsing, formatting, or integrating?
Formatting Consistency: Ensuring the AI always followed the expected format (especially for JSON) required careful prompt engineering and validation.

3. How did you ensure that the AI returned JSON reliably?
To ensure reliable JSON output from the AI:
I provided explicit instructions in the AI prompt, asking it to respond strictly in JSON format and specifying the exact schema required.
I used the Structured Output Parser node in n8n, which validates and parses the AI’s response according to the defined schema.
I tested the workflow with multiple examples to confirm that the AI consistently returned valid JSON.

4. What issues did you encounter and how did you resolve them?
I encountered problems with expired or invalid tokens when connecting to Gmail. This can be resolved by re-authenticating the Gmail credentials in n8n and ensuring the account had the necessary permissions.

5. What might you improve or add in future iterations?
- User Feedback: <br>
Provide instant feedback to users after form submission, such as a confirmation message or a summary of their submission. 
- Additional Integrations: <br> 
Add more integrations, such as storing results in a database, sending notifications via Slack, or connecting to HR systems.





