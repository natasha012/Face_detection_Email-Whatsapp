import cv2
import numpy as np
model=cv2.CascadeClassifier('haarcascade_frontalface_default.xml')


#to send email
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText
def send_email(user, recipient):
    mail_content = """
    Your face has been detected!!!
    You have logged into your laptop.
    """
    #The mail addresses and password
    sender_address = user
    sender_pass = 'XXXXXXXXXX'
    receiver_address = recipient
    #Setup the MIME
    message = MIMEMultipart()
    message['From'] = sender_address
    message['To'] = receiver_address
    message['Subject'] = 'Log-in detected.'   #The subject line
    #The body and the attachments for the mail
    message.attach(MIMEText(mail_content, 'plain'))
    #Create SMTP session for sending the mail
    session = smtplib.SMTP('smtp.gmail.com', 587) #use gmail with port
    session.starttls() #enable security
    session.login(sender_address, sender_pass) #login with mail_id and password
    text = message.as_string()
    session.sendmail(sender_address, receiver_address, text)
    session.quit()
    print('Mail Sent')
    
    
    
#to send a whatsapp message
from selenium import webdriver
from time import sleep
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.chrome.options import Options
from selenium.webdriver.common.keys import Keys
def whatsapp():
    driver = webdriver.Chrome(ChromeDriverManager().install())
    message='Meha! Tasha has logged in.'
    driver.get("https://web.whatsapp.com/") 
    sleep(20)
    driver.find_element_by_xpath('//span[@title="Megaa"][@dir="auto"]').click()

    driver.find_element_by_xpath('//div[@dir="ltr"][@data-tab="6"][@spellcheck="true"]').send_keys(message, Keys.ENTER)
    print('WhatsApp message has been sent')
    
cap=cv2.VideoCapture(0)
intruder=False
while True:
    ret,photo= cap.read()

    face=model.detectMultiScale(photo)
    if len(face)==0:
        pass
    else:
        x1=face[0][0]
        y1=face[0][1]
        x2= x1+face[0][2]
        y2= y1+face[0][3]

        aphoto=cv2.rectangle(photo,(x1,y1),(x2,y2),[0,255,0],5)
        cv2.imshow('camera is live...',aphoto)
        if cv2.waitKey(100)==13:
            cap.release()
            break
        intruder=True
            
        
cv2.destroyAllWindows()

if intruder==True:
    whatsapp()
    send_email("tashdumdum@gmail.com", "tashavergiskr@gmail.com")
