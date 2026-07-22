# VLF-Direction-Finding-Grabber
An advanced, browser-based tool for real-time Very Low Frequency (VLF) signal analysis, bearing extraction, and geographic triangulation.

Linked to: VLF Maps MultiPortal with link & pre-filled questions to AI,ML,LLM,& GenAI. https://github.com/GiamMaBasedResearchers/VLFMONITORING

Thanks especially to the VLF & LF Group that allows us these analyzes with publicly available data!

[https://www.ecmwf.int/ , http://astria.tacc.utexas.edu/AstriaGraph/, http://astria.tacc.utexas.edu/AstriaGraph/, https://rom-saf.eumetsat.int/](https://www.qsl.net/dl4yhf/spectra1.html) , DL0AO VLF-Grabber near Amberg, JN59VK https://vlf.u01.de/ , VLF Grabber in Nürnberg, JN59NJ https://df6nm.de/vlf/vlfgrabber.htm

Obviously, there will be several fixes to be made, and the code isn't clean, and you will find entities that appear to be false positives but are not always false positives. I consider the exercise very interesting for various levels of understanding, knowledge and technicalities.

As always, you can use the plain HTML locally 👋👋👋

To preview GitHub HTML files, use these services by pasting the link [https://github.com/GiamMaBasedResearchers/VLFMONITORING/blob/main/index.html](https://github.com/GiamMaBasedResearchers/VLF-Direction-Finding-Grabber/blob/main/VLF_DF%202.html)

https://htmlpreview.github.io/?

https://raw.githack.com/ (Tested / working)

Thanks to:

https://github.com/neoascetic/rawgithack

https://github.com/htmlpreview/htmlpreview.github.com (Tested / working)


🛰️ VLF Direction Finding Grabber


<img width="1917" height="922" alt="image" src="https://github.com/user-attachments/assets/933348fd-06e6-4d0c-8548-69beea934afc" />



An advanced, browser-based tool for real-time Very Low Frequency (VLF) signal analysis, bearing extraction, and geographic triangulation. This application interfaces with live remote spectrogram feeds to detect signal anomalies, extract directional data from visual compass overlays, and plot multi-station triangulations on interactive 2D and 3D maps.
🌟 Key Features
1. Advanced Spectrogram Analysis

     Multi-Station Support: Simultaneously monitors up to three remote VLF receivers (e.g., DF6NM Nurnberg, VLF-4 Amber, VLF-10 Amber).
     Time/Frequency Synchronization: Click anywhere on a spectrogram to instantly sync the time and frequency across all active stations. (Shortcut: Shift + Click to sync auto-detection across all panels).
     Calibration Tools: Built-in utilities to calibrate Frequency (FCAL) and Time (TCAL) mappings directly from the spectrogram pixels.
     Local Image Loading: Bypass CORS restrictions or analyze historical data by loading local images via the FILE button. Includes a direct download button for capturing current frames.

2. High-Precision Pixel Recognition & Lens

     Interactive Magnifier (Lens): A high-zoom lens follows the cursor, providing exact pixel RGB and HSV values in real-time.
     Signal Color Sampling: Intelligent color detection algorithm that scans a localized radius around the cursor to find faint signal traces (reds/oranges) even when the exact center pixel is dark.

3. Compass Bearing Extraction

     Center of Mass Auto-Centering (AC): A highly optimized, anti-freeze algorithm that reads the compass region's pixel data only once and calculates the true center of the compass dial using a weighted Center of Mass approach. 
     HSV Color-Space Filtering: Extracts bearing angles by converting pixels to HSV, applying strict noise filters to ignore JPEG artifacts, and isolating the target signal needle.
     180° & 360° Compass Support: Fully supports both unidirectional (360°) and bidirectional (180° x2) compass displays, automatically calculating the opposite bearing for 180° setups.

4. Geographic Triangulation & Mapping

     2D Interactive Map (Leaflet): Plots receiver locations and projects great-circle bearing lines. Automatically calculates and marks the intersection points (signal origins) when multiple bearings are available.
     3D Globe Visualization (Three.js): Switch to a 3D wireframe globe to visualize bearing trajectories and spatial relationships in a three-dimensional context.
     Signal Tracker: A built-in manager to add, track, and clear multiple signal frequencies and their corresponding bearings.

🛠️ Technology Stack

     Core: Vanilla JavaScript (ES6 Modules) — no heavy frameworks, ensuring lightning-fast DOM manipulation and canvas rendering.
     Styling: Tailwind CSS combined with custom CSS variables for a dark, sleek, "control-room" aesthetic.
     Mapping (2D): Leaflet.js with CartoDB Dark Matter tiles.
     Mapping (3D): Three.js for WebGL globe rendering.
     Icons: Font Awesome.
     Fonts: JetBrains Mono & Orbitron.

⚙️ How It Works
The Auto-Center Algorithm

Previous brute-force methods caused UI freezing by iteratively testing hundreds of center coordinates. This updated version utilizes a Center of Mass algorithm:

    It defines a bounding box around the estimated compass area.
    It reads the ImageData array exactly once.
    It iterates through the pixels, applying a strict HSV filter (saturation > 0.15, value > 0.12) to find colored compass elements.
    It calculates the weighted centroid of these pixels, instantly returning the exact compass center with a quality score based on pixel count.

Bearing Calculation

Once the center is established, the application reads the circular region around the compass. For every valid colored pixel, it calculates the angle relative to the center using Math.atan2. These angles are aggregated into a 360-bin array, smoothed, and sorted to find the strongest peaks. If a target hue is provided (via the color picker), it weighs the peaks based on hue proximity to ensure the correct signal is selected.
📡 Data Sources & References

This tool is designed to interface with standard VLF grabber formats. Default configurations are provided for:

     DF6NM Nurnberg (Germany) — 360° Compass
     VLF-4 Amber (Germany) — 360° Compass
     VLF-10 Amber (Germany) — 180° Compass

VLF signal monitoring concepts and spectrogram formats are based on standards from the VLF community and SID Laboratories.
🚀 Usage Guide

    Load Images: The app automatically fetches live images every 30 seconds. For pixel-accurate reading, click FILE to load a local copy (this enables all reading features).
    Calibrate (Optional): Use FCAL and TCAL to align the grid with the spectrogram's axes. Use COMP to manually set the compass center and radius if Auto-Center fails.
    Read Bearings: 
         Click directly on a compass to manually set a bearing.
         Click READ to automatically detect the bearing based on the color currently selected in the CLR picker.
         Click AC to force Auto-Center recalculation.
    Track Signals: Enter a frequency in the SIGNAL TRACKER box and click DF. The app will gather all current bearings, draw lines on the map, and calculate the intersection.
    Export Config: Click EXPORT in the top bar to generate a JSON snapshot of your current calibration settings.


⚠️ Disclaimer

Disclaimer: The code is for educational, training, analysis, & security purposes, & is intended for understanding & knowledge. The authors assume no liability for the misuse of this tool or the data it visualizes. Always ensure you have permission to access and visualize telemetry data.

Credits

This code provide from: "GiamMa-based researchers SDR R&D IoT" | @GiammaIoT2 License

This project is provided for research and educational purposes.
