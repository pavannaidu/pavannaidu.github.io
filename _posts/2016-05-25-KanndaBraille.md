---
title: 'Bridging Accessibility: Developing a Kannada Text to Braille Interpreter'
date: 2016-05-25
permalink: /posts/2016/05/KanndaBraille/
tags:
  - OCR
  - Neural Network
---

Our team developed a Kannada Text to Braille Interpreter system to address the limited availability of Braille materials in Kannada. This innovative project utilizes Optical Character Recognition (OCR) technology to convert scanned Kannada text into Braille format, enhancing accessibility for visually impaired individuals. The system integrates preprocessing, segmentation, and character recognition techniques to achieve an average accuracy of 71% in text recognition.

Methodology
------
* Twitter: Initially 69527 rows, 41 columns; preprocessed to 22703 rows, 5 columns.
* Non-Twitter: Initially 443183 rows, 41 columns; preprocessed to 300844 rows, 5 columns.

Methodology
------
Our approach involved several key steps:
* **Image Preprocessing**: We used Otsu's thresholding method to binarize the input image and applied noise reduction techniques.
* **Segmentation**: The system segments the text into lines, words, and individual characters using connected component analysis and projection profiles.
* **Character Recognition**: We employed the Tesseract OCR engine, customized for Kannada script, to recognize individual characters.
* **Braille Mapping**: Recognized Kannada characters are mapped to their corresponding Braille Unicode values.
* **GUI Development**: We created a user-friendly MATLAB GUI for easy interaction with the system.

Key Findings
------
* The system achieved an average text recognition accuracy of 71% across multiple pages of Kannada text.
* Tesseract OCR engine, when combined with custom segmentation techniques, proved effective for Kannada character recognition.
* The GUI allows users to easily process images, view recognized text, and generate Braille output.
* The system can handle complex Kannada characters, including those with attached vowel modifiers (vattus).


Final thoughts
------
This project represents a significant step towards improving accessibility of Kannada literature for visually impaired individuals. While the current accuracy is promising, there's room for improvement through further refinement of the recognition algorithms and expansion of the training dataset. Future enhancements could include developing a mobile application version and integrating with Braille embossing printers for direct output.

> Team: Pradyumna B Shetty, Priyanka P, S Abhinandan and Pavan Naidu. Under the guidance of Dr. T Shreekanth, Assistant Professor, Dept. of E & C, SJCE, Mysuru.