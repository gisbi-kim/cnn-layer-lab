# CNN Layer Lab

Browser-based CNN teaching lab for MNIST and Fashion-MNIST.

Live page: https://gisbi-kim.github.io/cnn-layer-lab/

This page is designed for classroom use: students can load a small CNN in the browser, train it one epoch at a time, inspect intermediate feature maps, and compare how the same network behaves on transformed datasets.

## What Students Can Try

- Train a CNN directly in the browser with TensorFlow.js.
- Step through training one epoch at a time instead of running all epochs automatically.
- Watch loss, prediction probabilities, and full test-set accuracy change after each epoch.
- Inspect all convolution and pooling feature maps at once.
- Change the number of convolution layers from 1 to 5.
- Compare MNIST, Fashion-MNIST, inverted images, low-contrast images, shifted images, noisy images, and mixed-label images.
- Save trained weights in the browser and reload them later for generalization tests.
- Delete saved weights from the browser when an experiment is no longer needed.

## Dataset Options

The dataset selector currently includes:

- MNIST original
- MNIST inverted
- MNIST noisy
- MNIST shifted right
- MNIST low contrast
- MNIST digit mix 80/20
- MNIST digit mix 50/50
- Fashion-MNIST
- Fashion-MNIST inverted
- Fashion-MNIST mix 70/30

For the 50/50 MNIST mix, either of the two mixed digits is counted as correct during evaluation. For 80/20 and 70/30 mixes, the dominant class is treated as the main answer.

## Teaching Flow

1. Load MNIST original and show that the input is a 28x28 grayscale image.
2. Train one epoch and compare prediction probabilities before and after training.
3. Open the feature-map view and compare early convolution maps with later maps.
4. Run full test-set evaluation and discuss why single samples are not enough.
5. Change the dataset to low contrast, noise, shift, or mix variants and test generalization.
6. Switch to Fashion-MNIST and ask why the same 28x28 image format becomes a harder classification problem.
7. Change the number of convolution layers and compare speed, accuracy, and feature maps.

## Generalization Test With Saved Weights

Weights are saved to the browser's local IndexedDB storage through TensorFlow.js. This means a saved model is available later on the same device and browser, without a server.

Example classroom flow:

1. Select `MNIST low contrast`.
2. Load data and train for several epochs.
3. Click `Save current weights`.
4. Switch the dataset to `MNIST original` and load data again.
5. Select the saved weight entry.
6. Click `Load pretrained weight`.
7. Compare the full test-set accuracy against the model trained directly on the original dataset.

Saved weight names include the training dataset, convolution-layer count, epoch count, training sample count, and save time. For example, a name may indicate that the model was trained on low-contrast MNIST with 2 convolution layers for 10 epochs.

The delete button removes the selected saved model from the browser's IndexedDB storage and removes it from the dropdown.

## Classroom Questions

- Why is the prediction almost random before training?
- Which feature maps look like edges, strokes, or local parts?
- Does a higher epoch count always improve test accuracy?
- How does test accuracy differ from one manually selected sample?
- What happens when the image is low contrast or color-inverted?
- Why might Fashion-MNIST be harder than digit MNIST?
- When two digits are mixed, what should the "correct" answer mean?

## Local Run

This is a static page. A local web server is recommended because the browser loads external TF.js and image assets.

```bash
python3 -m http.server 8765
```

Then open:

```text
http://127.0.0.1:8765/index.html
```

## Deployment

The site is hosted with GitHub Pages from the `main` branch root.

After editing `index.html`:

```bash
git add index.html README.md teacher_note.md
git commit -m "Update CNN Layer Lab"
git push
```

GitHub Pages may take a short time to rebuild after each push.

## Data And Runtime Notes

- The app uses TensorFlow.js in the browser.
- Training and evaluation run on the visitor's own computer.
- Saved weights stay in the visitor's browser IndexedDB storage.
- MNIST and Fashion-MNIST image/label files are loaded from public browser-friendly data files.
- No server-side training code is required.
- Large test-set evaluation may take longer on slow student laptops, but the default setting evaluates the full loaded test set.

## Files

- `index.html`: the complete interactive lab.
- `teacher_note.md`: instructor-facing lesson flow and report prompts.
