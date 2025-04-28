# API Automation Frame work

# Required Installations

Before you begin, ensure you have the following tools installed:

pip install requests
pip install behave
(If you want, you can also create a requirements.txt later.)

# BDD Format
**1.Feature: API Testing

  **Scenario: Verify GET request to the users endpoint
   **Given I send a GET request to "https://reqres.in/api/users?page=2"
    **Then the response status code should be 200
    **And the response should contain "total"
  
**2. features/steps/api_steps.py
**import requests
**from behave import given, when, then

**@given('I send a GET request to "{url}"')
**def step_impl(context, url):
    **context.response = requests.get(url)

**@then('the response status code should be {status_code:d}')
**def step_impl(context, status_code):
    **assert context.response.status_code == status_code, \
        **f"Expected {status_code} but got {context.response.status_code}"

**@then('the response should contain "{key}"')
**def step_impl(context, key):
    **response_json = context.response.json()
    **assert key in response_json, f"Key '{key}' not found in response"


## Running the Tests

**Simply run:

**behave
**You'll see the feature and steps execute beautifully in BDD style ✅.

