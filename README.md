# Rental Management System

This is a FastAPI application designed to manage rental information and automate billing processes using Google Sheets. The application includes endpoints for creating users, updating billing information, generating monthly billing lines, and sending email reminders.

## Features

- Create and manage tenant information
- Automatically calculate and update rent, utilities, gas, and other charges
- Generate monthly billing records
- Send email reminders for rent payments
- Integrate with Google Sheets for data storage
- Securely manage credentials using Google Cloud Secret Manager

## Requirements

- Python 3.7+
- FastAPI
- gspread
- google-auth
- google-cloud-secret-manager
- smtplib

## Setup

1. **Clone the repository**:
    ```bash
    git clone https://github.com/muhtasim7/Rent-Control
    cd Rent-Control
    ```

2. **Create and activate a virtual environment**:
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3. **Install dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

4. **Google Cloud Setup**:
    - Create a Google Cloud project and enable the Secret Manager API.
    - Store your service account JSON file and SMTP password in Google Cloud Secret Manager.
    - Ensure the service account has the necessary permissions for accessing Google Sheets and Secret Manager.

5. **Environment Variables**:
    - Set up environment variables for Google Cloud credentials.
    ```bash
    export GOOGLE_APPLICATION_CREDENTIALS="path/to/your/service-account-file.json"
    ```

## Usage

1. **Run the FastAPI server**:
    ```bash
    uvicorn main:app --reload
    ```

2. **Access the API documentation**:
    Open your web browser and go to `http://127.0.0.1:8000/docs` to see the interactive API documentation.

## Endpoints

- **Create User**: `POST /user/`
    - Parameters: `name`, `email`, `age`, `phone_number`, `id_number`, `staying`, `current_address`, `previous_address`, `start_date`, `rent`, `Utilities`, `GAS`, `Other`, `paid_amount`
    - Description: Adds a new user and their initial rent record to Google Sheets. Creates a new worksheet for the user with headers and initial billing information.

- **Update Billing**: `PUT /update_billing/`
    - Parameters: `name`, `rent`, `utilities`, `gas`, `other`, `paid`, `staying`
    - Description: Updates billing information for a specific user by adding a new row to their worksheet with the updated rent, utilities, gas, other charges, and payment information.

- **Create Billing Lines**: `POST /create-billing-lines/`
    - Description: Creates billing lines for each user based on the most recent data, summing up their rents, utilities, gas, other charges, and payments.

- **New Month**: `POST /new-month/`
    - Description: Adds a new row for each user in their worksheet to indicate the start of a new billing month.

- **Delete User**: `DELETE /user/`
    - Parameters: `name`
    - Description: Deletes a user from the main sheet and their corresponding worksheet.

- **Send Email**: `POST /send-email/`
    - Description: Sends rent reminder emails to tenants.

- **Send Email to Landlord**: `POST /send-email-Manzur/`
    - Description: Sends a summary email to the landlord for each tenant.

## License

This project is licensed under the MIT License.

## Contributing

Contributions are welcome! Please fork the repository and create a pull request with your changes.

## Contact

If you have any questions or need further assistance, feel free to contact me at [muhtasimswarnil@gmail.com](mailto:muhtasimswarnil@gmail.com).

---

[GitHub Repository](https://github.com/muhtasim7/Rent-Control)
