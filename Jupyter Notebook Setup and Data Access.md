### Jupyter Notebook Setup and Data Access

In this notebook, we will cover how to properly set up a Jupyter notebook within a virtual environment, read configuration settings from a `config.ini` file using the `configparser` module, and access data files stored in the `data` directory using relative paths.

---

### 1. Setting Up Jupyter Notebook in a Virtual Environment

To ensure that your Jupyter notebook runs within the correct virtual environment, follow these steps:

1. **Activate the Virtual Environment:**

   ```sh
   source env/bin/activate
   ```

2. **Install Jupyter in the Virtual Environment:**

   ```sh
   pip install jupyter
   ```

3. **Install `ipykernel` to Add the Virtual Environment to Jupyter:**

   ```sh
   pip install ipykernel
   ```

4. **Add the Virtual Environment to Jupyter:**

   ```sh
   python -m ipykernel install --user --name=env --display-name "Python (env)"
   ```

5. **Start Jupyter Notebook:**

   ```sh
   jupyter notebook
   ```

6. **Select the Correct Kernel:**

   - When you open a notebook, ensure you select the kernel associated with your virtual environment:
     - Go to `Kernel > Change kernel` and select `Python (env)`.

---

### 2. Configuration Setup

We will read configuration settings from a `config.ini` file. This allows us to manage our application settings in a centralized and organized manner.

```python
import configparser
import os
import pandas as pd

# Create a ConfigParser object
config = configparser.ConfigParser()

# Define the path to the config file (modify the path according to your setup)
config_file_path = os.path.join('.', 'config.ini')

# Read the config file
config.read(config_file_path)

# Access the settings
db_host = config['database']['host']
db_port = config['database']['port']
db_user = config['database']['username']
db_password = config['database']['password']
db_name = config['database']['database']

api_key = config['api']['key']

data_dir = config['paths']['data_dir']
log_dir = config['paths']['log_dir']
output_dir = config['paths']['output_dir']

debug_mode = config['environment'].getboolean('debug_mode')
log_level = config['environment']['log_level']

# Print the values to verify
print(f"Database Host: {db_host}")
print(f"API Key: {api_key}")
print(f"Data Directory: {data_dir}")

# List all files in the data folder
data_files = os.listdir(data_dir)
print("Data files:", data_files)

# Example: Read a CSV file from the data folder
csv_file_path = os.path.join(data_dir, 'your_data_file.csv')
data = pd.read_csv(csv_file_path)

# Display the first few rows of the dataframe
data.head()
```

### Explanation

1. **Define the Relative Path to the Config File:**
   - `config_file_path = os.path.join('.', 'config.ini')`
   - This assumes your `config.ini` file is in the root directory of your repository.

2. **Access the Data Directory:**
   - `data_dir = config['paths']['data_dir']` retrieves the path to the data directory from the config file.
   - Use `os.listdir(data_dir)` to list files in the data directory.

3. **Read a CSV File:**
   - Construct the full path to the CSV file using `os.path.join(data_dir, 'your_data_file.csv')`.
   - Read the CSV file into a pandas DataFrame with `pd.read_csv(csv_file_path)`.

### Summary

1. **Set up Jupyter Notebook:**
   - Activate your virtual environment.
   - Install Jupyter and `ipykernel`.
   - Add the virtual environment to Jupyter and start the notebook.
   - Select the correct kernel.

2. **Configuration Setup:**
   - Use `configparser` to read configuration settings from `config.ini`.

3. **Data Access:**
   - Access and list files in the `data` directory.
   - Read and display data from a CSV file using pandas.
