📦 Required Installations

Install these libraries first:

pip install requests
pip install behave
(If you want, you can also create a requirements.txt later.)

📂 Project Structure

api-bdd-framework/
├── features/
│   ├── steps/
│   │   └── api_steps.py      # 🛠️ Step definitions (calls API, validates responses)
│   ├── environment.py         # ⚙️ (Optional) Hooks like before/after scenario
│   └── api.feature            # 📄 BDD Feature file (Scenarios)
├── utilities/
│   └── api_helpers.py         # 📚 Reusable helper functions (GET, POST, etc.)
├── reports/                   # 📈 Reports (optional later)
├── README.md                  # 📝 Project documentation
├── behave.ini                 # ⚙️ Behave configurations
└── requirements.txt           # 📦 List of dependencies
✍️ Example Files

1. requirements.txt
requests
behave
2. features/api.feature
Feature: API Testing

  Scenario: Verify GET request to the users endpoint
    Given I send a GET request to "https://reqres.in/api/users?page=2"
    Then the response status code should be 200
    And the response should contain "total"
3. features/steps/api_steps.py
import requests
from behave import given, when, then

@given('I send a GET request to "{url}"')
def step_impl(context, url):
    context.response = requests.get(url)

@then('the response status code should be {status_code:d}')
def step_impl(context, status_code):
    assert context.response.status_code == status_code, \
        f"Expected {status_code} but got {context.response.status_code}"

@then('the response should contain "{key}"')
def step_impl(context, key):
    response_json = context.response.json()
    assert key in response_json, f"Key '{key}' not found in response"
4. utilities/api_helpers.py
(Optional later if you want to abstract request logic)

import requests

def get(url):
    return requests.get(url)

def post(url, payload):
    return requests.post(url, json=payload)
5. (Optional) features/environment.py
def before_scenario(context, scenario):
    print(f"\n🚀 Starting Scenario: {scenario.name}")

def after_scenario(context, scenario):
    print(f"✅ Finished Scenario: {scenario.name}\n")
6. behave.ini (Configuration file)
[behave]
default_tags=~@skip
format=pretty
🧪 Running the Tests

Simply run:

behave
You'll see the feature and steps execute beautifully in BDD style ✅.

🌟 Quick Summary


Tool	Purpose
requests	Send HTTP requests (GET, POST...)
behave	Write BDD-style feature files and scenarios