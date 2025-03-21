# MeloTTS Demo WebUI

This is an unofficial web-based demonstration of the MeloTTS text-to-speech (TTS) system.  MeloTTS is a high-quality, multi-lingual TTS engine. This WebUI allows you to easily generate speech from text in various languages and with different speaker voices.

**HF Spaces Demo:** A live demo is also available on Hugging Face Spaces: [https://huggingface.co/spaces/mrfakename/MeloTTS](https://huggingface.co/spaces/mrfakename/MeloTTS)

**GitHub Repository (Original MeloTTS):** [https://github.com/myshell-ai/MeloTTS](https://github.com/myshell-ai/MeloTTS)

**Demo Author:** [mrfakename](https://twitter.com/realmrfakename)

## Features

*   **Multi-lingual Support:**  Generates speech in English (EN), Spanish (ES), French (FR), Chinese (ZH), Japanese (JP), and Korean (KR).
*   **Multiple Speakers:**  Offers a selection of speaker voices for each language (where available).  Be sure to explore different speakers, such as "EN-Default," for varied results.
*   **Adjustable Speed:** Controls the speaking rate from 0.1 (very slow) to 10.0 (very fast).
*   **Simple Interface:**  Uses Gradio for an intuitive web interface.
*   **Progress Bar:** Displays a progress bar during synthesis.
*   **API Access:**  Provides API endpoints for programmatic use.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine.

### Prerequisites

1.  **Python:** Requires Python 3.x.
2.  **Dependencies:** You'll need to install the necessary Python packages.  The code includes these key libraries:
    *   `gradio`: For the web interface.
    *   `torch`:  PyTorch, for the underlying TTS model.  It will attempt to use a CUDA-enabled GPU if available, otherwise it will fall back to CPU.
    *   `unidic`: Needed for Japanese support, will be downloaded in setup.
    *   `nltk`: Used for natural language processing, specifically parts of speech tagging.
    *   `melo` (presumably a local module - see Installation).  This is the core MeloTTS library.

### Installation

1.  **Clone the Repository (or download the code):**

    ```bash
    git clone <repository_url>  # Replace <repository_url> if you have the code in a repo
    cd <repository_directory> # Navigate into project
    ```
    If you don't use Git, download the provided code as a ZIP file and extract it.

2.  **Install Dependencies:**

    ```bash
    pip install -r requirements.txt
    ```
    Create `requirements.txt` file and add these libraries:
    ```txt
        gradio
        torch
        unidic-lite
        nltk
    ```
    **Important:** The provided code assumes a local module named `melo`.  You'll likely need to obtain this from the official MeloTTS repository ([https://github.com/myshell-ai/MeloTTS](https://github.com/myshell-ai/MeloTTS)) and place it in the same directory as the script, or adjust the import statement accordingly.  You may need to adapt the `melo` directory structure to work as a local module.

3.  **Download unidic:**
    This step is essential for Japanese language support. The code executes it automatically.

    ```bash
    python -m unidic download
    ```

4.  **Download NLTK resources:**

    ```bash
    python -c "import nltk; nltk.download('averaged_perceptron_tagger_eng')"
    ```
    The code includes this download command.  This downloads the English part-of-speech tagger.

### Running the WebUI

1.  **Execute the Python Script:**

    ```bash
    python your_script_name.py  # Replace with the actual filename
    ```

2.  **Access the Web Interface:**
    The script will launch a local web server.  Gradio will typically provide a URL like `http://127.0.0.1:7860` in your console.  Open this URL in your web browser.

## Usage

1.  **Select a Language:** Choose from the available languages (EN, ES, FR, ZH, JP, KR) using the radio buttons.
2.  **Select a Speaker:** Choose a speaker from the dropdown menu. The available speakers will change depending on the selected language.
3.  **Enter Text:** Type or paste the text you want to synthesize into the "Text to speak" textbox.  Default text is provided for each language.
4.  **Adjust Speed (Optional):** Use the slider to control the speaking speed.
5.  **Synthesize:** Click the "Synthesize" button.  A progress bar will appear while the audio is being generated.
6.  **Listen:** Once the synthesis is complete, the generated audio will be available in the audio player.

## API Usage

The Gradio app also exposes an API, which is enabled with `demo.queue(api_open=True)`.  The `launch(show_api=True)` call displays the API documentation in the Gradio interface. You can use this to integrate the TTS functionality into other applications.  The main API function is `/predict`, which corresponds to the `synthesize` function.

The API takes the following inputs (as JSON):

*   `text` (str): The text to synthesize.
*   `speaker` (str): The name of the speaker.
*   `speed` (float): The speaking speed.
*   `language` (str): The language code (e.g., "EN").

The API returns the audio data as a base64-encoded WAV file.

## Troubleshooting

*   **`melo` module not found:** Ensure that the `melo` directory (from the MeloTTS repository) is correctly placed and importable. You might need to create an `__init__.py` file inside the `melo` directory to make it a proper Python package.
*   **CUDA out of memory:** If you encounter CUDA memory errors, try reducing the batch size or other memory-intensive operations within the `melo` library (if possible).  If that doesn't work, you may need to run the model on the CPU by changing `device = 'cuda'` to `device = 'cpu'`, although this will be significantly slower.
*   **Slow synthesis:** Speech synthesis can be computationally intensive. Using a GPU significantly speeds up the process. If you're using a CPU, synthesis will take longer.
*  **Gradio Interface Issues:** Ensure that you have a compatible browser and that JavaScript is enabled.

## Key improvements and explanations in this README:

*   **Clearer Prerequisites:** Separates Python installation from package dependencies.
*   **Explicit Installation:** Provides `pip install -r requirements.txt` instructions with `requirements.txt` file.
*   **`melo` Module Handling:**  Clearly explains the dependency on the `melo` module and how to handle it.  This is crucial, as the provided code won't work without it.
*   **Unidic and NLTK:** Explains *why* these are needed.
*   **Step-by-step Running:**  Makes it easy to follow the execution process.
*   **Detailed Usage Instructions:** Explains each part of the UI.
*   **API Documentation:**  Describes how to use the API.
*   **Troubleshooting:**  Addresses common issues users might encounter.
*   **Markdown Formatting:** Uses proper Markdown for readability.
*   **HF Spaces and GitHub Links:**  Includes links to the live demo and the original project.
*   **Concise and Organized:** Presents the information logically.
