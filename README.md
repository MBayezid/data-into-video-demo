# Data-to-Video Converter Documentation

## 📌 Overview
A Python-based tool that converts any file/folder into a lossless video format and reconstructs the original data perfectly. Ideal for data archiving in video form.

![Workflow Diagram](Screenshots/Screenshot from 2025-03-01 21-03-02.png)

## 🔧 How It Works

### Encoding Workflow (Files → Video)
1. **File Selection**  
   `select_files()`: Upload files via GUI to "uploaded_files" directory
2. **ZIP Creation**  
   `create_archive()`: Bundle files into "original.zip" using DEFLATE compression
3. **Binary Conversion**  
   `create_frames()`: Convert ZIP to RGB pixel frames (256x256 default)
4. **Video Encoding**  
   `encode_video()`: Create FFV1-encoded AVI file using lossless compression

### Decoding Workflow (Video → Files)
1. **Frame Extraction**  
   `extract_frames()`: Decode video to raw RGB frames
2. **Data Reconstruction**  
   Rebuild ZIP from pixel data using size header
3. **File Extraction**  
   `extract_archive()`: Unzip contents to "extracted_files"

## 💡 Key Features
```python
# Size header ensures accurate reconstruction
header = len(original_data).to_bytes(4, 'big')  # First 4 bytes store data length
data_with_header = header + original_data
```
- **Lossless Preservation**: Uses FFV1 video codec (archival-grade)
- **Automatic Padding**: Handles arbitrary file sizes
- **Integrity Check**: Final file comparison validation
- **Cross-Platform**: Works on any OS with Python 3.8+

## 🚀 Usage

### Encode Files
```python
files_to_video(output_video='my_data.avi', frame_size=(320, 240))
```

### Decode Video
```python
video_to_files('my_data.avi', 'restored_files')
```

### Verify Integrity
```python
original = open('original.zip', 'rb').read()
extracted = open('restored_files/output.zip', 'rb').read()
print("Data Match:", original == extracted)  # True/False
```

## 🛠️ Scope for Improvement

| Area                | Current Implementation       | Potential Enhancement                |
|---------------------|------------------------------|--------------------------------------|
| **Compression**     | DEFLATE (ZIP)                | Zstandard/Brotli compression         |
| **Error Handling**  | Basic size validation        | Reed-Solomon error correction        |
| **Security**        | No encryption                | AES-256 payload encryption           |
| **Performance**     | In-memory processing         | Disk streaming for large files       |
| **Metadata**        | File sizes only              | Full directory structure preservation|

## ⚠️ Current Limitations
1. **Large Video Sizes**  
   10MB ZIP → ~20MB video (2:1 size ratio)
2. **No Partial Recovery**  
   Entire video needed for reconstruction
3. **Basic UI**  
   Command-line only interface

## 🌐 Use Cases
- **Data Archiving**: Store documents as YouTube videos
- **Steganography**: Hide data in plain sight
- **Cold Storage**: Long-term preservation 

## 📦 Dependencies
```bash
# Core Requirements
pip install ffmpeg-python numpy pillow

# System Packages (Ubuntu)
sudo apt install ffmpeg
```

## 📄 License
MIT License - Free for commercial and personal use

**Created by**: [Musanna Bayezid]  
**Version**: 1.2 (2-3-2025)  
**Repository**: [https://github.com/MBayezid/data-conversion-demo-python]
