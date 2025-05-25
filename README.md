# 💌 Girlfriend Grievance Portal

A fun grievance portal built using Flask, Python, and SQLite for managing grievances between users. The portal allows users to submit grievances, while administrators can respond to them, track their resolution, and send email notifications.

## 🌐 Features

- User authentication for both user and administrator
- Submit grievances with title, description, mood, and priority
- View grievances and their resolution status
- Admin dashboard to manage grievances and send responses
- Email notifications to both admins and users
- Docker support for easy deployment
- Traefik integration for reverse proxy and SSL

## 🛠️ Technologies Used

- **Backend:** Python 3.10, Flask
- **Database:** SQLite
- **Frontend:** HTML, CSS (Bootstrap)
- **Email Service:** Gmail SMTP
- **Container:** Docker
- **Reverse Proxy:** Traefik

## 🚀 Quick Start with Docker

### Prerequisites

- Docker and Docker Compose installed
- Traefik already set up and running
- A domain name pointing to your server (for SSL)

### Directory Structure
```
/root
├── docker-compose.yml (Traefik compose file)
├── traefik/
│   └── ... (Traefik config files)
└── grievance-portal/
    ├── app.py
    ├── requirements.txt
    ├── Dockerfile
    ├── docker-compose.yml
    ├── .env
    ├── data/          # For database persistence
    └── ... (other portal files)
```

### Setup Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/your-username/girlfriend-grievance-portal.git
   cd girlfriend-grievance-portal
   ```

2. **Create Data Directory**
   ```bash
   mkdir -p data
   ```

3. **Configure Environment Variables**
   Create a `.env` file with the following variables:
   ```env
   EMAIL_ADMIN=your.email@gmail.com
   EMAIL_PASS=your-app-password
   EMAIL_DEFAULT_SENDER=your.email@gmail.com
   EMAIL_USER_RECEIVER=user.email@gmail.com
   USER_NAME=girlfriend
   USER_PASSWORD=user123
   ADMIN_NAME=boyfriend
   ADMIN_PASSWORD=admin123
   PORTAL_URL=https://your-domain.com
   ```

4. **Build and Run**
   ```bash
   docker-compose up -d
   ```

5. **Access the Portal**
   Visit `https://your-domain.com`

## 📧 Gmail Setup

1. Enable 2-Step Verification in your Google Account
2. Generate an App Password:
   - Go to Google Account → Security
   - Under "2-Step Verification", click on "App passwords"
   - Select "Mail" and your device
   - Use the generated password as `EMAIL_PASS`

## 🔒 Security Considerations

- Change default passwords in the .env file
- Use strong passwords for both user and admin accounts
- Keep system and Docker images updated
- Regularly backup your database
- Never commit .env file to version control

## 📦 Database Backup

```bash
# Create backup directory
mkdir -p backups

# Backup database
docker cp grievance-portal:/app/data/grievances.db ./backups/grievances.db.$(date +%Y%m%d)
```

## 🔄 Updating

```bash
# Pull latest changes
git pull

# Rebuild and restart
docker-compose down
docker-compose up -d --build
```

## 🐛 Troubleshooting

1. Check container logs:
   ```bash
   docker-compose logs -f
   ```

2. Verify container status:
   ```bash
   docker ps
   ```

3. Check network connectivity:
   ```bash
   docker network inspect traefik-public
   ```

4. Common Issues:
   - Database permissions: Ensure the data directory has proper permissions
   - Email issues: Verify Gmail app password and 2FA settings
   - Traefik routing: Check domain configuration and SSL certificates

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

---

## 📄 Clone This Repo Into Your Own GitHub (For Beginners)

Want to customize or privately host your own version of this project? Here's how you can copy it to your GitHub:

1. **Visit the Original Repo**: Sign in to Github and navigate to the original repo here:  
   `https://github.com/iamcvam/girlfriend-grievance-portal`
2. **Click "Fork"** (top-right corner):  
   This will create a copy of the project in your own GitHub account.
3. **(Optional) Rename the Repository**:  
   After forking, go to the "Settings" tab of your new repo and change the name if you like.
4. You now have your own private/public version of the code to deploy and modify!

---

## 🖼️ How to Add Images

Want to personalize the portal by adding your own images (like custom banners or cute icons)? It's easy!

1. Go to the project folder.
2. Open the `static/images/` directory. This is where all your image files are stored.
3. Copy and paste your image file into that folder.
4. Replace `home_image.webp` with the image of your choice, and so on for all the images. Do not rename the images, just replace them.

That's it! The image will now be displayed on the page.

---

## 💻 Want to Run Locally? (Optional for Devs)

### Prerequisites

- Python 3.x
- pip (Python package manager)

### Steps

1. **Clone the repository:**

   ```bash
   git clone https://github.com/your-username/girlfriend-grievance-portal.git
   cd girlfriend-grievance-portal
   ```

2. **Create and activate a virtual environment:**

   ```bash
   python3 -m venv venv
   source venv/bin/activate  # For Linux/Mac
   .\venv\Scripts\activate   # For Windows
   ```

3. **Install required dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables:**

   Edit the `.env` file in the root of the project and add the following:

    ```env
    # Gmail address to send notifications from (admin)
    EMAIL_ADMIN=admin.email@example.com

    # App-specific password generated from your Gmail account
    EMAIL_PASS=yourapppassword

    # The default sender for outgoing emails (usually same as EMAIL_ADMIN)
    EMAIL_DEFAULT_SENDER=admin.email@example.com

    # Recipient email address for user (the person submitting grievances)
    EMAIL_USER_RECEIVER=user.email@example.com

    # Username and password for user (grievance submitter)
    USER_NAME=girlfriend
    USER_PASSWORD=user123

    # Username and password for admin (responder)
    ADMIN_NAME=boyfriend
    ADMIN_PASSWORD=admin123

    # Your hosted app URL (used in email templates)
    PORTAL_URL=http://your-grievance-portal-url
    ```
   - Replace `admin.email@example.com` and `user.email@example.com` with your actual Gmail credentials.
   - Replace `girlfriend` and `boyfriend` with user and admin display names respectively, as desired. Similarly with their corresponding passwords.
   - The `EMAIL_PASS` should be your Gmail app password (not your Google account password).

    To generate a Gmail app password:  
    - Visit [Google App Passwords](https://myaccount.google.com/apppasswords)
    - Generate a 16-character password and paste it as `EMAIL_PASS`

5. **Initialize the database:**

   ```bash
   python
   >>> from app import init_db
   >>> init_db()
   ```

   This will create the necessary SQLite database for storing grievances.

6. **Run the application:**

   ```bash
   flask run
   ```

   The portal should now be running at `http://localhost:5000`.

## Usage

1. **Login:**
   - Regular users can log in with the `USER_NAME` and `USER_PASSWORD`.
   - Administrators can log in with the `ADMIN_NAME` and `ADMIN_PASSWORD`.

2. **Submit Grievance:**
   - After logging in, regular users can submit grievances with a title, description, mood, and priority.

3. **Admin Dashboard:**
   - Administrators can view all grievances, respond to them, and mark them as resolved.

4. **Email Notifications:**
   - Email notifications are sent to both the admin and user when a grievance is submitted and when a response is given.

## 📁 Project Structure

```
girlfriend-grievance-portal/
│
├── app.py                # Main application logic
├── .env                  # Environment variables
├── requirements.txt      # Python dependencies
├── .gitignore            # Git ignore file
├── templates/            # HTML templates
│   ├── home.html
│   ├── login.html
│   ├── submit.html
│   ├── thankyou.html
│   ├── my_grievances.html
│   └── dashboard.html
└── venv/                 # Virtual environment
```

### Notes:

- Make sure to set up your environment variables correctly in the `.env` file.
- If you're using Gmail for sending emails, ensure you use an app password (not your Google account password) if two-factor authentication (2FA) is enabled.

For more information, visit the official [Flask Documentation](https://flask.palletsprojects.com/).

## 🐳 Self-Hosting with Docker and Traefik

This guide explains how to deploy the Grievance Portal using Docker Compose, with Traefik as a reverse proxy.

### Directory Structure
```
/root
├── docker-compose.yml         # (Traefik compose file)
├── data/
│   └── letsencrypt/          # SSL certificates
└── grievance-portal/
    ├── app.py
    ├── requirements.txt
    ├── Dockerfile
    ├── docker-compose.yml     # (Portal compose file)
    ├── .env
    ├── data/                 # For database persistence
    └── ... (other portal files)
```

### 1. Main Traefik Configuration
Create a `docker-compose.yml` in your root directory:
```yaml
version: '3'
services:
  traefik:
    image: traefik:v3
    container_name: traefik
    restart: unless-stopped
    ports:
      - 443:443
      - 127.0.0.1:8080:8080
    command:
      - "--api.insecure=true"
      - "--providers.docker=true"
      - "--providers.docker.exposedbydefault=false"
      - "--entryPoints.websecure.address=:443"
      - "--entryPoints.web.http.redirections.entryPoint.to=websecure"
      - "--entryPoints.web.http.redirections.entryPoint.scheme=https"
      - "--certificatesresolvers.myresolver.acme.tlschallenge=true"
      - "--certificatesresolvers.myresolver.acme.email=hello@shivamr.com"
      - "--certificatesresolvers.myresolver.acme.storage=/letsencrypt/acme.json"
      - "--log.level=INFO"
      - "--ping"
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
      - "./data/letsencrypt:/letsencrypt"
    networks:
      - traefik-public

networks:
  traefik-public:
    name: traefik-public
```

### 2. Clone the Project
```bash
cd /root
# Clone the repository into its own directory
git clone https://github.com/your-username/girlfriend-grievance-portal.git grievance-portal
cd grievance-portal
```

### 3. Create and Configure .env
```bash
nano .env
```
Add your environment variables:
```env
EMAIL_ADMIN=your.email@gmail.com
EMAIL_PASS=your-app-password
EMAIL_DEFAULT_SENDER=your.email@gmail.com
EMAIL_USER_RECEIVER=user.email@gmail.com
USER_NAME=girlfriend
USER_PASSWORD=user123
ADMIN_NAME=boyfriend
ADMIN_PASSWORD=admin123
PORTAL_URL=https://your-domain.com
```

### 4. Create Dockerfile
```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
RUN python3 -c "from app import init_db; init_db()"
EXPOSE 5000
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "--workers", "3", "app:app"]
```

### 5. Create docker-compose.yml (in grievance-portal directory)
```yaml
version: '3'
services:
  grievance-portal:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: grievance-portal
    restart: unless-stopped
    env_file:
      - .env
    volumes:
      - ./data:/app/data
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.grievance-portal.rule=Host(`your-domain.com`)"
      - "traefik.http.routers.grievance-portal.entrypoints=websecure"
      - "traefik.http.routers.grievance-portal.tls=true"
      - "traefik.http.routers.grievance-portal.tls.certresolver=myresolver"
      - "traefik.http.services.grievance-portal.loadbalancer.server.port=5000"
    networks:
      - traefik-public

networks:
  traefik-public:
    external: true
```

### 6. Start the Services
First, start Traefik:
```bash
cd /root
docker-compose up -d
```

Then, start the grievance portal:
```bash
cd /root/grievance-portal
docker-compose up -d
```

### 7. Access the Portal
Visit `https://your-domain.com` in your browser.

### 8. Troubleshooting
- Check container logs: `docker-compose logs -f`
- Check if the container is running: `docker ps | grep grievance-portal`
- Check Traefik logs: `docker logs traefik`
- Check network: `docker network inspect traefik-public`
- Check SSL certificates: `ls -la /root/data/letsencrypt/`

### 9. Database Backup
```bash
# Create backup directory
mkdir -p backups

# Backup database
docker cp grievance-portal:/app/data/grievances.db ./backups/grievances.db.$(date +%Y%m%d)
```

---
