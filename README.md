# Applicant Tracking System Automation  

This UiPath project automates the registration and interaction process for Employees and Employers, providing functionality for resume scoring, job preparation assistance, and employer management.  

## Features  

- **Employee Registration:**  
  Employees can register by providing their personal and educational details. After registration, they receive a confirmation email and gain access to an intelligent chatbot.  
- **Employer Registration:**  
  Employers can register and receive a confirmation email.  
- **Resume Scoring and Job Preparation:**  
  Employees can use a Gemini-based chatbot to score their resumes and get guidance on job preparation based on a provided job description.  

## Workflow  

### Registration  

1. **User Type Selection:**  
   - User selects either `Employee` or `Employer`.  

2. **Input Fields for Employee:**  
   - Title (`Mr/Mrs/Miss`)  
   - Name  
   - Email  
   - Phone Number  
   - Date of Birth (DOB)  
   - College  
   - Degree  
   - CGPA  
   - Graduation Year  
   - Internships  

3. **Input Fields for Employer:**   
   - Company Name  
   - Email  
   - Phone Number
   - Company Address
   - Job Profile
   - Pay Scale
   - Job Location
   - Interview Date
   - Training Period  

4. **Data Storage:**  
   - Details are stored in a Data Table element.  
   - Data is appended to an Excel file.  

5. **Feedback to User:**  
   - Displays messages:  
     - "Thank you for your application. We will reach out to you soon."  
     - "An email has been sent to your mentioned email for confirmation."  

6. **Excel to PDF Conversion:**  
   - Converts the registration data in the Excel file to a PDF for future reference.  

7. **Email Confirmation:**  
   - Sends a confirmation email using the SMTP function:  
     - **To:** Employee's email.  
     - **Subject:** A customizable subject line.  
     - **Body:** Includes title, name, and a message about their application.  

### Chatbot Interaction for Employees  

1. **Resume Scoring:**  
   - Employees can interact with a Gemini-based chatbot to score their resumes.  
   - The chatbot evaluates the resume against pre-fed job descriptions.  
   - Workflow:  
     - Reads an `InputPrompt.txt` containing a chatbot prompt (JSON format).  
     - Appends the resume text to the prompt.  
     - Sends the combined prompt as an HTTP POST request to the chatbot API.  
     - Receives and deserializes the JSON response from the chatbot.  
     - Displays the chatbot's response.  
     - Asks, "Is your chat done?"  
       - If `Yes`, the loop ends.  
       - If `No`, the loop continues.  

2. **Job Preparation Assistance:**  
   - Employees can input specific queries related to job preparation.  
   - Workflow is similar to resume scoring, referencing the `inputprompt2.txt` file containing prompts for job preparation assistance.  

### Employer Functionality  

- Registration follows the same process as Employees, except no chatbot functionality is provided.  

## Configuration  

### Setting up SMTP for Email  

1. Click on the **SMTP Function** in the workflow.  
2. In the **Properties** panel on the right, navigate to the **Logon** section:  
   - **Email:** Enter your 2FA-enabled Gmail address.  
   - **Password:** Use an app password generated from Gmail.  
3. To generate an app password:  
   - Go to Gmail **Security Settings**.  
   - Search for "App Password" and follow the steps provided on the website to generate one.  

### Setting up the HTTP Request for Chatbot Interaction  

1. Click on **Configure** in the HTTP Request activity.  
2. Enter the API endpoint generated from **Google AI Studio**.  
3. Use the **POST** method and set the response format to **JSON**.  
4. In the **Properties** panel on the right, under the **Options** section:  
   - For **Body**, use the variable storing the prompt and resume text (e.g., `GenAiBody`).  
   - For **Output**, store the response in a variable to display the Gemini chatbot's response.  
5. If a timeout error occurs due to busy Gemini servers, adjust the **Timeout** setting in the configuration options.  

## Prerequisites  

- UiPath Studio installed.  
- 2FA enabled email with **App Password**
- API endpoint and key for the Gemini-based chatbot or any other prefered AI agent.  
- Predefined prompts in `InputPrompt.txt` and `inputprompt2.txt` for chatbot interactions.  

## File Structure  

- **Main.xaml**: Contains the main workflow logic.  
- **InputPrompt.txt**: JSON file with chatbot prompts for resume scoring.  
- **inputprompt2.txt**: JSON file with chatbot prompts for job preparation.  
- **Employee.xlsx**: Excel file storing registration details.  
 - **Employer.xlsx**: Excel file storing registration details.   

## How to Run  

1. Open the project in UiPath Studio.  
2. Run the workflow **Main.xaml**.
3. Configure SMTP settings in the `Send Email` activity.  
4. Update API endpoint details in the HTTP request activity.  
5. Follow the on-screen prompts for registration and interaction.  

---  
