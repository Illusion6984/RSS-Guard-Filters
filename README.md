# RSS-Guard-Filters
Some RSS Guard filters. I tried using the examples provided in the website and they did not work for me. Thus, I decided to create my own, and share it in the hopes it helps someone else. 

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
