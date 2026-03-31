# Ex05 Image Carousel

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
### ImageCarousel.js
```
import { useState, useEffect } from "react";

export default function ImageCarousel() {
  const images = [
    "https://picsum.photos/id/1015/800/400",
    "https://picsum.photos/id/1016/800/400",
    "https://picsum.photos/id/1018/800/400",
    "https://picsum.photos/id/1020/800/400"
  ];

  const [currentIndex, setCurrentIndex] = useState(0);

  const nextImage = () => {
    setCurrentIndex((prev) => (prev + 1) % images.length);
  };

  const prevImage = () => {
    setCurrentIndex((prev) => (prev - 1 + images.length) % images.length);
  };

  useEffect(() => {
    const interval = setInterval(nextImage, 3000);
    return () => clearInterval(interval);
  }, []);

  return (
    <div
      style={{
        display: "flex",
        flexDirection: "column",
        alignItems: "center",
        justifyContent: "center",
        height: "100vh",
        backgroundColor: "#f5f5f5",
        fontFamily: "Arial"
      }}
    >
      {/* Title */}
      <h1 style={{ marginBottom: "20px" }}>Image Carousel</h1>

      {/* Carousel Box */}
      <div
        style={{
          position: "relative",
          width: "800px",
          height: "400px",
          overflow: "hidden",
          borderRadius: "15px",
          boxShadow: "0 8px 20px rgba(0,0,0,0.2)",
          backgroundColor: "white"
        }}
      >
        {/* Image */}
        <img
          src={images[currentIndex]}
          alt="carousel"
          style={{
            width: "100%",
            height: "100%",
            objectFit: "cover"
          }}
        />

        {/* Previous Button */}
        <button
          onClick={prevImage}
          style={{
            position: "absolute",
            top: "50%",
            left: "10px",
            transform: "translateY(-50%)",
            backgroundColor: "rgba(0,0,0,0.5)",
            color: "white",
            border: "none",
            padding: "10px",
            borderRadius: "50%",
            cursor: "pointer"
          }}
        >
          ◀
        </button>

        {/* Next Button */}
        <button
          onClick={nextImage}
          style={{
            position: "absolute",
            top: "50%",
            right: "10px",
            transform: "translateY(-50%)",
            backgroundColor: "rgba(0,0,0,0.5)",
            color: "white",
            border: "none",
            padding: "10px",
            borderRadius: "50%",
            cursor: "pointer"
          }}
        >
          ▶
        </button>
      </div>

      {/* Dots Indicator */}
      <div style={{ marginTop: "15px", display: "flex", gap: "10px" }}>
        {images.map((_, index) => (
          <div
            key={index}
            onClick={() => setCurrentIndex(index)}
            style={{
              width: "12px",
              height: "12px",
              borderRadius: "50%",
              backgroundColor: index === currentIndex ? "black" : "gray",
              cursor: "pointer"
            }}
          />
        ))}
      </div>
    </div>
  );
}
```
### App.js
```
import ImageCarousel from "./ImageCarousel";

function App() {
  return <ImageCarousel />;
}

export default App;
```
## OUTPUT
<img width="1907" height="911" alt="image" src="https://github.com/user-attachments/assets/eea16bd8-0aa0-4fa8-bd9d-c669b569d566" />


## RESULT
The program for creating Image Carousel using React is executed successfully.
