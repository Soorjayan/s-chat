# S Chat – Real-Time Messaging Application

S Chat is a full-stack real-time messaging web application designed to provide a smooth and interactive communication experience. The application supports private conversations, group chats, real-time messaging, file sharing, and user account management.

## 🚀 Features

- User registration and login with JWT authentication
- Secure password hashing using bcrypt
- Real-time messaging using Socket.IO
- Private conversations and group chats
- Online/offline user presence and last-seen information
- Typing indicators
- Message delivery and read receipts
- Unread message counts and notification sounds
- Emoji picker
- File sharing, including images, videos, and documents
- User profile photo management
- Account settings and password changes
- Light and dark themes
- Responsive user interface

## 🛠️ Tech Stack

**Frontend**
- React
- Vite
- JavaScript
- CSS

**Backend**
- Node.js
- Express.js
- Socket.IO
- JWT Authentication
- bcrypt

**Database**
- MongoDB Atlas
- Mongoose

**Tools and Deployment**
- Git and GitHub
- Postman
- Vercel (frontend hosting)
- Render (backend hosting)

## 📂 Project Structure

```text
S-Chat/
├── frontend/
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── vercel.json
├── backend/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── middleware/
│   ├── package.json
│   └── server.js
├── .gitignore
└── README.md
```

*Note: The exact folders and files may vary depending on the current project version.*

## ⚙️ Local Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/s-chat.git
cd s-chat
```

### 2. Install backend dependencies

```bash
cd backend
npm install
```

Configure the backend environment variables in a local `.env` file according to the backend configuration.

### 3. Install frontend dependencies

Open a separate terminal:

```bash
cd frontend
npm install
```

Create a frontend `.env` file with the appropriate local API and Socket.IO URLs.

### 4. Run the application

Start the backend using its configured start script:

```bash
cd backend
npm start
```

Start the frontend in a separate terminal:

```bash
cd frontend
npm run dev
```

Open the local URL displayed by Vite in your browser.

## 🌐 Deployment

The planned deployment architecture is:

- **Frontend:** Vercel
- **Backend:** Render
- **Database:** MongoDB Atlas

Configure the required environment variables and production URLs in the hosting dashboards before deployment.

## 🔐 Security Notes

- Never commit `.env` files or secret keys to GitHub.
- Store production credentials in the hosting provider's environment variables.
- Use strong database credentials and appropriate MongoDB Atlas network access rules.
- Configure CORS to allow only the intended frontend origins.

## 🎯 Project Objective

The objective of S Chat is to develop a full-stack messaging application while gaining practical experience in frontend development, backend API development, database integration, authentication, real-time communication, and cloud deployment.

## 👨‍💻 Author

**Soorjayan Varatharajan**

Computer Engineering Undergraduate  
University of Jaffna

## 📄 License

Add a license if you intend to distribute this project under specific reuse terms.
