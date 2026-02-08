# FastAPI Learning Project

This is a personal learning project created to explore and understand FastAPI, a modern, fast web framework for building APIs with Python. The project implements a simple instagram-like application as a practical exercise to learn various FastAPI concepts and features.

![Fast Api Media Sharing PLatform](https://img.shields.io/badge/Python-3.12+-blue.svg)
![FastAPI Version](https://img.shields.io/badge/FastAPI-0.122.0+-orange.svg)
![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)

> **Note:** This is not intended to be a production-ready social media application. The main goal is to learn FastAPI through hands-on implementation.




## Learning Objectives

This project was built to learn and practice the following FastAPI concepts:

- **Async/Await Programming**: Using async/await with FastAPI for non-blocking operations
- **Database Integration**: SQLAlchemy with async support using aiosqlite
- **User Authentication**: Implementing JWT-based authentication with fastapi-users
- **File Uploads**: Handling multipart form data and file uploads
- **External API Integration**: Using ImageKit for image/video storage
- **Dependency Injection**: Leveraging FastAPI's dependency system
- **Pydantic Schemas**: Data validation and serialization
- **RESTful API Design**: Creating clean, well-structured endpoints
- **Lifecycle Management**: Using lifespan events for database initialization

## Tech Stack

### Backend

- **FastAPI**: Modern, fast web framework for building APIs
- **SQLAlchemy**: SQL toolkit and ORM with async support
- **aiosqlite**: Async SQLite driver
- **fastapi-users**: Ready-to-use and customizable authentication and user management
- **ImageKit**: Cloud-based image and video upload, storage, and transformation service
- **Uvicorn**: ASGI server for running FastAPI applications

### Frontend (Demo)

- **Streamlit**: Simple Python web app framework for demonstration purposes

## Project Structure

```
fast_api/
├── app/
│   ├── app.py          # Main FastAPI application with endpoints
│   ├── db.py           # Database models and session management
│   ├── schemas.py      # Pydantic schemas for request/response validation
│   ├── users.py        # User authentication and management
│   └── images.py       # ImageKit configuration
├── frontend.py         # Streamlit frontend for testing the API
├── main.py             # Entry point for running the server
└── pyproject.toml      # Project dependencies
```

## ImageKit Integration

This project uses ImageKit for handling image and video uploads. ImageKit is a cloud-based media management platform that provides:

- **File Upload**: Upload images and videos directly from the FastAPI backend
- **URL Generation**: Get publicly accessible URLs for uploaded media
- **Image Transformations**: Resize, crop, and apply effects to images on-the-fly
- **Video Optimization**: Automatic video compression and format conversion

### How It Works

1. **Configuration**: ImageKit is initialized in [`app/images.py`](app/images.py) using environment variables:
   - `IMAGEKIT_PRIVATE_KEY`: Private key for authentication
   - `IMAGEKIT_PUBLIC_KEY`: Public key for API access
   - `IMAGEKIT_URL`: Your ImageKit URL endpoint

2. **Upload Process** ([`app/app.py`](app/app.py:32-72)):
   - User uploads a file through the `/upload` endpoint
   - File is temporarily saved to disk
   - ImageKit API uploads the file to cloud storage
   - ImageKit returns a public URL and file metadata
   - Post record is created in the database with the ImageKit URL
   - Temporary file is cleaned up

3. **Image Transformations** ([`frontend.py`](frontend.py:152-167)):
   - Images are transformed using ImageKit's URL-based transformation API
   - Captions are overlaid on images using base64 encoding
   - Videos are resized and padded for consistent display

### Benefits of Using ImageKit

- No need to manage local file storage
- Automatic CDN delivery for fast loading
- Built-in image optimization and compression
- Easy to implement transformations without server-side processing
- Scalable storage solution

## API Endpoints

### Authentication

- `POST /auth/jwt/login` - User login
- `POST /auth/register` - User registration
- `GET /auth/jwt/logout` - User logout
- `POST /auth/forgot-password` - Request password reset
- `POST /auth/verify` - Verify user email

### Users

- `GET /users/me` - Get current user info
- `PATCH /users/me` - Update current user profile

### Posts

- `POST /upload` - Upload a new post (image/video with caption)
- `GET /feed` - Get all posts in the feed
- `DELETE /posts/{post_id}` - Delete a post (owner only)

## Setup Instructions

### Prerequisites

- Python 3.12
- uv package manager

### Installation (Using UV)

1. Clone the repository:

```bash
git clone <repository-url>
cd fast_api
```


2. Set up environment variables:
   Create a `.env` file in the root directory:

```
SECRET=your-secret-key-here
IMAGEKIT_PRIVATE_KEY=your-imagekit-private-key
IMAGEKIT_PUBLIC_KEY=your-imagekit-public-key
IMAGEKIT_URL=https://ik.imagekit.io/your-id
```

To get ImageKit credentials:

- Sign up at [imagekit.io](https://imagekit.io)
- Create a new project
- Copy your private key, public key, and URL endpoint from the dashboard

3. Run the FastAPI server:

- Make sure uv is installed on your system. If not, follow the documentation at: https://docs.astral.sh/uv/
  
```bash
uv run main.py
```
UV will automatically start a virtual envrionment, install dependencies and start the server running on localhost.

The API will be available at `http://localhost:8000`

4. (Optional) Run the Streamlit frontend:

```bash
streamlit run frontend.py
```

The frontend will be available at `http://localhost:8501`

## API Documentation

FastAPI automatically generates interactive API documentation:

- **Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`

## What Was Learned

Through this project, I gained practical experience with:

1. **FastAPI Fundamentals**: Route definitions, request handling, response models
2. **Async Database Operations**: Using SQLAlchemy with async/await patterns
3. **Authentication Flow**: JWT token generation, validation, and user management
4. **File Handling**: Temporary file management, multipart form data processing
5. **ImageKit Integration**: Cloud-based media upload, storage, and transformation
6. **Error Handling**: HTTP exceptions and proper error responses
7. **Database Relationships**: One-to-many relationships between users and posts
8. **Dependency Injection**: Creating reusable dependencies for sessions and authentication
9. **API Security**: Protecting routes with authentication requirements
10. **External API Integration**: Working with third-party services (ImageKit)

## Future Learning Opportunities

Potential areas to expand this learning project:

- Add pagination to the feed endpoint
- Implement post likes and comments
- Add user profiles and following functionality
- Use PostgreSQL instead of SQLite
- Implement rate limiting
- Add comprehensive testing with pytest
- Containerize with Docker
- Add API versioning

## License

This is a personal learning project. Feel free to use it for educational purposes.
