# RSS-Guard-Filters
Some RSS Guard filters. I tried using the examples provided in the website and they did not work for me. Thus, I decided to create my own, and share it in the hopes it helps someone else. 

# Set Label depending on Condition

'''
// Keyword and label definition
const keyword = 'steam';
const labelName = 'Steam';

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
'''

# Multiple Condition Labeling

'''
// Array of conditions and their corresponding labels
const conditionsAndLabels = [
    { condition: 'steam', label: 'Steam' },
    { condition: 'notification', label: 'Notifications' },
    { condition: 'tired', label: 'Tired stuff' },
    { condition: 'upgrade', label: 'Upgrades' }
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
'''
