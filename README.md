# RSS-Guard-Filters
I've created some custom RSS Guard filters that I'd like to share with you. After trying out the examples provided on the website without success, I decided to experiment and come up with my own solutions. Needless to say, it is an incredible tool and RSS reader. 

To ensure compatibility, please note that it's essential to create labels with the same name before using these filters. This will help prevent any issues or errors.

# Set Label depending on Condition

```
// Keyword and label definition
const keyword = 'dog';
const labelName = 'Dog';

function filterMessage(msg) {
    if (msg && msg.title) {
        const lowerCaseTitle = msg.title.toLowerCase();
        if (lowerCaseTitle.includes(keyword.toLowerCase())) {
            const labelId = msg.findLabelId(labelName);
            msg.assignLabel(labelId);
        }
    }
    return MessageObject.Accept;
}

// Ensure the script is executed for each message
if (typeof msg !== 'undefined') {
    filterMessage(msg);
} else {
    console.error('Error: msg is not defined.');
}
```

# Multiple Conditions Labeling
This will handle several separate labels at once with the purpose to not clutter the filters. 

```
// Array of conditions and their corresponding labels
const conditionsAndLabels = [
    { condition: 'dog', label: 'Dog' },
    { condition: 'cat', label: 'Cat' },
    { condition: 'stock', label: 'Stocks' },
    { condition: 'tech', label: 'Tech' }
];

// Function to filter and label the current message
function filterMessage(msg) {
    if (msg && msg.title) {
        const lowerCaseTitle = msg.title.toLowerCase();
        
        // Iterate over each condition and label pair
        for (let pair of conditionsAndLabels) {
            const lowerCaseCondition = pair.condition.toLowerCase();
            if (lowerCaseTitle.includes(lowerCaseCondition)) {
                const labelId = msg.findLabelId(pair.label);
                msg.assignLabel(labelId);
                break; // Assign only the first matching label
            }
        }
    }
    return MessageObject.Accept;
}

// Ensure the script is executed for each message
if (typeof msg !== 'undefined') {
    filterMessage(msg);
} else {
    console.error('Error: msg is not defined.');
}
```
# Regex Queries Tips

To activate the Regex Queries, enable "Probes" when selecting additional nodes. This option is located among "Important", "labels", and "Unread."

## AND / OR Operators

For 'OR', use a vertical bar, `|`, without any spaces before and after:

```
dog|cat
```

For 'AND', put the words with a space as separation. This will match the words in order of appearance:

```
dog cat
```

When word order isn't important, lookaheads can help. However, they do slow down the query significantly. I'm keeping an eye out for alternative solutions to improve efficiency:

```
(?=.*cat)(?=.*dog)(?=.*gull)
```

## Case Sensitivity 

"Regex Queries" are **case sensitive** by default. To perform a case-insensitive search, prefix your query with the `-i` flag:


```
(?i)dog
```

```
(?i)dog|cat|seagull
```

