# MATSCI465_ShuhangXia
This was created in 2026.1.7. for MATSCI465 course. ^-^
This environment requires Python NumPy, SciPy, Matplotlib, HyperSpy and py4DSTEM.

### Project Structure Directory



# Assignment02：
Virtual Detectors allow you to "re-image" your sample after the experiment is finished, just as if you were still sitting at the microscope.

Data Foundation: 4D-STEM records a complete 2D diffraction pattern for every single pixel in the scanned area (creating a 4D dataset).

Post-Masking: Using computer algorithms, you generate a "virtual" shape (for example, a small circle for Bright Field or a ring for Dark Field).

Pixel Integration: The intensity of the electrons falling within that virtual shape is summed up for every diffraction frame to determine the brightness of the corresponding pixel in the final image.

Because the raw data contains information about all electrons, you can freely adjust the detector's size, shape, or position after the experiment. This allows you to extract Bright Field (BF), Annular Dark Field (ADF), or any specific angular image from the same data without needing to re-run the experiment.
