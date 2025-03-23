# Prodigy-Task-2
Pixel Manipulation for image encryption
from PIL import Image
import numpy as np
import os

def encrypt_image(image_path, output_path):
    try:
        img = Image.open(image_path)
        pixels = np.array(img)

        encrypted_pixels = pixels.copy()
        encrypted_pixels[:, :, 0], encrypted_pixels[:, :, 2] = pixels[:, :, 2], pixels[:, :, 0]

        encrypted_img = Image.fromarray(encrypted_pixels)
        encrypted_img.save(output_path)
        print(f"Image encrypted and saved to {output_path}")
    except FileNotFoundError:
        print(f"Error: The file '{image_path}' was not found. Please check the file path.")
    except Exception as e:
        print(f"An error occurred: {e}")

def decrypt_image(image_path, output_path):
    try:
        img = Image.open(image_path)
        pixels = np.array(img)

        decrypted_pixels = pixels.copy()
        decrypted_pixels[:, :, 0], decrypted_pixels[:, :, 2] = pixels[:, :, 2], pixels[:, :, 0]

        decrypted_img = Image.fromarray(decrypted_pixels)
        decrypted_img.save(output_path)
        print(f"Image decrypted and saved to {output_path}")
    except FileNotFoundError:
        print(f"Error: The file '{image_path}' was not found. Please check the file path.")
    except Exception as e:
        print(f"An error occurred: {e}")

script_dir = os.path.dirname(os.path.abspath(__file__))  
input_image = os.path.join(script_dir, "input_image.jpg") 
encrypted_image = os.path.join(script_dir, "encrypted_image.jpg") 
decrypted_image = os.path.join(script_dir, "decrypted_image.jpg")  

encrypt_image(input_image, encrypted_image)
decrypt_image(encrypted_image, decrypted_image)
