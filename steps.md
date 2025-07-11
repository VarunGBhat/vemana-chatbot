# Step 1: Create a New Project Folder

1. Open File Explorer or Command Prompt / Terminal.
2. Navigate to the location where you want your project.
3. Run:
   ```bash
   mkdir streamlit-gemini-app
   cd streamlit-gemini-app
   ```

# Step 2: Initialize Python Virtual Environment

1. Run this command to create the virtual environment:
   ```bash
   python -m venv venv
   ```
2. Activate it (for PowerShell):
   ```bash
   .\venv\Scripts\Activate.ps1
   ```
   If using Command Prompt (cmd), use:
   ```bash
   venv\Scripts\activate.bat
   ```

# Step 3: Install Required Packages

Run the following:

```bash
pip install streamlit python-dotenv google-generativeai
```

# Step 4: Create Your Python File

1. Create a new file named, for example, `app.py`.
2. Open it in any code editor (like VS Code).

# Step 5: Generate the prompt for the chatbot

1. Open copilot.
2. Change the model to deep research.
3. Paste the following prompt:

   ```
   now you behave as an prompt engineer, who have a huge experience in this field. and you are an expert in generating the prompts at industrial standards with a ton of creativity filled in it.
   If any other information is required from my side please ask me that and after getting all the information give me the prompt
   now your task is to generate me a prompt to give an llm so that i can retrive only required data and if i ask any irrelavent question after giving that prompt it should politely tell to use search engines.
   and this prompt i will be using in a chatbot for a college and it should retrive only the school data And for more information it should provide the redirecting link so that the user can go to that link and do more research
   the prompt should answerr to the following details
   the school name is VEMENA INSTITUE of TECHNOLOGY it is a college in Bangalore Bearing
   the college code for CET -> E092 and for COMED-K -> E145
   Having the following branches:
   ->Computer Science and Engineering
   ->Information Science and Engineering
   ->Electronics and Communication Engineering
   ->Mechanical Engineering ->Civil Engineering
   ->Basic Science ->Artificial Inteligence and Machine Learning
   ->Computer Science and Data Science
   ->Computer Science and Cyber Security

   The college has a good infrastructure and facilities The college also include a good hostel facility, Library
   The college encourages for Sports NCC NSS Cultural activites
   The college also has a student club and commitees to look after
   Colleges mission and Vision
   -->
   Vision of the Institute To become a leading institute by providing quality technical education and research with ethical values.
   Mission Statements: To continually improve quality education system that produces thinking engineers having good technical capabilities with human values. To nurture a good eco-system that encourages faculty and students to engage in meaningful research and development. To strengthen industry institute interface for promoting team work, internship and entrepreneurship. To enhance educational opportunities to the rural and weaker sections of the society to equip with practical skills to face the challenges of life.
   <--

   Use a friendly and engaging tone, incorporating relevant emojis and expressions to enhance the user experience

   Links:
   link landing page -- https://vemanait.edu.in/index.html
   ->Computer Science and Engineering -- https://vemanait.edu.in/computer-science-and-engineering.html
   ->Information Science and Engineering -- https://vemanait.edu.in/information-science-and-engineering.html
   ->Electronics and Communication Engineering -- https://vemanait.edu.in/electronics-and-communication-engineering.html
   ->Mechanical Engineering -- https://vemanait.edu.in/mechanical-engineering.html
   ->Civil Engineering -- https://vemanait.edu.in/civil-engineering.html
   ->Basic Science -- https://vemanait.edu.in/basic-science.html
   ->Artificial Inteligence and Machine Learning -- https://vemanait.edu.in/artificial-intelligence-and-machine-learning.html
   ->Computer Science and Data Science -- https://vemanait.edu.in/data-science.html
   ->Computer Science and Cyber Security -- https://vemanait.edu.in/cyber-security.html Hods
   ->Computer Science and Engineering -- Dr. Ramakrishna M
   ->Information Science and Engineering -- Dr. Rajanna M
   ->Electronics and Communication Engineering -- Dr. Parameshwara M C
   ->Mechanical Engineering -- Dr. Vijayasimha Reddy B.G.
   ->Civil Engineering -- Mrs. Elavarasi. V
   ->Basic Science
   ->Artificial Inteligence and Machine Learning -- Dr. Kantharaju H.C
   ->Computer Science and Data Science
   ->Computer Science and Cyber Security

   Principal -- Dr. Vijayasimha Reddy B.G.

   College location
   -- >
   #1 Mahayogi Vemana Road,
   3rd Block, Kormangala,
   Bengaluru-560 034.
   < --
   College Trust -- About Karnataka ReddyJana Sangha

   Management committee ->
   1 SRI. S. JAYARAMA REDDY PRESIDENT
   2 SRI. D.N. LAKSHMANA REDDY VICE PRESIDENT
   3 SRI. K.N. KRISHNA REDDY VICE PRESIDENT
   4 SRI. V.VENKATASHIVA REDDY VICE PRESIDENT
   5 SRI. N. SHEKAR REDDY GENERAL SECRETARY
   6 SRI. N. SOMASHEKAR REDDY JOINT SECRETARY
   7 SRI. K.R. NAGARAJA REDDY JOINT SECRETARY
   8 SRI. A.M. SRINIVASA REDDY JOINT SECRETARY
   9 SRI. M. CHANDRA REDDY TREASURER
   ```

4. Copy the response from copilot and save it in some place.

# Step 6: Create the chatbot code

1. Paste the following code in the file created:

   ```python
   import streamlit as st
   import google.generativeai as genai
   import os
   from dotenv import load_dotenv

   load_dotenv()

   genai.configure(api_key=os.getenv('GEMINI_API_KEY'))

   generation_config = {
       "temperature": 0.7,
       "top_p": 0.85,
       "top_k": 40,
       "max_output_tokens": 400,
   }

   model = genai.GenerativeModel(
       model_name="gemini-2.0-flash",
       generation_config=generation_config
   )
   SYSTEM_PROMPT = """ Paste the prompt given by copilot """
   st.set_page_config(page_title="VEMANA IT Chat", page_icon="🤖")
   st.title("🤖 VEMANA IT Chat Assistant")

   if "messages" not in st.session_state:
       st.session_state.messages = [
           {"role": "assistant", "content": "Hello! How can I help you today?"}
       ]

   for message in st.session_state.messages:
       with st.chat_message(message["role"]):
           st.markdown(message["content"])

   if prompt := st.chat_input("Type your question here..."):

       st.session_state.messages.append({"role": "user", "content": prompt})

       with st.chat_message("user"):
           st.markdown(prompt)

       full_prompt = f"{SYSTEM_PROMPT}\n\n:User  {prompt}"

       with st.chat_message("assistant"):
           response_placeholder = st.empty()
           full_response = ""

           response = model.generate_content(
               full_prompt,
               stream=True
           )

           for chunk in response:
               full_response += chunk.text
               response_placeholder.markdown(full_response + "▌")

           response_placeholder.markdown(full_response)

       st.session_state.messages.append({"role": "assistant", "content": full_response})

   ```

2. Create a .env file and paste the below code:

   ```
   GEMINI_API_KEY = “your_gemini_api_key"
   ```

# Step 7: Create a Gemini API key

1. Go to google ai studio.
2. Click on generate api.
3. Copy the api key.
4. Paste the api key in the place of “your_gemini_api_key”.
5. Make sure the api key is in double quotes.

# Step 8: Run the Streamlit App

In the terminal (make sure you're still in the virtual environment), run:

```bash
streamlit run app.py
```
