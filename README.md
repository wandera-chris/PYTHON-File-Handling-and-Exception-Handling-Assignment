# PYTHON-File-Handling-and-Exception-Handling-Assignment
# File Read & Write Challenge 🖋️: Create a program that reads a file and writes a modified version to a new file

def modify_and_write_file(input_filename, output_filename, modification_function):
    """
    Reads a file, modifies its contents using a given function, and writes the modified content to a new file.

    Args:
        input_filename: The name of the input file.
        output_filename: The name of the output file.
        modification_function: A function that takes a string (a line from the input file) and returns the modified string.
    """
    try:
        with open(input_filename, 'r') as infile, open(output_filename, 'w') as outfile:
            for line in infile:
                modified_line = modification_function(line)
                outfile.write(modified_line)
        print(f"File '{input_filename}' modified and written to '{output_filename}' successfully.")

    except FileNotFoundError:
        print(f"Error: Input file '{input_filename}' not found.")
    except Exception as e:
        print(f"An error occurred: {e}")

# Example modification function (e.g., convert to uppercase)
def uppercase_modification(line):
    return line.upper()

# Example usage
input_file = "input.txt"  # Replace with your input file name
output_file = "output.txt" # Replace with your output file name

# Create a dummy input file for testing purposes.
with open(input_file, 'w') as f:
    f.write("This is a line of text.\n")
    f.write("Another line for testing.\n")
    f.write("python is fun\n")

modify_and_write_file(input_file, output_file, uppercase_modification)

# Example modification function (e.g., add line numbers)
def add_line_numbers(line, line_number=[1]): #using a list to maintain state across function calls.
    modified_line = f"{line_number[0]}: {line}"
    line_number[0] += 1
    return modified_line

output_file_numbered = "output_numbered.txt"
modify_and_write_file(input_file, output_file_numbered, add_line_numbers)

# FUNCTION EXPLANATION

Flexibility with modification_function:
The modify_and_write_file function now takes a modification_function as an argument. This allows you to apply any desired modification to the file's contents without changing the core file reading/writing logic.
The example shows how to create two different modification functions: uppercase_modification and add_line_numbers.
Clearer Error Handling:
The try...except block now catches FileNotFoundError specifically, providing a more informative error message.
Also catches general exceptions.
Example Usage and Dummy Input:
The code includes an example of how to use the modify_and_write_file function.
Creates a dummy input file for testing.
Line Number Example:
Demonstrates how to maintain state within a modification function using a list, in order to add line numbers.
Clearer comments and docstrings.
Handles newlines: The code now correctly preserves newline characters, ensuring that the output file has the same line structure as the input file.
More robust function design: The code is more modular and reusable
