import string

MIN_LENGTH = 8
SPECIAL_CHARACTERS = string.punctuation  # e.g. !@#$%^&*()_+-=...


def validate_password(password: str) -> list:
    """
    Validates a password against the rules above.
    Returns a list of validation messages, one per rule.
    An empty list means the password passed every rule (not possible here,
    since we always return a message per rule — see below for a pass/fail
    version).
    """
    errors = []

    # Rule 1: minimum length
    if len(password) < MIN_LENGTH:
        errors.append(f"Password must be at least {MIN_LENGTH} characters long.")

    # Rule 2: uppercase letter
    has_upper = False
    for ch in password:
        if ch.isupper():
            has_upper = True
            break
    if not has_upper:
        errors.append("Password must contain at least one uppercase letter.")

    # Rule 3: lowercase letter
    has_lower = False
    for ch in password:
        if ch.islower():
            has_lower = True
            break
    if not has_lower:
        errors.append("Password must contain at least one lowercase letter.")

    # Rule 4: number
    has_digit = False
    for ch in password:
        if ch.isdigit():
            has_digit = True
            break
    if not has_digit:
        errors.append("Password must contain at least one number.")

    # Rule 5: special character
    has_special = False
    for ch in password:
        if ch in SPECIAL_CHARACTERS:
            has_special = True
            break
    if not has_special:
        errors.append("Password must contain at least one special character.")

    return errors


def is_valid(password: str) -> bool:
    """Returns True if the password satisfies all rules."""
    return len(validate_password(password)) == 0


def check_and_report(password: str) -> None:
    """
    Prints a clear validation report for a password.
    Does NOT print the actual password — only its validation status.
    """
    errors = validate_password(password)
    if not errors:
        print("✅ Password is valid. It meets all requirements.")
    else:
        print("❌ Password is invalid. Issues found:")
        for msg in errors:
            print(f"   - {msg}")


def main():
    print("=== Password Validator ===")
    print(f"Rules: min {MIN_LENGTH} chars, 1 uppercase, 1 lowercase, "
          "1 number, 1 special character.\n")

    while True:
        password = input("Enter a password to check (or 'q' to quit): ")
        if password.lower() == "q":
            print("Goodbye!")
            break
        check_and_report(password)
        print()


if __name__ == "__main__":
    main()
