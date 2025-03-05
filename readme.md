# Project Name : Tinder Scrapper

## Overview
This project consists of several Python scripts designed to interact with the Tinder API for various purposes such as scraping profiles, refreshing tokens, and filtering data. The main components of the project are `scraper.py`, `refresh_token.py`, `api_pb2.py`, and `filter.py`.

## Files and Their Functions

### scraper.py
This script is responsible for scraping profiles from th# Project Name : Tinder Scraper

## Overview
This project consists of several Python scripts designed to interact with the Tinder API for various purposes such as scraping profiles, refreshing tokens, and filtering data. The main components of the project are `scraper.py`, `refresh_token.py`, `api_pb2.py`, and `filter.py`.

## Files and Their Functions

### scraper.py
This script is responsible for scraping profiles from the Tinder API. It performs the following tasks:
- Fetches profile data from the Tinder API.
- Parses the profile data to extract relevant information.
- Saves the extracted data to log files and bio files.
- Handles rate limiting and token expiration.
- Uses OpenAI's API to parse Snapchat handles from bios.

#### Key Functions:
- `create_session()`: Creates a session with retry logic to handle transient errors.
- `getProfileList(account, timeout)`: Fetches the profile list from the Tinder API using the provided account details and handles rate limiting and token expiration.
- `parse_user(profile)`: Parses user data from the profile, including name, age, ID, s_number, and bio.
- `parse_snap(bio, timeout)`: Uses OpenAI's API to parse Snapchat handles from bios. Returns the handle if found, otherwise returns '-1'.
- `pass_id(id, snumber, headers, proxies, session, timeout)`: Sends a pass request to the Tinder API for the given user ID and s_number.
- `worker_wrapper(args)`: Wrapper function for multiprocessing to handle tasks and worker functions.
- `process_accounts_with_dynamic_pool(account_list, worker_function, timeout_per_task)`: Processes accounts using a dynamic pool of workers, handling tasks in parallel to improve performance.
- `main()`: Main function that orchestrates the scraping process, including setting up directories, parsing input data, and processing accounts.

### refresh_token.py
This script handles the refreshing of Tinder API tokens. It performs the following tasks:
- Reads account data from an input CSV file.
- Sends requests to the Tinder API to refresh tokens.
- Handles captcha challenges using the ImageTyperz API.
- Writes the updated tokens back to the input CSV file.

#### Key Functions:
- `solve_captcha(data, proxy)`: Solves captcha challenges using the ImageTyperz API and returns the response.
- `handle_captcha(account, ban_appeal)`: Handles captcha challenges for an account by solving the captcha and verifying the challenge.
- `encode(refresh_token)`: Encodes the refresh token into a protobuf message for the Tinder API request.
- `decode(bytes_received)`: Decodes the protobuf response from the Tinder API into a dictionary.
- `refresh_token(account)`: Sends a request to refresh the token for an account, handling captcha challenges and errors.
- `main()`: Main function that orchestrates the token refreshing process, including parsing input data, refreshing tokens, and writing updated tokens to the input CSV file.

### api_pb2.py
This file contains the protocol buffer definitions for the Tinder API. It includes the following:
- Definitions for various request and response messages used by the Tinder API.
- Serialization and deserialization logic for protobuf messages to facilitate communication with the Tinder API.

### filter.py
This script filters and processes text files containing bios. It performs the following tasks:
- Reads text files from the `bios` directory.
- Extracts Snapchat handles from the bios.
- Prints the extracted handles.

#### Key Functions:
- The script does not contain any functions but uses a for loop to process files and extract data.
- It reads each line from the text files, splits the line by commas, and checks for the presence of a Snapchat handle.
- If a valid Snapchat handle is found, it is added to the `leads` list and printed.

## Installation Instructions
1. Clone the repository:
    e Tinder API. It performs the following tasks:
- Fetches profile data from the Tinder API.
- Parses the profile data to extract relevant information.
- Saves the extracted data to log files and bio files.
- Handles rate limiting and token expiration.
- Uses OpenAI's API to parse Snapchat handles from bios.

#### Key Functions:
- `create_session()`: Creates a session with retry logic.
- `getProfileList(account, timeout)`: Fetches the profile list from the Tinder API.
- `parse_user(profile)`: Parses user data from the profile.
- `parse_snap(bio, timeout)`: Uses OpenAI's API to parse Snapchat handles from bios.
- `pass_id(id, snumber, headers, proxies, session, timeout)`: Sends a pass request to the Tinder API.
- `worker_wrapper(args)`: Wrapper function for multiprocessing.
- `process_accounts_with_dynamic_pool(account_list, worker_function, timeout_per_task)`: Processes accounts using a dynamic pool of workers.
- `main()`: Main function that orchestrates the scraping process.

### refresh_token.py
This script handles the refreshing of Tinder API tokens. It performs the following tasks:
- Reads account data from an input CSV file.
- Sends requests to the Tinder API to refresh tokens.
- Handles captcha challenges using the ImageTyperz API.
- Writes the updated tokens back to the input CSV file.

#### Key Functions:
- `solve_captcha(data, proxy)`: Solves captcha challenges using the ImageTyperz API.
- `handle_captcha(account, ban_appeal)`: Handles captcha challenges for an account.
- `encode(refresh_token)`: Encodes the refresh token into a protobuf message.
- `decode(bytes_received)`: Decodes the protobuf response from the Tinder API.
- `refresh_token(account)`: Sends a request to refresh the token for an account.
- `main()`: Main function that orchestrates the token refreshing process.

### api_pb2.py
This file contains the protocol buffer definitions for the Tinder API. It includes the following:
- Definitions for various request and response messages.
- Serialization and deserialization logic for protobuf messages.

### filter.py
This script filters and processes text files containing bios. It performs the following tasks:
- Reads text files from the `bios` directory.
- Extracts Snapchat handles from the bios.
- Prints the extracted handles.

#### Key Functions:
- The script does not contain any functions but uses a for loop to process files and extract data.


## How to run it

### Install required packages
- open cmd or terminal and go to current folder and run following command to install necessary pacakges.
`pip install -r .\requirements.txt`

### Run the script
In the cmd or terminal run 
`python .\scraper.py`