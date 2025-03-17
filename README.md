#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>

// Global strings to be used to randomly generate password components
std::string string_char = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ";
std::string string_num = "0123456789";
std::string string_special = "~!@#$%^&*()";

std::string toLower(std::string input)
{
    for (char& c : input) {
        c = std::tolower(c); // Convert each character to lowercase
    }
    return input;
}

// Function to get user input
void userInput(int &length, bool &use_special_chars, bool &use_numbers) {
    std::cout << "Enter the length of the password: ";
    std::cin >> length;

    std::string special_char_input;
    std::cout << "Include special characters? (yes/no): ";
    std::cin >> special_char_input;
    use_special_chars = (toLower(special_char_input) == "yes");

    std::string numbers_input;
    std::cout << "Include numbers? (yes/no): ";
    std::cin >> numbers_input;
    use_numbers = (toLower(numbers_input) == "yes");
}

// Function to generate the password
std::string generate_password(int length, bool use_special_chars, bool use_numbers) {
    // Ensure password length is valid
    if (length < 3) {
        throw std::invalid_argument("Password length must be at least 3.");
    }

    std::string password;
    std::srand(static_cast<unsigned int>(std::time(0))); // Seed random number generator

    // Step 1: First character must be an alphabet
    password += string_char[std::rand() % string_char.length()];

    // Step 2: Generate the remaining characters (length - 2)
    for (int i = 1; i < length - 2; ++i) {
        password += string_char[std::rand() % string_char.length()];
    }

    // Step 3: Add a number or alphabet based on 'use_numbers'
    if (use_numbers) {
        password += string_num[std::rand() % string_num.length()];
    } else {
        password += string_char[std::rand() % string_char.length()];
    }

    // Step 4: Add a special character or alphabet based on 'use_special_chars'
    if (use_special_chars) {
        password += string_special[std::rand() % string_special.length()];
    } else {
        password += string_char[std::rand() % string_char.length()];
    }

    return password;
}

int main() {
    int length;
    bool use_special_chars;
    bool use_numbers;

    // Get user input
    userInput(length, use_special_chars, use_numbers);

    try {
        // Generate password
        std::string generated_password = generate_password(length, use_special_chars, use_numbers);

        // Output the generated password
        std::cout << "\nGenerated Password: " << generated_password << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Error: " << e.what() << std::endl;
    }

    return 0;
}
