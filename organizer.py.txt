import os
import shutil
from pathlib import Path

# Folder to organize (Downloads)
TARGET_FOLDER = Path.home() / "Downloads"

CATEGORIES = {
    "Images": [".jpg", ".jpeg", ".png", ".gif"],
    "Documents": [".pdf", ".docx", ".txt"],
    "Videos": [".mp4", ".mkv"],
    "Music": [".mp3"],
    "Archives": [".zip", ".rar"]
}

def get_category(file):
    ext = file.suffix.lower()
    for category, extensions in CATEGORIES.items():
        if ext in extensions:
            return category
    return "Other"

def organize(folder):
    for item in folder.iterdir():
        if item.is_file():
            category = get_category(item)
            dest = folder / category
            dest.mkdir(exist_ok=True)
            shutil.move(str(item), str(dest / item.name))
            print(f"Moved {item.name} -> {category}")

organize(TARGET_FOLDER)