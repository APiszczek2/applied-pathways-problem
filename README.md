import re
names_and_basetext = []
answer_values = []
types = []
file = open('appliedpathways_input_file.py', 'r')
file_text = file.read()
file.close()
#locating the names to populate what would be the Question Label Column
matches = re.finditer('#name:(.*?)#', file_text, re.DOTALL) 

for matchNum, match in enumerate(matches):
    matchNum = matchNum + 1
    
    for groupNum in range(0, len(match.groups())):
        groupNum = groupNum + 1
        names_and_basetext.append(match.group(groupNum))

#locating the 'Path1,2,3' for the Answer Values Column
matches1 = re.finditer('#answer_names:(.*?)#', file_text, re.DOTALL) 
for matchNum, match in enumerate(matches1):
    matchNum = matchNum + 1
    
    for groupNum in range(0, len(match.groups())):
        groupNum = groupNum + 1
        answer_values.append(match.group(groupNum))

#locating the 3 'true\n's for the Answer Values Column
matches2 = re.finditer('#additionaldata:result:(.*?)#', file_text, re.DOTALL) 

for matchNum, match in enumerate(matches2):
    matchNum = matchNum + 1
    
    for groupNum in range(0, len(match.groups())):
        groupNum = groupNum + 1
        answer_values.append(match.group(groupNum))

#locating the types for the Type column
matches3 = re.finditer('#type: (.*?)#', file_text, re.DOTALL) 
for matchNum, match in enumerate(matches3):
    matchNum = matchNum + 1
    
    for groupNum in range(0, len(match.groups())):
        groupNum = groupNum + 1
        types.append(match.group(groupNum))
        
import terminaltables as tt           
from terminaltables import AsciiTable

#I've never created a table before but this seemed like the easiest way. I was also looking
#at NumPy and PrettyTable.

table_data = [
        ['Question Label', 'Answer Values', 'Type'],
        [names_and_basetext[0], '\n',  types[0]],
        [names_and_basetext[1], '\n',  types[1]],
        [names_and_basetext[2], answer_values[0], types[2]],
        [names_and_basetext[3], answer_values[1], types[3]],
        [names_and_basetext[4], '\n', types[4]],
        [names_and_basetext[5], '\n', types[5]],
        [names_and_basetext[6], '\n', types[6]],
        [names_and_basetext[7], answer_values[2], types[7]],
        [names_and_basetext[8], '\n', types[8]],
        [names_and_basetext[9], '\n', types[9]],
        [names_and_basetext[10], '\n', types[10]],
        [names_and_basetext[11], answer_values[3], types[11]],
        [names_and_basetext[12], '\n', types[12]],
        [names_and_basetext[13], '\n', types[13]],
        [names_and_basetext[14], '\n', types[14]],
        [names_and_basetext[15], '\n', types[15]],
        [names_and_basetext[16], '\n', types[16]],     
        ]
#I believe populating the data table with a loop would've been the most
#efficient way, but I was running into some problems using a while loop
#so I opted for the pretty and less efficient table.

table = AsciiTable(table_data)
print (table.table)

