#phone #number #solution 
FRENCH_PHONE_PATTERN = /^(0|\+33[\s-]?)[1-9][\s-]?(\d{2}[\s-]?){4}$/

def french_phone_number?(phone_number)
  !phone_number.match(FRENCH_PHONE_PATTERN).nil?
end


my #solution 

def french_phone_number?(phone_number)

  pp clean_number = phone_number.gsub(/[\s\-]+/, "")

  

  if clean_number.match?(/^(?!0{2})0\d{9}/)

    true

  

  else

    clean_number.match?(/^\+33\d{9}/)

  end

end

  
  
  

pp french_phone_number?("+33 6 65 36 36 36")

#regex #pattern #explanation 
Sure, let's delve deeper into the `FRENCH_PHONE_PATTERN` regular expression, breaking it down for clarity and providing a code snippet to demonstrate its usage.

### Detailed Explanation

```regex
^(0|\+33[\s-]?)[1-9][\s-]?(\d{2}[\s-]?){4}$
```

1. **Start of the Line Assertion (`^`):** This anchors the entire pattern to the beginning of the string, ensuring that what follows matches from the start.

2. **Country Code or Leading Zero Group (`(0|\+33[\s-]?)`):**
   - `0`: Matches a single leading zero, common in domestic French phone numbers.
   - `|`: Logical OR operator, allowing for an alternative match.
   - `\+33`: Matches the international country code for France, `+33`.
   - `[\s-]?`: Matches zero or one occurrence of a space (`\s`) or a hyphen (`-`). This part makes the inclusion of a separator optional after the country code or leading zero.

3. **First Digit of the Phone Number (`[1-9]`):** This matches the first digit of the actual phone number, which must be between 1 and 9. French phone numbers do not start with 0 after the initial country code or leading zero.

4. **Optional Separator After the First Digit (`[\s-]?`):** Allows for an optional space or hyphen after the first digit of the phone number.

5. **Four Groups of Two Digits (`(\d{2}[\s-]?){4}`):**
   - `\d{2}`: Matches exactly two digits, corresponding to the standard grouping in French phone numbers.
   - `[\s-]?`: Permits an optional space or hyphen after each pair of digits.
   - `{4}`: This quantifier repeats the preceding pattern (two digits followed by an optional separator) exactly four times, covering the remaining eight digits of the phone number.

6. **End of the Line Assertion (`$`):** This anchors the pattern to the end of the string, ensuring that it matches only if the pattern concludes with the phone number format specified.

### Code Snippet

The following JavaScript snippet demonstrates how to use the `FRENCH_PHONE_PATTERN` to validate French phone numbers:

```javascript
// Define the French phone number pattern
const FRENCH_PHONE_PATTERN = /^(0|\+33[\s-]?)[1-9][\s-]?(\d{2}[\s-]?){4}$/;

// Test strings
const testNumbers = [
  '0123456789',
  '+33 1 23 45 67 89',
  '01-23-45-67-89',
  '+33-1-23-45-67-89',
  '033123456789' // Invalid format
];

// Function to validate French phone numbers
const validateFrenchPhoneNumber = (number) => FRENCH_PHONE_PATTERN.test(number);

// Validate each test number
testNumbers.forEach(number => {
  const isValid = validateFrenchPhoneNumber(number);
  console.log(`Number: ${number}, IsValid: ${isValid}`);
});
```

This snippet defines the regular expression and tests it against an array of phone numbers. The `validateFrenchPhoneNumber` function uses the `.test` method to check if a given string matches the `FRENCH_PHONE_PATTERN`. The output will indicate whether each number in the `testNumbers` array is valid according to the regex pattern.

### Conclusion

Regular expressions like `FRENCH_PHONE_PATTERN` are powerful tools for pattern matching and validation. By breaking down and understanding each component of the regex, you can tailor it to fit specific validation requirements, such as those for French phone numbers in various formats. The provided code snippet demonstrates how to apply this regex in a practical scenario, validating an array of phone number strings.
how to #return #regex #matched 

```
def word_before_exclamation_mark(sentence)

  regex = /\w+\b(?=\s*!)/

  return sentence.match(regex)[0] if sentence.match?(regex)

end
```


![[Pasted image 20240216132100.png]]

