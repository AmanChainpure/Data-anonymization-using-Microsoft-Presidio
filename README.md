# Presidio-Based Data Anonymization in LangChain

## Overview

This project demonstrates how to anonymize personally identifiable information (PII) using PresidioAnonymizer and PresidioReversibleAnonymizer from LangChain Experimental. 
It covers:
- Standard anonymization of names, phone numbers, emails, and repository numbers.
- Custom anonymization using regex-based detection and Faker-generated replacements.
- Reversible anonymization, allowing the retrieval of original data when needed.

## PresidioAnonymizer vs. PresidioReversibleAnonymizer
PresidioAnonymizer: Anonymization	Replaces PII with fake or randomized values	Replaces PII with consistent placeholders
PresidioReversibleAnonymizer: Customization	Can replace values with Faker-generated data (e.g., random names, numbers)	Uses structured placeholders instead of fake data

## Installation
Install the required dependencies:

pip install --upgrade langchain langchain-openai langchain-experimental presidio-analyzer presidio-anonymizer spacy Faker

## Usage Examples
### 1️⃣ Basic Anonymization (PresidioAnonymizer)

    from langchain_experimental.data_anonymizer import PresidioAnonymizer
    
    anonymizer = PresidioAnonymizer()
    
    text = "My name is John Doe, call me at 123-456-7890 and my email is johndoe@example.com."
    anonymized_text = anonymizer.anonymize(text)
    
    print(anonymized_text)
🔹 Expected Output:

    "My name is Jocelyn Koch, call me at 001-879-287-9536x00260 and my email is danielstrickland@example.org."
✅ Original data is replaced with fake, but non-reversible, values.

### 2️⃣ Reversible Anonymization (PresidioReversibleAnonymizer)

    from langchain_experimental.data_anonymizer import PresidioReversibleAnonymizer
    
    anonymizer = PresidioReversibleAnonymizer()
    
    text = "My name is John Doe, call me at 123-456-7890 and my email is johndoe@example.com."
    anonymized_text = anonymizer.anonymize(text)
    
    print(anonymized_text)
🔹 Expected Output:

    "My name is <PERSON>, call me at <PHONE_NUMBER> and my email is <EMAIL_ADDRESS>."
✅ Original data is hidden but can be restored later.

### Why Use This?

- ✔ Privacy Protection: Anonymizes sensitive data for compliance with GDPR, HIPAA, etc.
- ✔ Flexible Customization: Define custom patterns (e.g., repo numbers, account IDs) for masking.
- ✔ Reversible Anonymization: Restore data when required for authorized use cases.

### References:

- Data anonymization with Microsoft Presidio: http://python.langchain.com/v0.1/docs/guides/productionization/safety/presidio_data_anonymization/

