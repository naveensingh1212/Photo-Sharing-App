# ImageGenie (Django Photo Sharing App)

ImageGenie is an AI-powered photo clustering and sharing app built with Django. It lets users upload multiple photos, automatically cluster faces, view clusters, search for images by a reference photo, and download an entire cluster as a ZIP.

**Repository structure (important parts)**
- `backend/` — Django project and app code (`core`, `home`) and `manage.py`
- `backend/db.sqlite3` — SQLite database (local)
- `static/` — project static assets and `static/images/` for uploaded images and thumbnails
- `templates/` — Django templates used by the app

## Features
- Upload multiple photos at once
- Automatic face detection & clustering (DBSCAN on face embeddings)
- Search for images in a cluster using a reference photo (selfie)
- Download cluster/album as a ZIP file
- Room-based / user-based organization (random 8-character room IDs in the app)

## Tech Stack
- Backend: Django (Python) — project located in `backend/`
- Face recognition: `face_recognition`, `dlib`, `opencv-python`
- ML / clustering: `numpy`, `scikit-learn` (DBSCAN), `scipy`
- Storage: Local filesystem for images; `db.sqlite3` for metadata

## Screenshots
(Place screenshots in `static/` or reference them from `public/photo/` if you keep them there.)

Main Page (example):
![Main Page](./static/images/577ff77cdd0895a01f8b4c75.jfif)
Upload Page (example):
![Upload Page](./static/images/5e187cc2b2e66a44187ad008.jfif)

> Replace the screenshot paths above with your actual screenshot files if you want nicer images in this README.

## Prerequisites
- Windows (PowerShell shown below)
- Python 3.8 recommended (project developed and tested with Python 3.8/3.9)
- C/C++ build toolchain for `dlib` (Visual Studio Build Tools), and system libraries for `face_recognition`/`dlib`

## Setup (Windows PowerShell)
1. Open PowerShell and change to the project folder:

```powershell
cd "C:\Users\HP\OneDrive\Desktop\Photo-Sharing-App"
```

2. Create (if you don't have one) and activate a virtual environment (Python 3.8 recommended):

```powershell
py -3.8 -m venv .env
.\.env\Scripts\Activate.ps1
```

3. Upgrade pip and install dependencies:

```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

> Note: If `dlib` or `face_recognition` fails to install with `pip`, make sure you have the Visual Studio Build Tools installed and follow the platform-specific guidance for `dlib` installation.

4. Apply Django migrations and create a superuser (if needed):

```powershell
cd backend
python manage.py migrate
python manage.py createsuperuser  # optional, to access /admin/
```

5. Run the development server:

```powershell
python manage.py runserver 0.0.0.0:8000
```

Open your browser at `http://127.0.0.1:8000/` to view the app.

## How to use
- Register / login (the app generates an 8-character room code during registration)
- Upload photos on the main page (or the upload page)
- Click `Process` (or equivalent) to run face detection + clustering — thumbnails of clusters will be created in `static/images/` and `Person` / `PersonGallery` records will be stored in the DB
- Click an album to view photos and use the "Download" link to get a ZIP of that cluster

## Important file locations
- Templates: `backend/templates/` and `backend/home/templates/` (project-level `templates/` is used)
- Uploaded images / thumbnails: `static/images/`
- Django project settings: `backend/core/settings.py`
- App views / clustering logic: `backend/home/views.py`

## Troubleshooting
- If `pip freeze` fails or your venv `pip` is broken, reactivate the venv and run `python -m pip install -r requirements.txt` instead.
- If face detection runs slowly or errors with OpenCV/dlib, ensure the C++ build tools are present and `dlib` is compiled for your Python version.

## Improving `requirements.txt`
The repository includes a basic `requirements.txt`. For exact package versions, activate the project venv and run:

```powershell
.\.env\Scripts\Activate.ps1
pip freeze > requirements.txt
```

If `pip freeze` fails, let me know and I can help fix the virtualenv pip launcher.

## License & Contact
If you want to collaborate, email: 2k22.cse.2213543@gmail.com
LinkedIn: https://www.linkedin.com/in/h-a-r-s-h

---

If you'd like, I can:
- Run `pip freeze` properly to produce an exact `requirements.txt` (I can fix the venv launcher if needed),
- Add screenshots into `static/` and update the README image references, or
- Add a short `docs/` folder with developer notes about building `dlib` on Windows.

