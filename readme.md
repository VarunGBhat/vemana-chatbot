# VEMANA IT Chat Assistant

## Overview

This project is a chatbot application built using Streamlit and Google Generative AI. The chatbot is designed to assist users with information about VEMENA INSTITUTE OF TECHNOLOGY, Bangalore, India. It provides info-rich responses about the college, its branches, infrastructure, vision, and mission, while politely redirecting users to general search engines for queries outside its scope.

## Features

- Warm and engaging responses with relevant emojis.
- Info-rich answers about the college's branches, facilities, vision, and mission.
- Redirect links for further learning.
- Strict adherence to the scope of knowledge.

## Technologies Used

- **Streamlit**: For building the web interface.
- **Google Generative AI**: For generating conversational responses.
- **Python**: Backend programming language.
- **dotenv**: For managing environment variables securely.

## Setup Instructions

1. Install the required Python packages:

   ```
   pip install streamlit google-generativeai python-dotenv
   ```

2. Create a `.env` file in the root directory and add your Google Generative AI API key:

   ```
   GEMINI_API_KEY=your_api_key_here
   ```

3. Run the application:
   ```
   streamlit run chatbot_streamlit.py
   ```

## Usage

- Open the application in your browser.
- Type your question in the chat input box.
- The chatbot will respond with relevant information about VEMENA INSTITUTE OF TECHNOLOGY.

## Response Rules

1. If the user's question fits the scope, the chatbot provides info-rich answers with emojis and redirect links.
2. If the question is outside the scope, the chatbot responds with:
   ```
   "I'm sorry, but I can only discuss VEMENA Institute info. Please use general search engine. 🙏"
   ```

## Links

- [Streamlit Documentation](https://docs.streamlit.io/)
- [Google Generative AI Documentation](https://developers.google.com/generative-ai)
- [VEMENA INSTITUTE OF TECHNOLOGY](https://vemanait.edu.in/index.html)
