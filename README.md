# 🤖 AI Assistant Web App

This is a **Full Stack AI Assistant Application** built using **React (Vite)** for the frontend and **Node.js + Express + MongoDB** for the backend.  
The app integrates **JWT authentication**, **Cloudinary** for image/media hosting, **Multer** for handling file uploads, and **Google Gemini API** for generative AI-powered content generation.

---

## 🚀 Features

### 🧠 AI-Powered Content Generation
- Integrated with **Google Gemini API** to enable intelligent, server-side generative AI features.
- The frontend can easily consume AI-generated data through the backend’s `/api/gemini` endpoint.

### 🖼️ Image Upload & Management
- **Multer** middleware handles multipart/form-data uploads.
- **Cloudinary** hosts uploaded images securely and returns optimized URLs.
- User profile images are updated dynamically in the database.

### 🔐 Secure Authentication System
- JWT-based authentication flow ensures protected routes and secure user sessions.
- `isAuth` middleware verifies tokens and allows only authorized actions.

### ⚛️ Modern Frontend Stack
- Built with **React + Vite** for fast development and optimized builds.
- Component-driven structure (`App.jsx`, `Card.jsx`, `context/`, `pages/`).
- Clean UI built with **Tailwind CSS** (optional styling layer if added).

---
## 🔄 Application Flow

### **Flow 1 — Authenticated Image Upload**
**Frontend → Multer → Cloudinary → User Record**

1. **Frontend**
   - User selects image from form (`<input type="file">`).
   - Sends `POST /api/users/upload` with `multipart/form-data`.
   - Includes `Authorization: Bearer <JWT>` header.

2. **Server Middleware Chain**
   - `isAuth` → verifies JWT and sets `req.userId`.
   - `multer` → parses uploaded file and attaches to `req.file`.

3. **Controller Logic**
   - Uploads file to **Cloudinary** using `cloudinary.uploader.upload(...)`.
   - Updates user document:
     ```js
     User.findByIdAndUpdate(req.userId, { avatar: url }, { new: true });
     ```
   - Returns updated user or image URL to frontend.

4. **Frontend**
   - Receives the Cloudinary URL and updates the UI/state.

---


**Developer Notes**

You can modify Gemini API prompts or parameters in backend/gemini.js.
To customize image upload limits or accepted file types, edit backend/middlewares/multer.js.
The project follows the MVC (Model–View–Controller) structure for clarity and scalability.

**License**

This project is licensed under the MIT License.

 **Acknowledgment**
 
This project was built by following a tutorial-based guide on creating an AI Assistant with Cloudinary, Multer, and Gemini API integrations, adapted and deployed for portfolio purposes.

 **Author**: Sarabjeet Singh
