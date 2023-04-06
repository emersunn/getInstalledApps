import os
import csv
import plistlib
from datetime import datetime

# Read the list of excluded apps from a CSV file
def read_excluded_apps_from_csv(file_path):
    excluded_apps = []

    with open(file_path, newline='') as csvfile:
        reader = csv.reader(csvfile)  # Use csv.reader() instead of csv.DictReader()
        next(reader)  # Skip the header
        for row in reader:
            excluded_apps.append(row[0])  # Append the app name from the row

    return excluded_apps

# Get a list of installed apps, excluding those in the provided list
def get_installed_apps(excluded_apps):
    applications_dir = '/Applications'
    apps = []

    # Iterate through the applications in the /Applications directory
    for app in os.listdir(applications_dir):
        if app.endswith('.app'):
            info_plist = os.path.join(applications_dir, app, 'Contents', 'Info.plist')
            if os.path.exists(info_plist):
                with open(info_plist, 'rb') as f:
                    plist = plistlib.load(f)
                    app_name = plist.get('CFBundleName', app)
                    
                    # If the app is not in the excluded list, add it to the list of installed apps
                    if app_name not in excluded_apps:
                        app_version = plist.get('CFBundleShortVersionString', 'Unknown')
                        app_bundle_id = plist.get('CFBundleIdentifier', 'Unknown')
                        app_install_date = datetime.fromtimestamp(os.path.getmtime(info_plist)).strftime('%Y-%m-%d')
                        
                        apps.append({'name': app_name, 'version': app_version, 'bundle_id': app_bundle_id, 'install_date': app_install_date})
    
    return apps

# Save the list of installed apps to a CSV file
def save_apps_to_csv(apps, file_path):
    with open(file_path, 'w', newline='') as csvfile:
        fieldnames = ['name', 'version', 'bundle_id', 'install_date']
        writer = csv.DictWriter(csvfile, fieldnames=fieldnames)

        writer.writeheader()
        for app in apps:
            writer.writerow(app)

# Main script execution
if __name__ == '__main__':
    # Read the list of excluded apps from the CSV file
    excluded_apps = read_excluded_apps_from_csv('excluded_apps.csv')
    
    # Get the list of installed apps, excluding the specified apps
    apps = get_installed_apps(excluded_apps)
    
    # Save the list of installed apps to a CSV file
    save_apps_to_csv(apps, 'installed_apps.csv')
