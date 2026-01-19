import smtplib
from email.message import EmailMessage
import os
from dotenv import load_dotenv
import openai

# Load environment variables
load_dotenv()

EMAIL_ADDRESS = os.getenv("EMAIL_ADDRESS")
EMAIL_PASSWORD = os.getenv("EMAIL_PASSWORD")
OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")

openai.api_key = OPENAI_API_KEY

def generate_email(prompt):
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "system", "content": "You are a helpful email writing assistant."},
            {"role": "user", "content": prompt}
        ]
    )
    return response.choices[0].message.content

def send_email(to_email, subject, body):
    msg = EmailMessage()
    msg["From"] = EMAIL_ADDRESS
    msg["To"] = to_email
    msg["Subject"] = subject
    msg.set_content(body)

    with smtplib.SMTP_SSL("smtp.gmail.com", 465) as server:
        server.login(EMAIL_ADDRESS, EMAIL_PASSWORD)
        server.send_message(msg)

if __name__ == "__main__":
    user_prompt = input("What email do you want to send? : ")
    receiver = input("Receiver email address: ")

    email_body = generate_email(user_prompt)

    send_email(receiver, "AI Generated Email", email_body)

    print("✅ Email sent successfully!")
