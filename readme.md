# Project Name : Tinder Scraper

## Overview
This project consists of several Python scripts designed to interact with the Tinder API for various purposes such as scraping profiles, refreshing tokens, and filtering data. The main components of the project are `scraper.py`, `refresh_token.py`, `api_pb2.py`, and `filter.py`.

## Files and Their Functions

### Non-Python Files

#### .env
This file contains environment variables used by the scripts, such as API keys, credentials, and configuration settings. It's used to store sensitive information that shouldn't be hardcoded in the scripts.

#### api.proto
This is a Protocol Buffer definition file that defines the structure of messages used for communication with the Tinder API. It's used to generate the `api_pb2.py` file.

#### failed_tokens.csv
This CSV file stores information about tokens that failed to refresh. It helps track problematic accounts that may need manual intervention.

#### input.csv
This is the main input file containing account data such as refresh tokens, proxies, and other account-specific information needed for the scraper to function.

#### requirements.txt
This file lists all the Python package dependencies required to run the project. It's used with pip to install all necessary packages.

### Python Scripts

#### scraper.py
This script is responsible for scraping profiles from the Tinder API. It performs the following tasks:
- Fetches profile data from the Tinder API.
- Parses the profile data to extract relevant information.
- Saves the extracted data to log files and bio files.
- Handles rate limiting and token expiration.
- Uses OpenAI's API to parse Snapchat handles from bios.

##### Key Functions:
- `create_session()`: Creates a session with retry logic to handle transient errors.
- `getProfileList(account, timeout)`: Fetches the profile list from the Tinder API using the provided account details and handles rate limiting and token expiration.
- `parse_user(profile)`: Parses user data from the profile, including name, age, ID, s_number, and bio.
- `parse_snap(bio, timeout)`: Uses OpenAI's API to parse Snapchat handles from bios. Returns the handle if found, otherwise returns '-1'.
- `pass_id(id, snumber, headers, proxies, session, timeout)`: Sends a pass request to the Tinder API for the given user ID and s_number.
- `worker_wrapper(args)`: Wrapper function for multiprocessing to handle tasks and worker functions.
- `process_accounts_with_dynamic_pool(account_list, worker_function, timeout_per_task)`: Processes accounts using a dynamic pool of workers, handling tasks in parallel to improve performance.
- `main()`: Main function that orchestrates the scraping process, including setting up directories, parsing input data, and processing accounts.

#### refresh_token.py
This script handles the refreshing of Tinder API tokens. It performs the following tasks:
- Reads account data from an input CSV file.
- Sends requests to the Tinder API to refresh tokens.
- Handles captcha challenges using the ImageTyperz API.
- Writes the updated tokens back to the input CSV file.

##### Key Functions:
- `solve_captcha(data, proxy)`: Solves captcha challenges using the ImageTyperz API and returns the response.
- `handle_captcha(account, ban_appeal)`: Handles captcha challenges for an account by solving the captcha and verifying the challenge.
- `encode(refresh_token)`: Encodes the refresh token into a protobuf message for the Tinder API request.
- `decode(bytes_received)`: Decodes the protobuf response from the Tinder API into a dictionary.
- `refresh_token(account)`: Sends a request to refresh the token for an account, handling captcha challenges and errors.
- `main()`: Main function that orchestrates the token refreshing process, including parsing input data, refreshing tokens, and writing updated tokens to the input CSV file.

#### api_pb2.py
This file contains the protocol buffer definitions for the Tinder API. It includes the following:
- Definitions for various request and response messages used by the Tinder API.
- Serialization and deserialization logic for protobuf messages to facilitate communication with the Tinder API.

#### filter.py
This script filters and processes text files containing bios. It performs the following tasks:
- Reads text files from the `bios` directory.
- Extracts Snapchat handles from the bios.
- Prints the extracted handles.

##### Key Functions:
- The script does not contain any functions but uses a for loop to process files and extract data.
- It reads each line from the text files, splits the line by commas, and checks for the presence of a Snapchat handle.
- If a valid Snapchat handle is found, it is added to the `leads` list and printed.

## How to run it

### Run in PyCharm (Step by Step)
1. **Open PyCharm** and select "Open" from the welcome screen.
2. **Navigate to the project directory** and select it, then click "OK".
3. **Set up Python Interpreter**:
   - Go to File > Settings (or PyCharm > Preferences on macOS).
   - Navigate to Project > Python Interpreter.
   - Click on the gear icon and select "Add".
   - Choose "Virtual Environment" and select the base interpreter.
   - Make sure "Inherit global site-packages" is checked.
   - Click "OK" to create the virtual environment.

4. **Install Dependencies in PyCharm**:
   - Open the Terminal tool window in PyCharm (View > Tool Windows > Terminal).
   - Run `pip install -r requirements.txt` to install all required packages.
   
   Alternatively, you can install packages through PyCharm's interface:
   - Go to File > Settings (or PyCharm > Preferences on macOS).
   - Navigate to Project > Python Interpreter.
   - Click the "+" button at the bottom of the packages list.
   - Search for each package listed in requirements.txt and install them.
   - For multiple packages, you can select them all at once before clicking "Install Package".

5. **Configure Environment Variables**:
   - Right-click on the script you want to run (e.g., `scraper.py`).
   - Select "Modify Run Configuration".
   - In the "Environment variables" field, add any necessary variables or point to your `.env` file.
   - Click "Apply" and "OK".

6. **Run the Script**:
   - Right-click on `scraper.py` in the Project Explorer.
   - Select "Run 'scraper'" to execute the script.
   - Alternatively, open `scraper.py` and click the green "Run" button in the top-right corner of the editor.

7. **View Output**:
   - The script's output will appear in the "Run" tool window at the bottom of the PyCharm interface.
   - Check the "bios" and "logs" directories for generated files.

### Run from Command Line
If you prefer to run from the command line instead of PyCharm:

1. **Install required packages**:
   ```
   pip install -r requirements.txt
   ```

2. **Run the script**:
   ```
   python scraper.py
   ```
