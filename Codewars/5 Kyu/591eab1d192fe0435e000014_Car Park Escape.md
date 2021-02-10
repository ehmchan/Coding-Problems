## [Car Park Escape](https://www.codewars.com/kata/591eab1d192fe0435e000014/)

# Problem
Introduction
A multi-storey car park (also called a parking garage, parking structure, parking ramp, parkade, parking building, parking deck or indoor parking) is a building designed for car parking and where there are a number of floors or levels on which parking takes place. It is essentially an indoor, stacked car park. Parking structures may be heated if they are enclosed.

Design of parking structures can add considerable cost for planning new developments, and can be mandated by cities or states in new building parking requirements. Some cities such as London have abolished previously enacted minimum parking requirements (Source Wikipedia)

Task
Your task is to escape from the carpark using only the staircases provided to reach the exit. You may not jump over the edge of the levels (you’re not Superman!) and the exit is always on the far right of the ground floor.
Rules
1. You are passed the carpark data as an argument into the function.

2. Free carparking spaces are represented by a 0

3. Staircases are represented by a 1

4. Your parking place (start position) is represented by a 2

5. The exit is always the far right element of the ground floor.

6. You must use the staircases to go down a level.

7. You will never start on a staircase.

8. The start level may be any level of the car park.

9. Each floor will have only one staircase apart from the ground floor which will not have any staircases.
Returns
Return an array of the quickest route out of the carpark

R1 = Move Right one parking space.

L1 = Move Left one parking space.

D1 = Move Down one level.
Example
Initialise
carpark = [[1, 0, 0, 0, 2],
           [0, 0, 0, 0, 0]]
Working Out
- You start in the most far right position on level 1
- You have to move Left 4 places to reach the staircase => "L4"
- You then go down one flight of stairs => "D1"
- To escape you have to move Right 4 places => "R4"
Result
result = ["L4", "D1", "R4"]

# Solution
```Python
def escape(carpark):
    start = 2
    stair = 1
    positions = []
    direction_vals = []
    temp_result = []
    result = []
    
    # determine positions for start, stair and exit
    for count, sublevel in enumerate(carpark):
        if start in sublevel:
            start_pos = [carpark.index(sublevel), sublevel.index(start)]
            positions.append(start_pos)
        if stair in sublevel:
            stair_pos = [count, sublevel.index(1)]
            positions.append(stair_pos)

    exit = [len(carpark) - 1, len(sublevel) - 1]
    positions.append(exit)
    
    # remove all positions on any floors above/prior to start position
    actual_positions = positions[positions.index(start_pos):]
    
    # check if start and exit are on same position
    if start_pos == exit:
        return []
    else:
        # subtract adjacent positions to determine direction values
        for pos_item in range(len(actual_positions) - 1):
            dir = [(actual_positions[pos_item][0] - actual_positions[pos_item + 1][0]),
                   (actual_positions[pos_item][1] - actual_positions[pos_item + 1][1])]
            direction_vals.append(dir)
    
        # with value of direction, determine letter (L, R, D)
        for item in direction_vals:
            # check left or right
            if item[0] < 0:
                temp_result.append("D1")
            if item[1] > 0:
                temp_result.append(f"L{item[1]}")
            elif item[1] < 0:
                temp_result.append(f"R{item[1] * -1}")
    
        # check for multiple D1 in a row and combine them into final result
        count = 1
        for pos in range(len(temp_result)):  
            if temp_result[pos] != "D1":
                result.append(temp_result[pos])
            elif pos != len(temp_result) - 1:
                if temp_result[pos] == temp_result[pos + 1]:
                    count += 1
                else:
                    result.append(f"D{count}")
                    count = 1
            else:
                result.append(f"D{count}")
                count = 1
        
        return result
```
