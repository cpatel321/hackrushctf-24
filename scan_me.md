Given bianry code simply was a 1 and 0 transcribed to pixels in a 2D array. I wrote a python script to convert pixel data to binary. 

```python

import cv2
import numpy as np


def image_to_block_binary(image_path, block_size=10):
  """Reads an image and converts 10x10 pixel blocks to 0 (all dark) or 1 (any light).

  Args:
      image_path: Path to the image file.
      block_size: Size of the square block (default: 10).

  Returns:
      A NumPy array with dimensions representing the image divided into blocks,
      where each value is 0 (all dark) or 1 (any light pixel within the block).
  """
  # Read the image in grayscale mode
  image = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)

  # Get image height, width, and number of channels (should be 1 for grayscale)
  image_height, image_width, channels = image.shape

  # Ensure block size doesn't exceed image dimensions
  block_size = min(block_size, image_height, image_width)

  # Calculate the number of blocks along each dimension (rounded down)
  num_blocks_height = image_height // block_size
  num_blocks_width = image_width // block_size

  # Create an empty array to store the block-level binary values
  block_binary_image = np.zeros((num_blocks_height, num_blocks_width), dtype=np.uint8)

  # Loop through each block
  for y in range(num_blocks_height):
    for x in range(num_blocks_width):
      # Get the starting pixel coordinates for the current block
      start_y = y * block_size
      start_x = x * block_size

      # Extract the block of pixels
      block = image[start_y:start_y + block_size, start_x:start_x + block_size]

      # Check if any pixel in the block is light (greater than threshold)
      is_any_light = np.any(block > 127)

      # Set the block value in the binary image (1 for any light, 0 for all dark)
      block_binary_image[y, x] = 1 if is_any_light else 0

  return block_binary_image


# Example usage
image_path = "path/to/your/image.jpg"
block_size = 10
block_binary_image = image_to_block_binary(image_path, block_size)

# Print the block-level binary image
print(block_binary_image)

```

The output of the script was the binary data of the image. I then converted the binary data to ASCII and got the flag.

Flag is HRCTF{h0p3fully_7h15_w45n'7}

