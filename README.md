# Image-to-pencil-sketch
import cv2

def convert_to_pencil_sketch(image_path):
    # Load the image
    image = cv2.imread(image_path)

    if image is None:
        print("Error: Image not found or cannot be loaded.")
        return

    # Convert the image to grayscale
    gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

    # Invert the grayscale image
    inverted_gray_image = 255 - gray_image

    # Apply GaussianBlur to the inverted image
    blurred_image = cv2.GaussianBlur(inverted_gray_image, (21, 21), sigmaX=0, sigmaY=0)

    # Invert the blurred image
    inverted_blurred_image = 255 - blurred_image

    # Create the pencil sketch image by dividing the grayscale image by the inverted blurred image
    pencil_sketch_image = cv2.divide(gray_image, inverted_blurred_image, scale=256.0)

    # Show the original and pencil sketch images side by side
    cv2.imshow("Original Image", image)
    cv2.imshow("Pencil Sketch", pencil_sketch_image)

    # Wait until a key is pressed or the windows are closed
    cv2.waitKey(0)
    cv2.destroyAllWindows()

if __name__ == "__main__":
    image_path ="path to image.jpg"
    convert_to_pencil_sketch(image_path)
#replace path to image.jpg with the real image path.
