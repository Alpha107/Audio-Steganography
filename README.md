# Audio-Steganography

## DCT

This code implements an audio steganography technique, where a secret audio signal is embedded into a cover audio signal using the Discrete Cosine Transform (DCT). The DCT, commonly used in image and audio processing, transforms the audio signals from the time domain into the frequency domain, allowing for embedding with minimal perceptual distortion. After embedding, the secret audio can be extracted from the stego (modified) audio.

## Steps Involved: 

### **1. Loading Audio Files:**
The function load_audio(file_path, target_sr) is responsible for loading the cover and secret audio files. These audio signals are resampled to the specified sample rate (44.1 kHz by default).

Both the cover and secret files are transformed into a single-channel (mono) numpy array of audio samples. If any audio is stereo, the first channel is selected.

### **2. Embedding the Secret Audio**
The main task of the program is to hide the secret audio within the cover audio using DCT. This is done by the embed_secret_into_cover(cover, secret, alpha) function.

DCT-Based Embedding:

**Step 1: Apply DCT:** Both cover and secret audios are transformed into the frequency domain using DCT.

**Step 2: Embed the Secret:** The DCT coefficients of the secret are added to the cover’s DCT coefficients, with a strength factor alpha (default 0.1) to control the embedding strength. This ensures that the secret audio is blended without excessively distorting the cover audio.

**Step 3: Inverse DCT:** After embedding, the modified DCT coefficients are transformed back into the time domain using inverse DCT (IDCT) to form the stego audio.

## **3. Saving the Stego Audio**
Once the secret audio has been embedded into the cover audio, the stego audio is saved to a file using save_audio(file_path, audio, sr).

**4. Extracting the Secret Audio**
The embedded secret audio is extracted using the extract_secret_from_stego(stego, cover, alpha) function, which effectively reverses the embedding process.

DCT-Based Extraction:
Step 1: Apply DCT: The DCT is applied to both the stego audio and the original cover audio.

Step 2: Extract the Secret: The secret audio is recovered by subtracting the cover's DCT coefficients from the stego’s and dividing by the embedding strength alpha.

Step 3: Inverse DCT: The recovered DCT coefficients are transformed back into the time domain using IDCT.

The extracted secret audio is then saved to a file for comparison

**5. Metrics: MSE and SNR Calculation**
To evaluate the quality of the embedding and extraction process, two metrics are computed:

Mean Squared Error (MSE): This measures the difference between the original secret and the extracted secret. A lower value indicates better quality.

Signal-to-Noise Ratio (SNR): This measures the amount of noise introduced during the embedding process. A higher SNR indicates better preservation of the original signal.

**6. Visualizing and Analyzing Results**

The program provides various visualizations to compare the original, stego, and extracted signals:

Waveform Comparisons:
Waveform of Cover vs Stego: This shows how much the stego audio deviates from the cover audio.

Waveform of Original Secret vs Extracted Secret: This compares the original secret and the extracted secret.

Spectrogram Analysis:
Spectrograms visualize the frequency content of audio signals over time, which helps identify differences between the cover, stego, and extracted secret signals.

RMS Energy Comparison:
Root Mean Square (RMS) values show the average energy of the audio signals. Comparing RMS values of the cover, stego, and extracted secret reveals how much energy distortion is introduced during the embedding and extraction processes.

Histogram and Correlation:
- Amplitude Histograms for cover, stego, and extracted secret signals provide insight into how the amplitude distribution changes after embedding and extraction.

- Correlation Plot: This shows the correlation between cover and stego audio, highlighting how closely the two waveforms match after embedding.








