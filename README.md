# Traffic-Flow-Analysis-Task

1. Requirements
-Python: Version 3.8 or later

-Operating System: Windows (Linux/Mac supported but paths may differ)

-Internet Connection: Required for:

-Downloading YouTube traffic video

-Downloading YOLO model weights

Hardware:

-GPU recommended for faster processing

-CPU will work (slower)

2. Install Dependencies
-Open a terminal or command prompt and run:

--pip install yt-dlp ultralytics opencv-python pandas filterpy scipy

Dependency Details:

-yt-dlp → Downloads YouTube traffic video

-ultralytics → YOLOv8 object detection

-opencv-python → Video frame processing & overlay drawing

-pandas → CSV file creation and manipulation

-filterpy → Kalman Filter for SORT tracking

-scipy → IOU computation and Hungarian algorithm for tracking

3. Prepare the Script
-Save the Python code (provided separately) as:

    traffic_flow_analysis.py

4. Run the Script
-In terminal or command prompt:

    python traffic_flow_analysis.py

5. What the Script Does
-Downloads YouTube Video as traffic.mp4.

-Loads YOLOv8 model (yolov8n.pt) to detect vehicles:

-Car → COCO ID: 2

-Motorcycle → 3

-Bus → 5

-Truck → 7

--Implements SORT tracking to assign a unique ID to each detected vehicle.

Defines Lane Boundaries:

lanes_x = [300, 600, 900]
-Lane 1 → x < 300

-Lane 2 → 300 ≤ x < 600

-Lane 3 → x ≥ 600

-Counts Vehicles per Lane (only once per unique ID to avoid duplicates).

Overlays on Video:

-Yellow lane boundary lines

-Blue bounding boxes for vehicles

-Green text showing vehicle ID & lane number

-Yellow text with real-time lane counts

Saves Outputs:

-processed_traffic.mp4 → Annotated output video
-traffic_analysis.csv → Detailed vehicle log:
-Vehicle_ID, Lane, Frame, Timestamp
-Console summary with total counts per lane

6. Output Files
-After execution, you will have:

-traffic.mp4 → Downloaded YouTube traffic video

-processed_traffic.mp4 → Video with lane overlays & counts

-traffic_analysis.csv → CSV log of detected vehicles

  Example CSV:

  Vehicle_ID,Lane,Frame,Timestamp
1,1,15,0.50
2,2,20,0.66
3,3,22,0.73

  Example Console Output:
=== Final Vehicle Counts ===
Lane 1: 167
Lane 2: 234
Lane 3: 2359

7. Customization
-Change Lane Boundaries
   Edit in script:
      lanes_x = [300, 600, 900]
-Adjust values to match your video’s perspective.

-Change Detected Vehicle Classes
   Inside detection loop:
       if cls in [2, 3, 5, 7]:
       COCO IDs: car=2, motorcycle=3, bus=5, truck=7

-Model Accuracy vs Speed

    model = YOLO("yolov8n.pt")  # Nano: fastest, least accurate
    model = YOLO("yolov8s.pt")  # Small: more accurate, slower

8. Notes
-CPU mode will be slower than GPU.

-Script overwrites previous processed_traffic.mp4 and traffic_analysis.csv.

Works best with:

-Fixed camera

-Clear lane markings

-Current version uses vertical lane lines — for curves, polygon-based lane detection should be implemented.
