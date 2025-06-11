# numpy-calculator
# Output = file [Output_numpy (2).txt]

import numpy as np

def calculate(data_list):
    """
    Calculates mean, variance, standard deviation, max, min, and sum
    of rows, columns, and flattened elements for a 3x3 matrix.

    Args:
        data_list (list): A list containing exactly 9 digits.

    Returns:
        dict: A dictionary containing the calculated statistics.
              The format is:
              {
                'mean': [axis0_means, axis1_means, flattened_mean],
                'variance': [axis0_variances, axis1_variances, flattened_variance],
                'standard deviation': [axis0_stds, axis1_stds, flattened_std],
                'max': [axis0_maxs, axis1_maxs, flattened_max],
                'min': [axis0_mins, axis1_mins, flattened_min],
                'sum': [axis0_sums, axis1_sums, flattened_sum]
              }
              All values in the returned dictionary will be lists (for axis calculations)
              or single numbers (for flattened calculations), not NumPy arrays.

    Raises:
        ValueError: If the input list does not contain exactly nine numbers.
    """
    # 1. Check if the list contains exactly 9 elements
    if len(data_list) != 9:
        raise ValueError("List must contain nine numbers.")

    # 2. Convert the list into a 3x3 NumPy array
    # The reshape method ensures the list is converted into a 3x3 matrix
    matrix = np.array(data_list).reshape(3, 3)

    # 3. Perform calculations for mean, variance, standard deviation, max, min, and sum
    # Calculations are done along axis 0 (columns), axis 1 (rows),
    # and for the flattened (entire) array.
    
    # Use .tolist() to convert NumPy array results into Python lists as required
    
    calculations = {
        'mean': [
            matrix.mean(axis=0).tolist(),  # Mean of columns
            matrix.mean(axis=1).tolist(),  # Mean of rows
            matrix.mean().tolist()         # Mean of flattened array (single number)
        ],
        'variance': [
            matrix.var(axis=0).tolist(),   # Variance of columns
            matrix.var(axis=1).tolist(),   # Variance of rows
            matrix.var().tolist()          # Variance of flattened array
        ],
        'standard deviation': [
            matrix.std(axis=0).tolist(),   # Standard deviation of columns
            matrix.std(axis=1).tolist(),   # Standard deviation of rows
            matrix.std().tolist()          # Standard deviation of flattened array
        ],
        'max': [
            matrix.max(axis=0).tolist(),   # Max of columns
            matrix.max(axis=1).tolist(),   # Max of rows
            matrix.max().tolist()          # Max of flattened array
        ],
        'min': [
            matrix.min(axis=0).tolist(),   # Min of columns
            matrix.min(axis=1).tolist(),   # Min of rows
            matrix.min().tolist()          # Min of flattened array
        ],
        'sum': [
            matrix.sum(axis=0).tolist(),   # Sum of columns
            matrix.sum(axis=1).tolist(),   # Sum of rows
            matrix.sum().tolist()          # Sum of flattened array
        ]
    }

    return calculations

# --- Example Usage (for testing purposes, typically in main.py) ---
# You can put the code below into a separate main.py file for testing
# or run it directly if this is your only file for quick checks.

if __name__ == "__main__":
    # Example 1: Test with valid input
    print("--- Testing with valid input ---")
    try:
        valid_data = [0,1,2,3,4,5,6,7,8]
        result_valid = calculate(valid_data)
        print(f"Input: {valid_data}")
        # Using json.dumps for pretty printing the dictionary
        import json
        print("Output:\n", json.dumps(result_valid, indent=2))
    except ValueError as e:
        print(f"Error: {e}")

    print("\n" + "=" * 50 + "\n")

    # Example 2: Test with invalid input (less than 9 numbers)
    print("--- Testing with invalid input (less than 9 numbers) ---")
    try:
        invalid_data_short = [1,2,3,4,5]
        result_invalid_short = calculate(invalid_data_short)
        print(f"Input: {invalid_data_short}")
        print("Output:\n", result_invalid_short) # This line won't be reached
    except ValueError as e:
        print(f"Error: {e}")

    print("\n" + "=" * 50 + "\n")

    # Example 3: Test with another valid input from FreeCodeCamp's tests
    print("--- Testing with another valid input ---")
    try:
        another_valid_data = [2,6,2,8,4,0,1,5,7]
        result_another_valid = calculate(another_valid_data)
        print(f"Input: {another_valid_data}")
        import json
        print("Output:\n", json.dumps(result_another_valid, indent=2))
    except ValueError as e:
        print(f"Error: {e}")
