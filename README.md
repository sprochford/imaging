# TIFF Image Resizer Script

This Bash script processes TIFF image files in the current directory, resizing them to a maximum height of 4400 pixels and saving them in a new directory called "4400 pixels". It also preserves metadata and provides robust error handling and logging.

## Features

*   Resizes TIFF images to a maximum height of 4400 pixels.
*   Preserves metadata using `exiftool`.
*   Robust error checking and logging to a file named `error_report_[folder_name]_[first_file]-[last_file].log`.
*   Two-pass conversion to handle potential transient errors.
*   File count verification to ensure all files are processed.
*   User notifications via dialog boxes and sound (macOS specific).
*   Suppresses specific ImageMagick warnings for cleaner logs.

## Requirements

*   **ImageMagick:** Required for image processing (`magick`). Install using your system's package manager (e.g., `brew install imagemagick` on macOS, `sudo apt-get install imagemagick` on Debian/Ubuntu).
*   **ExifTool:** Required for metadata preservation. Install using your system's package manager (e.g., `brew install exiftool` on macOS, `sudo apt-get install libimage-exiftool-perl` on Debian/Ubuntu).
*   **macOS (for notifications and sound):** The dialog box notifications and sound playback are macOS specific. The core image processing functionality will work on other Unix-like systems.

## Usage

1.  Save the script to a file (e.g., `resize_tiffs.sh`).
2.  Make the script executable: `chmod +x resize_tiffs.sh`
3.  Place the script in the directory containing the TIFF files you want to process.
4.  Run the script: `./resize_tiffs.sh`

## Script Breakdown

The script performs the following steps:

1.  **Setup and Initialization:** Creates the output directory, gathers TIFF files, and sets up the error log.
2.  **Functions:**
    *   `check_file()`: Checks if an output file exists and is a valid image.
    *   `convert_file()`: Resizes the image, sets density, compresses it, and copies metadata.
3.  **Main Processing Loop (First Pass):** Iterates through each TIFF file, converting it if necessary and validating the conversion.
4.  **Second Pass (Re-check):** Performs a second pass to catch any files that failed to convert in the first pass.
5.  **File Count Check:** Verifies that the number of output files matches the number of input files.
6.  **Completion and Notification:** Displays a completion message, opens the current directory, and plays a sound (macOS only).
