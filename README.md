def encrypt(text, shift):
  encrypted_text = ""
  for char in text:
      if char.isalpha():
          if char.isupper():
              encrypted_text += chr((ord(char) - 65 + shift) % 26 + 65)
          else:
              encrypted_text += chr((ord(char) - 97 + shift) % 26 + 97)
      else:
          encrypted_text += char
  return encrypted_text
def decrypt(encrypted_text, shift):
  decrypted_text = ""
  for char in encrypted_text:
      if char.isalpha():
          if char.isupper():
              decrypted_text += chr((ord(char) - 65 - shift) % 26 + 65)
          else:
              decrypted_text += chr((ord(char) - 97 - shift) % 26 + 97)
      else:
          decrypted_text += char
  return decrypted_text
def main():
  while True:
      choice = input("Do you want to encrypt or decrypt? (e/d): ").lower()
      if choice == 'e':
          text = input("Enter your message to encrypt: ")
          shift = int(input("Enter the shift value: "))
          encrypted_text = encrypt(text, shift)
          print("Encrypted text:", encrypted_text)
      elif choice == 'd':
          encrypted_text = input("Enter your message to decrypt: ")
          shift = int(input("Enter the shift value: "))
          decrypted_text = decrypt(encrypted_text, shift)
          print("Decrypted text:", decrypted_text)
      else:
          print("Invalid choice! Please select 'e' for encryption or 'd' for decryption.")
      contin = input("Do you want to continue? (yes/no): ").lower()
      if contin != 'yes':
          break
if __name__ == "__main__":
  main()
from PIL import Image

def encrypt_image(image_path, key):
    image = Image.open(image_path)
    encrypted_image = image.copy()
    width, height = image.size
    for y in range(height):
        for x in range(width):
            pixel = image.getpixel((x, y))
            encrypted_pixel = tuple((p + key) % 256 for p in pixel)
            encrypted_image.putpixel((x, y), encrypted_pixel)
    encrypted_image.save("encrypted_image.png")
    print("Image encrypted successfully!!")

def decrypt_image(image_path, key):
    encrypted_image = Image.open(image_path)
    decrypted_image = encrypted_image.copy()
    width, height = encrypted_image.size
    for y in range(height):
        for x in range(width):
            encrypted_pixel = encrypted_image.getpixel((x, y))
            decrypted_pixel = tuple((p - key) % 256 for p in encrypted_pixel)
            decrypted_image.putpixel((x, y), decrypted_pixel)
    decrypted_image.save("decrypted_image.png")
    print("Image decrypted successfully!!")

def main():
    print("1. Encrypt Image")
    print("2. Decrypt Image")
    choice = int(input("Enter your choice: "))
    if choice == 1:
        image_path = input("Enter path to the image to encrypt: ")
        key = int(input("Enter encryption key (an integer): "))
        encrypt_image(image_path, key)
    elif choice == 2:
        image_path = input("Enter path to the image to decrypt: ")
        key = int(input("Enter decryption key (an integer): "))
        decrypt_image(image_path, key)
    else:
        print("Invalid choice.")

if __name__ == "__main__":
    main()
