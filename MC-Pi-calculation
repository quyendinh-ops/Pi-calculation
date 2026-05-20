#!/bin/bash

# Set the number of iterations. Use the first argument passed to the script, or default to 50000.
ITERATIONS=${1:-50000}
INSIDE_CIRCLE=0

# Bash's built-in $RANDOM generates an integer between 0 and 32767.
# We will treat 32767 as our radius (r). 
# Therefore, r^2 = 32767 * 32767 = 1073676289.
R_SQUARED=1073676289

echo "Starting Monte Carlo simulation to estimate Pi..."
echo "Running $ITERATIONS iterations. Please wait..."

# Loop for the specified number of iterations
for (( i=1; i<=ITERATIONS; i++ )); do
    # Get random X and Y coordinates (between 0 and 32767)
    X=$RANDOM
    Y=$RANDOM

    # Calculate distance squared from origin (X^2 + Y^2)
    (( DIST_SQUARED = X*X + Y*Y ))

    # Check if the point is inside the circle sector
    if (( DIST_SQUARED <= R_SQUARED )); then
        (( INSIDE_CIRCLE++ ))
    fi
done

# Calculate Pi = 4 * (Inside / Total)
# Since bash can't do decimals, we pipe the variables to 'awk' to do the final floating-point division.
PI_EST=$(awk -v inside=$INSIDE_CIRCLE -v total=$ITERATIONS 'BEGIN { printf "%.5f", 4 * (inside / total) }')

echo "-----------------------------------"
echo "Total Points:    $ITERATIONS"
echo "Points Inside:   $INSIDE_CIRCLE"
echo "Estimated Pi:    $PI_EST"
echo "Actual Pi:       3.14159..."
echo "-----------------------------------"
