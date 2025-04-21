Wildlife Intrusion Alert System
Overview
The Wildlife Intrusion Alert System is a computer vision-based tool designed to detect wildlife intrusions in farmland or protected areas and notify users via SMS. Developed as part of a research project, it uses YOLOv8 for animal detection, OpenCV for image preprocessing, and Twilio for real-time alerts. This repository contains the implementation (a Python notebook) and the accompanying research paper, exploring the system’s design, performance, and applications in agricultural protection.
Features

Animal Detection: Identifies wildlife in images (visible or infrared) using YOLOv8.
Image Preprocessing: Enhances low-light or night vision images with CLAHE.
SMS Alerts: Sends notifications via Twilio when animals are detected.
Research Insights: Includes a paper detailing methodology, experiments, and results.

Repository Contents

wildlife_alert.ipynb: Jupyter notebook with the system’s implementation.
wildlife_paper.pdf: Research paper discussing the system’s design and findings.
requirements.txt: Python dependencies for running the notebook.
.gitignore: Excludes sensitive files and large assets.
LICENSE: MIT License for code usage.

Setup Instructions
Prerequisites

Python 3.8+
A Twilio account with SID, Auth Token, and phone numbers.
Sample images (visible or infrared) for testing.

Installation

Clone the Repository:
git clone https://github.com/yourusername/wildlife-intrusion-alert-system.git
cd wildlife-intrusion-alert-system


Install Dependencies:
pip install -r requirements.txt


Set Up Twilio Credentials:

Create a .env file in the root directory:TWILIO_ACCOUNT_SID=your_account_sid
TWILIO_AUTH_TOKEN=your_auth_token
TWILIO_PHONE=+your_twilio_number
FARMER_PHONE=+your_recipient_number


Ensure python-dotenv is installed (pip install python-dotenv).


Run the Notebook:

Open wildlife_alert.ipynb in Jupyter Notebook or Google Colab.
Upload a test image (e.g., test_image.jpg) to the notebook’s environment.
Execute cells to preprocess the image, detect animals, and send SMS alerts.



Usage

Input Image: Provide an image (visible or infrared) containing potential wildlife.
Preprocessing: The notebook enhances image contrast using CLAHE.
Detection: YOLOv8 identifies animals, flagging detections.
Alerts: If animals are detected, an SMS is sent to the specified number (e.g., “Alert: Animals detected in your farmland!”).
Output: View annotated images with bounding boxes in the notebook.

Research Paper
The included wildlife_paper.pdf details:

System architecture and algorithms.
Experimental results (e.g., detection accuracy, SMS reliability).
Applications in farmland protection and wildlife management.

Troubleshooting

Twilio Errors: Verify credentials in .env and ensure sufficient Twilio credits.
Image Issues: Ensure images are in supported formats (.jpg, .png) and accessible.
YOLOv8 Failures: Confirm yolov8n.pt is downloaded (auto-handled by ultralytics).
Colab Limits: Use a local environment for heavy processing or long-running tasks.

Making It Look Natural and Professional
To ensure the repository looks authentic and polished without appearing forced:

Clear README: This README is concise, avoids jargon, and focuses on usability, reflecting your research’s practical value.
Logical Structure: Files are organized (notebook, paper, requirements) for easy navigation.
Commit History: Use meaningful commit messages (e.g., “Add notebook with YOLOv8 implementation,” “Include research paper”) to show organic development.
Engage the Community: Add a “Contributing” section to invite feedback, making the project feel collaborative.
Showcase Research: Highlight the paper to emphasize the project’s academic rigor.

Contributing
Contributions are welcome! To contribute:

Fork the repository.
Create a branch (git checkout -b feature/your-feature).
Commit changes (git commit -m "Add your feature").
Push to the branch (git push origin feature/your-feature).
Open a pull request.

License
This project is licensed under the MIT License. See LICENSE for details.
Acknowledgments

Built with YOLOv8, OpenCV, and Twilio.
Research conducted to advance wildlife protection in agriculture.

