# macOS App Tracker

This script scans the /Applications directory on a macOS system and generates a CSV file with a list of installed applications, excluding any applications specified in a separate CSV file. The generated list includes the app name, version, bundle identifier, and installation date.

## Requirements

Python 3.x

## Usage

1. Save the script as a file named app_tracker.py (or any other name you prefer).

2. Create a CSV file named excluded_apps.csv in the same directory as the script. This file should contain the names of the apps you want to exclude from the generated list. The first line should be a header with the name name, and each subsequent line should contain one app name. For example:

```
name
Safari
TextEdit
```

3. Open Terminal and navigate to the directory where you saved the script and the excluded_apps.csv file. You can use the cd command to change the directory. For example:
```
cd /path/to/your/script
```
4. Run the script using the Python interpreter:
```
python3 app_tracker.py
```
5. The script will create a new CSV file called installed_apps.csv in the same directory. This file contains the list of installed applications, excluding the ones specified in the excluded_apps.csv file.

## Customization

To change the location of the excluded_apps.csv file or the output file, modify the file paths in the main script execution section:
```
if __name__ == '__main__':
    excluded_apps = read_excluded_apps_from_csv('path/to/excluded_apps.csv')
    ...
    save_apps_to_csv(apps, 'path/to/installed_apps.csv')
```    
Replace path/to/excluded_apps.csv and path/to/installed_apps.csv with the actual file paths you want to use.


