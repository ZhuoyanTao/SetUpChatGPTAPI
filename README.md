# SetUpChatGPTAPI
Guide on Using ChatGPT via API
Please always ensure that you are in compliance with local laws and regulations when setting up and using services like the OpenAI API.

# Setting Up OpenAI API on Mac in Mainland China

This guide will walk you through the process of setting up the OpenAI API on your Mac computer in mainland China.

## Requirements

- macOS (latest version recommended)
- Python 3.6 or newer
- pip (Python package installer)
- OpenAI API key
- A VPN service (depending on the internet restrictions)

## Steps

1. **Install Python and pip**

   If you haven't already installed Python and pip on your Mac, you can do so by following these [instructions](https://docs.python-guide.org/starting/install3/osx/).

2. **Install the OpenAI Python client**

   Open Terminal and run the following command:

   ```shell
   pip install openai
   ```

Get your OpenAI API key

You need to apply for an API key from OpenAI. Visit the OpenAI website and follow the steps to apply for access. If approved, you will receive an API key.

Setup your OpenAI API key

You should save your API key in your environment variables for easy access. In Terminal, run:

   ```shell
   echo "export OPENAI_API_KEY='your-api-key'" >> ~/.bash_profile
   source ~/.bash_profile
   ```

Replace your-api-key with your actual API key.

3.Verify the setup

You can verify the setup by running a simple script that uses the OpenAI API. Here's a basic example:

```python
import openai

openai.api_key = os.getenv("OPENAI_API_KEY")

response = openai.Completion.create(
  engine="text-davinci-002",
  prompt="Translate the following English text to French: '{}'",
  max_tokens=60
)

print(response.choices[0].text.strip())

```
