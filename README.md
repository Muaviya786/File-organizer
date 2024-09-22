# File-organizer

import os
import shutil

FILE_CATEGORIES = {
    'Images': ['.jpg', '.jpeg', '.png', '.gif'],
    'Documents': ['.pdf', '.doc', '.docx', '.txt', '.ppt', '.pptx', '.xls', '.xlsx'],
    'Audio': ['.mp3', '.wav'],
    'Videos': ['.mp4', '.avi'],
    'Archives': ['.zip', '.rar'],
    'Scripts': ['.py', '.js'],
    'Executables': ['.exe'],
    'Others': []
}

def organize_files_by_type(directory_path):
    for filename in os.listdir(directory_path):
        file_path = os.path.join(directory_path, filename)

        if os.path.isfile(file_path):
            file_ext = os.path.splitext(filename)[1].lower()
            destination_folder = None
            
            for category, extensions in FILE_CATEGORIES.items():
                if file_ext in extensions:
                    destination_folder = category
                    break
            
            if not destination_folder:
                destination_folder = 'Others'

            destination_folder_path = os.path.join(directory_path, destination_folder)
            if not os.path.exists(destination_folder_path):
                os.makedirs(destination_folder_path)

            shutil.move(file_path, os.path.join(destination_folder_path, filename))

if __name__ == "__main__":
    directory = input("Enter the directory path to organize: ")

    if os.path.isdir(directory):
        organize_files_by_type(directory)
        print(f"Files in '{directory}' have been organized by file type.")
    else:
        print("Error: The specified directory does not exist.")
