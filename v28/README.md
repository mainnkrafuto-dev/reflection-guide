# v28 OpenCV preprocessing experiment

This folder is an isolated experiment based on the existing v25 page. The root `index.html` is not changed.

## What changed
- Keeps the existing PP-OCRv5 recognition path.
- If the first OCR pass does not find all four rank labels, it optionally loads OpenCV.js.
- Applies grayscale + CLAHE contrast enhancement, then adaptive thresholding, and retries OCR on the enhanced variants.
- If OpenCV.js cannot load, the original OCR result is still used.

## Important limitation
This is an image-preprocessing fallback, **not** a trained visual detector or partial-character recognizer. It may help with low contrast or uneven lighting. It cannot reliably identify a rank when the relevant characters are fully occluded. A true shape/template detector needs representative rank-label samples and testing against screenshots, including occlusion cases.

## Test checklist
1. Normal screenshot: compare 1st-4th recognition and marker coordinates with v25.
2. Low-contrast screenshot: check whether the enhanced pass recovers missed labels.
3. Partially occluded rank label: record whether the fallback helps; do not assume success.
4. Confirm the page still works when the OpenCV CDN is blocked/offline.
5. Measure load time and recognition latency on iPhone Safari.

Do not merge into the production branch until these tests pass and the user approves.
