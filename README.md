#### Industry dashboard data extraction
###### Codes Logic
For all the data extraction tasks, they all followed these steps: 
	Image extraction (rotated and captured the useful content)
	Pre-processing (grey scale, denoised, sharpened, inverted, etc)
	Recognition (using pytesseract, PaddleOCR, opencv template matching, contour detection, geometric reasoning, etc)
	Output results (in csv and annoted image)  
Because I don’t have enough data for model training, so I didn’t use neural networks ML model (like CNN), instead I used the light-scale method like pytesseract, PaddleOCR, etc. It will be less accurate, but the cost of training is also be reduced.
For error handling, I returned N for unreadable position.
######  Findings
Performance of different methods:
	For tesseract, it’s more useful when handling the single number. So mainly I used it in reading digit numbers. And before recognizing, I segmented the digit string into separate digit squares, and use tesseract to read one by one, return N for unreadable digit.
	For PaddleOCR, it’s more suitable for extracting a string of content (mixture of text and numbers) with regular shape and clear boundaries. So mainly I used it in timestamp reading.
	For opencv template matching, I tried to use it to recognize the unreadable numbers. But it didn’t work properly and will match wrong number. So while doing error handling, I need to trade tradeoff between accuracy and quantity. And I chose accuracy for priority.
	For contour detection, geometric reasoning, I used it in reading circle dial numbers. The basic idea is to find the circle outline, find the center of the circle, find the dial hand, calculate the angle of the hand and convert the angle into numbers. It worked quite well if the images have been processed properly.
