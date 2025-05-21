# Vision System

This directory contains the modules responsible for the visual processing capabilities of the TurboDrone project. It includes components for depth estimation, object detection, and potentially other visual tasks.

The main goal of this system is to process real-time video feeds from the drone to understand its environment, identify key features, and support navigation and mapping functionalities.

## Depth Processor

The `depth_processor` submodule is responsible for estimating depth from monocular (single camera) video feeds.

### `depth_estimator.py`

This script contains the `DepthEstimator` class, which is the core component for depth estimation.

**Key Features:**

*   **Real-time Estimation:** Designed to process video frames in real-time.
*   **Model:** Utilizes Apple's Depth Pro model for high-quality depth maps.
*   **Threaded Processing:** Employs a multi-threaded approach with input and output queues to prevent blocking the main application thread. This allows frames to be captured and processed asynchronously.
*   **Frame Management:** Includes a queue system to manage incoming frames and resulting depth maps.

**Usage:**

1.  **Initialization:**
    ```python
    from vision_system.depth_processor.depth_estimator import DepthEstimator
    estimator = DepthEstimator(max_queue_size=10)
    estimator.start()
    ```
2.  **Adding Frames:**
    ```python
    # Assuming 'frame' is a NumPy array (H, W, 3) from a video source
    estimator.add_frame(frame)
    ```
3.  **Getting Results:**
    ```python
    result = estimator.get_latest_result()
    if result:
        depth_map, fps = result
        # Process or display the depth_map
    ```
4.  **Stopping:**
    ```python
    estimator.stop()
    ```

### `test_depth_estimator.py`

This script provides a practical example of how to use the `DepthEstimator` class.

**Functionality:**

*   Captures video from the default camera.
*   Passes frames to the `DepthEstimator`.
*   Retrieves the estimated depth maps.
*   Visualizes both the original RGB frame and the resulting depth map side-by-side using OpenCV.
*   Displays current Frames Per Second (FPS).

**Running the Test:**

To run the test script, navigate to the `src/vision_system/depth_processor/` directory and execute:

```bash
python test_depth_estimator.py
```

Make sure you have a camera connected and the necessary dependencies (like OpenCV, PyTorch, and Depth Pro) installed in your environment.
