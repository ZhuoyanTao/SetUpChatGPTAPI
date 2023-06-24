# Setting Up OpenAI API on Mac

  This guide will walk you through the process of setting up the OpenAI API on your Mac computer from the very start to end.

## Requirements

- macOS (latest version recommended)
- Python 3.6 or newer
- pip (Python package installer)
- OpenAI API key
- A VPN service (depending on the internet restrictions)

## Prerequisites -- Python, Pip, Virtual Environment

  **1.Install Python and pip**
   
   _Mac OS X comes with Python 2.7 out of the box between versions 10.8 and 12.3. If your Mac OS X version is between these versions, you do not need to install or configure anything else to use Python 2. However, this version of Python is great for learning, but not suitable for development. The Python version that ships with OS X may be out of date from the official current Python release, which is considered the stable production version._

   To install a more recent version of Python and the package manager pip, follow these steps:

   Install GCC by downloading Xcode, the smaller Command Line Tools (you must have an Apple account) or the even smaller OSX-GCC-Installer package. If you already have Xcode installed, do not install OSX-GCC-Installer as they can cause issues together. If you perform a fresh install of Xcode, you will also need to add the command-line tools by running the following command in the terminal:
   
   ```shell
   $ xcode-select --install
   ```
   

   Install Homebrew, a package manager that fills a void in OS X. 
   Open Terminal or your favorite OS X terminal emulator and run the following command:
   ```shell
   $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
   ```

   This script will explain what changes it will make and prompt you before the installation begins. Once you've installed Homebrew, insert the Homebrew directory at the top of your PATH environment variable. You can do this by adding the following line at the bottom of your ~/.profile file:
   ```shell
   $ export PATH="/usr/local/opt/python/libexec/bin:$PATH"
   ```
   If you have OS X 10.12 (Sierra) or older use this line instead:

   ```shell
   $ export PATH=/usr/local/bin:/usr/local/sbin:$PATH
   ```

   Now you can install Python 3 by running

   ```shell
   $ brew install python
   ```

  Homebrew also installs pip pointing to the Homebrew’d Python 3 for you.

  At this point, you have the system Python 2.7 available, potentially the Homebrew version of Python 2 installed, and the Homebrew version of Python 3 as well. Running python will launch the Homebrew-installed Python 3 interpreter. If the Homebrew version of Python 2 is installed then pip2 will point to Python 2. If the Homebrew version of Python 3 is installed then pip will point to Python 3. The rest of the guide will assume that python references Python 3【26†source】.

  **2. Set Up Virtual Environments**
  The next step is to install Anaconda, so you can install dependencies and manage virtual environments. A Virtual Environment is a tool to keep the dependencies required by different projects in separate places, by creating virtual Python environments for them. It solves the “Project X depends on version 1.x but, Project Y needs 4.x” dilemma, and keeps your global site-packages directory clean and manageable.

  While this tutorial should lead you through the entire process without the need of clicking on external links, in the case of errors, please refer to instructions on [Anaconda's official documentation](https://docs.anaconda.com/anaconda/install/mac-os/#macos-graphical-install) to install Anaconda on your macOS machine. After downloading the installer, open a terminal window and run the following:

 ```bash
 bash ~/Downloads/Anaconda3-2020.05-MacOSX-x86_64.sh
 ```
  **If this error message pop up in the terminal**
  ```shell
  zsh: command not found: conda
  ```
  **run the following command:**
  ```shell
  echo 'export PATH="/Users/username/anaconda3/bin:$PATH"' >> ~/.zshrc
  ```

 To **verify** your installation, you can use the following command:

 ```bash
 conda --version
 ```

  **3. Create a virtual environment**
  Creating a virtual environment with Anaconda is straightforward. The command will look something like this:

   ```bash
   conda create --name myenv
   ```

  Replace myenv with the name of your virtual environment.

_Congratulations on setting up everything we need, now let's get to the meat!_

 ## Steps

  **1. Activate the virtual environment**
  Before you start using the virtual environment, you need to activate it. You can do this with the following command:
  (notice (base) on the very left of your command line part, this should change to the name of your conda environment after running the following command 
  ```bash
  conda activate myenv
  ```
  Replace myenv with the name of your virtual environment (that you created in the "Create a virtual environment" section).
  
  
  **2. Install the OpenAI Python client**

   Open Terminal and run the following command:

   ```shell
   $ pip install openai
   ```

  **3. Get your OpenAI API key**

   You need to apply for an API key from OpenAI. Visit the OpenAI website and follow the steps to apply for access. If approved, you will receive an API key.

  **4. Setup your OpenAI API key**

   You should save your API key in your environment variables for easy access. In Terminal, run:

   ```shell
   echo "export OPENAI_API_KEY='your-api-key'" >> ~/.bash_profile
   source ~/.bash_profile
   ```

   _Replace your-api-key with your actual API key._
   **Remember every time you change your API key, you need to run both commands above, not just the first one**

  **5. Verify the setup**

   You can verify the setup by running a simple script that uses the OpenAI API. Here's a basic example:

   ```python
  import openai
  import os
  
  openai.api_key = os.getenv("OPENAI_API_KEY")
  
  response = openai.Completion.create(
    engine="text-davinci-002",
    prompt="Translate the following French text to English: '{Zhuoyan Tao est un tel être humain talentueux}'",
    max_tokens=60
  )
  response = openai.Completion.create(
    engine="text-davinci-002",
    prompt="Translate the following French text to Chinese, don't translate the name: '{Zhuoyan Tao est un tel être humain talentueux}'",
    max_tokens=60
  )
  response = openai.Completion.create(
    engine="text-davinci-002",
    prompt="draw an ASCII heart",
    max_tokens=60
  )

print(response.choices[0].text.strip())

   
   ```

   Save this script to a file, say test_openai.py, and run it using:

   ```shell
   python3 test_openai.py
   ```
  **If you encounter this error message:**
  ```shell
  openai.error.RateLimitError: You exceeded your current quota, please check your plan and billing details.
  ```
  **It means you either did not register for an API plan (this is separate from chatGPT plan), or you have exceeded the quota for number of tokens for this month.**

  **6. Setting up a VPN**

   Depending on the current internet restrictions in China, you may need to use a VPN to access the OpenAI API. Choose a reliable VPN service, install it on your Mac and connect to a server. Please note that using a VPN should comply with local laws and regulations.

   **Note**
   Always ensure you are complying with all local laws and regulations when using services like the OpenAI API. If there are any changes in policy or new restrictions after this guide is written, please check the latest OpenAI policy or news for updates.

  **7. Create Your Own Interface**
  
   To make your own interface for interacting with the ChatGPT API, you'll need to create an application that can send HTTP requests to the API, handle the response, and present it in a user-friendly way. This can be done in many programming languages and frameworks, and the specific steps will depend on the tools you're using.

Here's a simplified example of how you might create a simple text-based interface in Python using the requests library:
```python
import requests
import json

# Set up the API call variables
url = "https://api.openai.com/v1/engines/davinci-codex/completions"
headers = {
    "Content-Type": "application/json",
    "Authorization": "Bearer YOUR_OPENAI_API_KEY"
}
data = {
    "prompt": "Translate the following English text to French: '{}'",
    "max_tokens": 60
}

# Create a loop that allows the user to enter text and get a response from the API
while True:
    # Get the user's input
    text = input("Enter some text to translate, or 'quit' to quit: ")

    # If the user wants to quit, break the loop
    if text.lower() == 'quit':
        break

    # Otherwise, send the text to the OpenAI API
    data['prompt'] = data['prompt'].format(text)
    response = requests.post(url, headers=headers, data=json.dumps(data))

    # Print the result
    if response.status_code == 200:
        result = response.json()
        print('Translation:', result['choices'][0]['text'])
    else:
        print('Error:', response.status_code, response.text)
```

## That's It!!!! Well Done!! You've Successfully Set Up Your Own Open AI API
Yes, you still have to pay Sam Altman, but now you've unleashed the possibility to customize this beast to your needs!

## Next Steps
To learn more about building your own interface, please refer to [Open AI's official tutorial](https://platform.openai.com/docs/quickstart/build-your-application)
Yes, I could've covered it here, but you've accomplished a lot today, take a well-deserved break!


