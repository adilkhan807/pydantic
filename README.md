# Pydantic Data Validation and Modeling

A collection of practical Python examples demonstrating how to use **Pydantic** to validate, structure, and serialize data. The examples use a patient record to explore typed fields, field constraints, custom validation, nested models, model-level validation, serialization, and computed fields.

This is a learning project designed to build a practical understanding of Pydantic and how it helps ensure that application data follows expected rules.

## Project Overview

The project covers the following Pydantic features:

- Basic data models using `BaseModel`
- Field types and constraints using `Field` and `Annotated`
- Email and URL validation with `EmailStr` and `AnyUrl`
- Custom field validation with `@field_validator`
- Model-level validation with `@model_validator`
- Nested models for structured data
- Model serialization with `model_dump()`
- Computed fields for derived values such as BMI

## Project Structure

```text
.
├── computed_fields.py       # Calculates BMI using a computed field
├── serialization.py         # Converts model data into a dictionary
├── nested_models.py         # Demonstrates nested Address and Patient models
├── model_validation.ipynb   # Demonstrates model-level validation
├── field_validator.py       # Demonstrates custom field validation
├── pyd_test.py              # Demonstrates Pydantic types and field constraints
└── README.md
```

## Requirements

- Python 3.9 or newer
- Pydantic 2.x
- `email-validator` (needed for `EmailStr`)

Install the required package:

```bash
python -m pip install "pydantic[email]"
```

## Getting Started

1. Clone or download the repository.
2. Open a terminal in the project directory.
3. Install the dependency shown above.
4. Open `model_validation.ipynb` in Jupyter Notebook, JupyterLab, or Google Colab.
5. Run the Python examples individually after checking the notebook-export note below.

## Running the Examples

```bash
python pyd_test.py
python field_validator.py
python nested_models.py
python serialization.py
python computed_fields.py
```

Open the notebook separately in Jupyter or Google Colab:

```text
model_validation.ipynb
```

**Notebook-export note:** Some `.py` files contain installation commands such as `pip install ...` or `!pip install ...` that were copied from notebook cells. These commands are not valid Python statements in a regular script. Install the dependencies in the terminal using the command above, then remove or comment out those installation lines before running the affected `.py` files.

## File-by-File Explanation

### 1. `pyd_test.py` — Basic Model and Field Constraints

Defines a `Patient` model with fields for name, email, LinkedIn URL, age, weight, marital status, allergies, and contact details.

It demonstrates:

- `BaseModel` for defining structured data.
- `EmailStr` for email validation.
- `AnyUrl` for URL validation.
- `Field` for constraints such as string length and numeric ranges.
- `Annotated` for adding validation metadata to type hints.

### 2. `field_validator.py` — Custom Field Validation

Uses `@field_validator` to apply custom rules:

- Accepts email addresses only from the `hdfc.com` and `icici.com` domains.
- Converts patient names to uppercase.
- Checks that age is greater than 0 and less than 100.

### 3. `model_validation.ipynb` — Model-Level Validation

Demonstrates validation involving multiple fields with `@model_validator(mode='after')`.

The example requires an emergency contact when a patient's age is greater than 60. If the required contact is missing, validation raises a `ValueError`.

### 4. `nested_models.py` — Nested Models

Defines an `Address` model and uses it as a field inside the `Patient` model. This keeps address information structured as a model rather than leaving it as an unvalidated dictionary.

### 5. `serialization.py` — Model Serialization

Uses `model_dump(exclude_unset=True)` to convert a Pydantic model instance into a Python dictionary while excluding fields that were not explicitly set.

### 6. `computed_fields.py` — Computed Fields

Uses `@computed_field` and a property to calculate the patient's Body Mass Index (BMI):

```python
bmi = weight / (height ** 2)
```

The result is rounded to two decimal places and exposed through `patient.bmi`.

## Important Notes

- The examples use sample patient data for learning purposes.
- These scripts are demonstrations, not a production-ready healthcare application.
- Do not use real patient information or other sensitive personal data in test examples.
- Validation rules are specific to each example. For instance, `field_validator.py` intentionally allows only two email domains.
- Age constraints differ between files because the examples demonstrate different validation approaches.
- Some Python files were exported from notebooks and may need the notebook installation commands removed or commented out before they can run as regular scripts.

## Learning Outcomes

By working through this project, you can learn how to:

1. Create structured data models with Pydantic.
2. Validate email addresses, URLs, and common Python data types.
3. Apply built-in field constraints.
4. Create custom field and model-level validation rules.
5. Organize related data using nested models.
6. Serialize model instances into dictionaries.
7. Calculate derived values using computed fields.

## Possible Improvements

- Add automated tests using `pytest`.
- Move sample data into separate test fixtures.
- Add examples showing how to handle validation errors.
- Organize reusable models into a dedicated package.
- Add a small FastAPI application to demonstrate request validation.

## License

No license is currently specified. Add a license file if you plan to distribute or reuse this project publicly.
