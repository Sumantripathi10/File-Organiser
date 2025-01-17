# File-Organiser
import os
import shutil

def organize_files(directory):
    categories = {
        "Images": [".jpg", ".jpeg", ".png", ".gif", ".bmp", ".tiff"],
        "Documents": [".pdf", ".doc", ".docx", ".txt", ".xlsx", ".pptx"],
        "Videos": [".mp4", ".avi", ".mkv", ".mov", ".wmv"],
        "Music": [".mp3", ".wav", ".aac", ".flac"],
        "Archives": [".zip", ".rar", ".tar", ".gz", ".7z"],
        "Scripts": [".py", ".js", ".html", ".css", ".java", ".cpp"],
        "Others": []
    }

    if not os.path.exists(directory):
        print(f"Directory not found: {directory}")
        return

    for category in categories:
        folder_path = os.path.join(directory, category)
        os.makedirs(folder_path, exist_ok=True)

    for filename in os.listdir(directory):
        file_path = os.path.join(directory, filename)

        if os.path.isdir(file_path):
            continue

        file_extension = os.path.splitext(filename)[1].lower()
        destination_folder = "Others"
        for category, extensions in categories.items():
            if file_extension in extensions:
                destination_folder = category
                break

        destination_path = os.path.join(directory, destination_folder, filename)
        shutil.move(file_path, destination_path)
        print(f"Moved: {filename} -> {destination_folder}")

if __name__ == "__main__":
   
    target_directory = input("Enter the path of the directory to organize: ").strip()

    organize_files(target_directory)
    print("File organization complete.")
