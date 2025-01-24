# data-conversion-demo-python

Python scripts that encodes data into a series of images (video) and then decodes the data back from the images. The script aims to demonstrate a proof-of-concept for encoding and decoding data within a series of images, potentially for applications like steganography or creating unique visual representations of data.

Encoding Process:

File Handling: The script starts by allowing the user to select or create a directory to store uploaded files. It then zips the selected files into a single archive.
Base64 Encoding: The zip archive is converted into a Base64 encoded string, and then further converted into its binary representation.
Image Generation: The binary data is used to generate a sequence of grayscale images. The method involves dividing the image into a grid and setting pixel values based on the binary data.

Decoding Process:

Video to Images: A video is created from the generated images. The video is then processed to extract individual frames.
Image Analysis: Each frame is analyzed to retrieve the binary data embedded within the pixel values.
Data Reconstruction: The extracted binary data is converted back to a Base64 encoded string and then decoded to recreate the original zip file.
File Extraction: The recreated zip file is unzipped to retrieve the original files.
