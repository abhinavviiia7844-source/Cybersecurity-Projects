# Cybersecurity-Projects

"""
Password Strength Checker
--------------------------
A command-line tool that evaluates the strength of a password based on:
- Length
- Use of uppercase and lowercase letters
- Use of numbers
- Use of special characters
- Whether it appears in a list of common/weak passwords


"""

import re
import getpass

# A small sample list of extremely common passwords.

COMMON_PASSWORDS = {
    "123456", "password", "123456789", "12345678", "12345",
    "qwerty", "abc123", "password1", "111111", "123123",
    "letmein", "iloveyou", "admin", "welcome", "monkey"
}


def check_password_strength(password: str) -> dict:
    """
    Analyze a password and return a dictionary with:
    - score (0-6)
    - strength label
    - list of specific suggestions to improve it
    """
    suggestions = []
    score = 0

    # 1. Length checks
    if len(password) >= 8:
        score += 1
    else:
        suggestions.append("Use at least 8 characters (12+ is even better).")

    if len(password) >= 12:
        score += 1

    # 2. Character variety checks
    if re.search(r"[a-z]", password):
        score += 1
    else:
        suggestions.append("Add at least one lowercase letter.")

    if re.search(r"[A-Z]", password):
        score += 1
    else:
        suggestions.append("Add at least one uppercase letter.")

    if re.search(r"[0-9]", password):
        score += 1
    else:
        suggestions.append("Add at least one number.")

    if re.search(r"[!@#$%^&*(),.?\":{}|<>_\-+=]", password):
        score += 1
    else:
        suggestions.append("Add at least one special character (e.g. ! @ # $ %).")

    # 3. Common password check (this overrides everything — an attacker
    # tries these first, so a "complex-looking" but common password is
    # still weak in practice)
    if password.lower() in COMMON_PASSWORDS:
        score = 0
        suggestions = ["This password is one of the most commonly used passwords "
                        "in the world and would be guessed almost instantly. Choose something unique."]

    # 4. Map score to a human-readable strength label
    if score <= 1:
        label = "Very Weak"
    elif score == 2 or score == 3:
        label = "Weak"
    elif score == 4:
        label = "Moderate"
    elif score == 5:
        label = "Strong"
    else:
        label = "Very Strong"

    return {
        "score": score,
        "max_score": 6,
        "label": label,
        "suggestions": suggestions
    }


def main():
    print("=== Password Strength Checker ===")
    print("(Your input will be hidden as you type)\n")

    # getpass hides the password as it's typed, just like a real login prompt
    password = getpass.getpass("Enter a password to check: ")

    result = check_password_strength(password)

    print(f"\nStrength: {result['label']}  ({result['score']}/{result['max_score']})")

    if result["suggestions"]:
        print("\nSuggestions to improve:")
        for tip in result["suggestions"]:
            print(f"  - {tip}")
    else:
        print("\nGreat job! No major weaknesses detected.")


if __name__ == "__main__":
    main()
