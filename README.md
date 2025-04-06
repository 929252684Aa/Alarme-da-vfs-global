# Alarme-da-vfs-global
Toca quando a ver mudança
import requests
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

# Função para verificar mudanças na VFS Global
def check_vfs_updates():
    url = "URL_DA_VFS_GLOBAL"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        # Lógica para verificar mudanças nos dados
        if data_changed(data):
            send_alert(data)

# Função para enviar alerta por email
def send_alert(data):
    sender_email = "andrecaiava286@gmail.com"
    receiver_email = "andrecaiava286@gmail.com"
    password = "Muacambumba30@"

    message = MIMEMultipart("alternative")
    message["Subject"] = "Alerta de Mudanças na VFS Global"
    message["From"] = sender_email
    message["To"] = receiver_email

    text = f"Foi detectada uma mudança nos dados: {data}"
    part = MIMEText(text, "plain")
    message.attach(part)

    with smtplib.SMTP_SSL("smtp.gmail.com", 465) as server:
        server.login(sender_email, password)
        server.sendmail(
            sender_email, receiver_email, message.as_string()
        )

# Função para verificar se os dados mudaram
def data_changed(data):
    # Implementar lógica para verificar mudanças nos dados
    return True

# Executar a verificação periodicamente
if __name__ == "__main__":
    check_vfs_updates()
