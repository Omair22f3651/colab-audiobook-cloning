Audiobook Generator with MMS-TTS in Google Colab
This project converts a PDF (e.g., Life 3.0 by Max Tegmark) into an audiobook using free, open-source tools in Google Colab. It extracts text from a PDF, generates speech with Hugging Face’s MMS-TTS model (approximating a user-provided voice sample), and merges audio into a single MP3. The project is built with Python 3.12.11 and versioned with Git.
Features

Extracts text from PDFs using PyPDF2.
Generates speech with facebook/mms-tts-eng, adjusted to mimic a user’s voice using librosa.
Merges audio chunks into an MP3 with pydub.
Runs in Google Colab with free GPU support.
Versioned in a Git repository for reproducibility.

Prerequisites

Google Colab account (free tier, T4 GPU recommended).
A PDF file (e.g., life3.0.pdf).
A voice sample (10-30 seconds, .m4a or .wav, clear and neutral tone).
GitHub account for cloning the repository.

Setup

Clone the Repository:
git clone https://github.com/your-username/colab-audiobook-project.git
cd colab-audiobook-project

Replace your-username with your GitHub username.

Open in Colab:

Upload Untitled1.ipynb to Google Colab (File > Upload notebook).
Alternatively, open directly via Colab’s GitHub integration:https://colab.research.google.com/github/your-username/colab-audiobook-project/blob/main/Untitled1.ipynb


Install Dependencies:Run the first cell in the notebook to install PyPDF2, pydub, and requests. For TTS, Cell 5 installs:
!pip install transformers==4.44.2 datasets==3.0.1 torchaudio==2.4.0 pydub==0.25.1 librosa==0.10.1 soundfile==0.12.1 numpy==1.26.0
!apt update && apt install -y ffmpeg


Prepare Files:

Upload your PDF (e.g., life3.0.pdf) and voice sample (e.g., voice_sample.m4a) when prompted by Cell 4.
Ensure the voice sample is 10-30 seconds, clear, and neutral for best results.


Switch to GPU:

Go to Runtime > Change runtime type > T4 GPU for faster audio generation (~0.5-1 second per chunk).



Usage

Run the Notebook:

Execute cells sequentially in Colab.
Cells 1-3: Install dependencies (PyPDF2, pydub, requests).
Cell 4: Upload PDF and voice sample, extract text, and create 4 chunks (9,452 characters).
Cell 5: Load MMS-TTS model (facebook/mms-tts-eng).
Cell 6: Generate audio chunks, adjusted to approximate your voice’s timbre.
Cell 7: Merge chunks into life_3.0_audiobook_mms.mp3 (~8-10 minutes) and download.


Expected Output:

Audio chunks in /content/tts_audio_chunks/ (e.g., chunk_000.wav to chunk_003.wav).
Final audiobook: life_3.0_audiobook_mms.mp3, downloaded via Colab.



File Structure
colab-audiobook-project/
├── Untitled1.ipynb       # Main notebook with audiobook generation code
├── .gitignore            # Excludes .wav, .mp3, .m4a, .pdf, and temp files
├── README.md             # This file

Note: Large files (life3.0.pdf, voice_sample.m4a, life_3.0_audiobook_mms.mp3) are excluded by .gitignore. Upload your own files when running the notebook.
Voice Approximation
MMS-TTS doesn’t support zero-shot voice cloning. Instead, librosa adjusts the generated audio’s RMS (timbre/energy) based on your voice sample. For true cloning, consider Coqui TTS with Python <=3.11 (requires Colab Python downgrade, not included here).
Troubleshooting

Tokenizer Error: Ensure Cell 5 completes without interruption. Verify tokenizer = AutoTokenizer.from_pretrained("facebook/mms-tts-eng").
Dependency Conflicts: If numpy issues arise, run:!pip install --force-reinstall numpy==1.26.0 transformers==4.44.2 datasets==3.0.1 torchaudio==2.4.0

Then restart runtime (Runtime > Restart runtime).
Memory Issues: Colab’s free tier (~12GB RAM, ~100GB disk) should suffice. If errors occur, reduce chunks in Cell 6 (e.g., text_chunks = text_chunks[:2]).
Voice Quality: If the output doesn’t resemble your voice, use a clearer, longer voice sample (20-30 seconds).
Colab Timeout: Save outputs to Google Drive (File > Download) or push to GitHub, as sessions reset after ~12 hours.

Contributing

Fork the repository.
Create a branch (git checkout -b feature/your-feature).
Commit changes (git commit -m "Add your feature").
Push to your fork (git push origin feature/your-feature).
Open a Pull Request.

License
MIT License. See LICENSE for details (if included in the repository).
Acknowledgments

Hugging Face for MMS-TTS (facebook/mms-tts-eng).
Google Colab for free GPU access.
PyPDF2, pydub, and librosa for text and audio processing.

Star the repo if you find this useful! 🚀 Questions? Open an issue or connect on LinkedIn.
