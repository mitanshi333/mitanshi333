def number_to_words(n):
    if n < 1 or n > 999999999:
        return "Number out of range"

    # Basic numbers
    ones = [
        "", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"
    ]
    teens = [
        "ten", "eleven", "twelve", "thirteen", "fourteen", "fifteen", 
        "sixteen", "seventeen", "eighteen", "nineteen"
    ]
    tens = [
        "", "", "twenty", "thirty", "forty", "fifty", "sixty", "seventy", 
        "eighty", "ninety"
    ]
    thousands = ["", "thousand", "million"]

    def chunk_number(n):
        """Break down the number into chunks of three digits."""
        chunks = []
        while n > 0:
            chunks.append(n % 1000)
            n //= 1000
        return chunks

    def convert_chunk(n):
        """Convert a chunk (0-999) to words."""
        if n == 0:
            return ""
        
        words = []
        if n >= 100:
            words.append(ones[n // 100])
            words.append("hundred")
            n %= 100

        if n >= 20:
            words.append(tens[n // 10])
            n %= 10
        
        if n >= 10:
            words.append(teens[n - 10])
            n = 0
        
        if n > 0:
            words.append(ones[n])
        
        return " ".join(words)

    chunks = chunk_number(n)
    word_parts = []
    
    for i in range(len(chunks)):
        if chunks[i] > 0:
            chunk_words = convert_chunk(chunks[i])
            if thousands[i]:
                chunk_words += " " + thousands[i]
            word_parts.append(chunk_words)

    return " ".join(reversed(word_parts)).strip()

# Example usage
number = 123456789
print(number_to_words(number))
