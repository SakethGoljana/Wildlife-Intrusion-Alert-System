# Wildlife Intrusion Alert System

## Overview
The **Wildlife Intrusion Alert System** is a computer vision-based solution designed violin detect wildlife intrusions in farmland or other monitored areas and alert users via SMS. Built with Python, YOLOv8 (`ultralytics`), OpenCV, and Twilio, the system processes images (including night vision) to identify animals and sends real-time notifications to a specified phone number. The implementation is provided in a Google Colab notebook, leveraging free cloud computing resources for ease of use.

This README provides detailed instructions for setting up, running, and customizing the system as implemented in the [Google Colab notebook](https://colab.research.google.com/drive/1RrdgFUps7U-YSULQjdf2A9VncTF2y5Lp?usp=sharing).

## Features
- **Animal Detection**: Uses YOLOv8 to detect wildlife in images, with support for both visible and infrared (night vision) inputs.
- **Image Preprocessing**: Enhances image quality using CLAHE (Contrast Limited Adaptive Histogram Equalization) for better detection in low-light conditions.
- **Real-time Alerts**: Sends SMS notifications via Twilio when animals are detected, ensuring prompt action.
- **User-Friendly**: Runs in Google Colab, requiring minimal setup and no local hardware.
- **Customizable**: Allows modification of detection thresholds, target animal classes, and Twilio credentials.

## Prerequisites
To run the Wildlife Intrusion Alert System, ensure you have:
- A **Google Account** to access Google Colab.
- A **Twilio Account** with:
  - Account SID, Auth Token, and a Twilio phone number (for sending SMS).
  - A verified recipient phone number (e.g., the farmer’s phone).
- Basic knowledge of **Python** and **Google Colab**.
- An internet connection to install dependencies and send SMS.
- Sample images (visible or infrared) for testing, or access to a dataset via Google Drive.

## Setup Instructions
Follow these steps to set up and run the system in Google Colab:

1. **Access the Colab Notebook**:
   - Open the [Wildlife Intrusion Alert System notebook](https://colab.research.google.com/drive/1RrdgFUps7U-YSULQjdf2A9VncTF2y5Lp?usp=sharing).
   - Sign in with your Google account if prompted.

2. **Install Dependencies**:
   - Run the first code cell to install required libraries:
     ```bash
     !pip install ultralytics twilio opencv-python-headless
     ```
   - This installs `ultralytics` (for YOLOv8), `twilio` (for SMS), and `opencv-python-headless` (for image processing).

3. **Upload or Access Input Images**:
   - **Upload Manually**:
     - Click the folder icon in the Colab sidebar.
     - Drag and drop your image files (e.g., `.jpg`, `.png`) or use the upload button.
   - **Use Google Drive** (optional):
     - Mount Google Drive by adding and running:
       ```python
       from google.colab import drive
       drive.mount('/content/drive')
       ```
     - Specify the path to your images in the notebook (e.g., `/content/drive/MyDrive/images/`).

4. **Configure Twilio Credentials**:
   - Update the Twilio configuration in the notebook with your credentials:
     ```python
     account_sid = 'your_account_sid'  # e.g., 'AC017379e1833fe16e7ecd2462a67be143'
     auth_token = 'your_auth_token'    # e.g., 'f238c8823b37d8e33cc1adcf0cba6370'
     twilio_phone = 'your_twilio_number'  # e.g., '+12293635761'
     farmer_phone = 'your_recipient_number'  # e.g., '+919059478739'
     ```
   - Obtain these from your Twilio dashboard (https://www.twilio.com/console).

5. **Run the System**:
   - Execute the notebook cells sequentially:
     1. **Install libraries** and import dependencies.
     2. **Preprocess images** using the `preprocess_image` function (handles grayscale/IR images with CLAHE).
     3. **Detect animals** using YOLOv8 on the uploaded image.
     4. **Send SMS alerts** via Twilio if animals are detected.
   - The notebook outputs:
     - A message indicating whether animals were detected (e.g., "Animals detected in the image!").
     - SMS confirmation (e.g., "SMS sent successfully! SID: ...") or a message if no animals were detected.

6. **View Results**:
   - Detection results (e.g., images with bounding boxes) are displayed using `matplotlib.pyplot`.
   - Download processed images from the Colab file explorer (`/content/`) if needed.

## Usage
- **Input**: Upload an image (visible or infrared) containing potential wildlife.
- **Processing**:
  - The `preprocess_image` function enhances image contrast, especially for night vision inputs, using CLAHE.
  - YOLOv8 detects animals, checking for predefined wildlife classes (e.g., deer, bear, etc.).
- **Output**:
  - Visual output: Processed image with bounding boxes around detected animals (displayed in Colab).
  - SMS alert: If animals are detected, an SMS is sent to the specified phone number with the message: "Alert: Animals detected in your farmland! Please take action."
- **Customization**:
  - Modify the YOLOv8 model (e.g., use a custom-trained model by replacing `yolov8n.pt`).
  - Adjust detection thresholds or target classes in the detection logic.
  - Change the SMS message or add additional notification methods (e.g., email).

### Example
To detect animals in an uploaded image:
1. Upload an image (e.g., `wildlife.jpg`) to Colab.
2. Ensure the notebook references the correct image path:
   ```python
   image = cv2.imread('/content/wildlife.jpg')
   ```
3. Run the preprocessing and detection cells.
4. If animals are detected, an SMS is sent, and the annotated image is displayed.

## Code Structure
The notebook includes the following key components:
- **Dependency Installation**:
  - Installs `ultralytics`, `twilio`, and `opencv-python-headless`.
- **Imports**:
  - Libraries: `YOLO` (ultralytics), `Client` (twilio), `cv2`, `numpy`, `files` (colab), `matplotlib.pyplot`.
- **Image Preprocessing**:
  - Function: `preprocess_image(image)`
  - Handles grayscale/IR images using CLAHE for contrast enhancement.
- **Animal Detection**:
  - Uses YOLOv8 (`yolov8n.pt`) to detect animals in preprocessed images.
  - Sets `animal_detected` flag based on detection results.
- **SMS Alerts**:
  - Configures Twilio credentials.
  - Sends SMS to the farmer’s phone if `animal_detected` is `True`.

## Directory Structure
The Colab environment is temporary but includes:
- `/content/`: Default working directory for uploaded images and outputs.
- `/content/yolov8n.pt`: YOLOv8 model weights (downloaded automatically by `ultralytics`).
- `/content/outputs/`: Processed images with bounding boxes (if saved).

## Troubleshooting
- **Dependency Errors**:
  - Ensure the `!pip install` cell runs successfully.
  - Restart the runtime (`Runtime > Restart runtime`) if installation fails.
- **Twilio Issues**:
  - Verify your Twilio credentials (SID, token, phone numbers) are correct.
  - Ensure the recipient number is verified in Twilio’s console.
  - Check your Twilio account balance for SMS credits.
- **Image Loading Errors**:
  - Confirm the image path is correct (e.g., `/content/your_image.jpg`).
  - Use `cv2.imread()` with valid image formats (`.jpg`, `.png`).
- **Colab Limits**:
  - Free Colab sessions may disconnect after inactivity or hit resource limits. Save outputs frequently or consider Colab Pro.
- **Missing Detection Logic**:
  - If the detection code is incomplete, ensure the YOLOv8 model is loaded and processes images correctly. A sample detection loop is:
    ```python
    model = YOLO('yolov8n.pt')
    results = model(preprocessed_image)
    animal_detected = any(cls in WILDLIFE_CLASSES for cls in results[0].names)
    ```

## Limitations
- **Single Image Processing**: The current implementation processes one image at a time. For video or real-time detection, modify the code to handle video streams (e.g., using `cv2.VideoCapture`).
- **Model Accuracy**: The pre-trained YOLOv8 model (`yolov8n.pt`) may not detect all wildlife species. Fine-tune the model with a custom dataset for better accuracy.
- **Colab Constraints**: Free Colab accounts have limited runtime and GPU availability. Heavy processing may require a local setup or Colab Pro.
- **Twilio Dependency**: SMS alerts require a paid Twilio account with sufficient credits.

## Contributing
Contributions are welcome! To contribute:
1. Fork the repository (if the notebook is hosted on GitHub).
2. Create a new branch for your feature or bug fix.
3. Submit a pull request with a clear description of changes.

Alternatively, suggest improvements by commenting on the Colab notebook or contacting the project maintainer.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments
- Built with [Google Colab](https://colab.research.google.com/) for free cloud computing.
- Utilizes [YOLOv8](https://github.com/ultralytics/ultralytics) for object detection.
- Powered by [Twilio](https://www.twilio.com/) for SMS notifications.
- Leverages [OpenCV](https://opencv.org/) for image processing.

## Contact
For questions or support, reach out via:
- **Email**: [your-email@example.com] (replace with actual contact if applicable).
- **GitHub Issues**: [Link to repository issues] (if hosted on GitHub).

---

**Note**: The notebook’s animal detection logic was truncated in the provided content. This README assumes a standard YOLOv8 detection workflow. If you can provide the missing code (e.g., the detection loop or base64 image processing), I can refine the README further. Let me know if you need additional assistance!
