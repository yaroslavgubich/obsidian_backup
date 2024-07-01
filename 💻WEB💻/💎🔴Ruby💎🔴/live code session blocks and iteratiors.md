![[Pasted image 20240209184224.png]]
#iterators #array 
![[Pasted image 20240209184613.png]]
#each_with_index
![[Pasted image 20240209184942.png]]
 #count #block 
 ![[Pasted image 20240209185111.png]]
#find 
![[Pasted image 20240209185418.png]]
![[Pasted image 20240209190957.png]]
#rspec #ruby #testing 
![[Pasted image 20240209194519.png]]
#alphabet #array
#example #snippet with #map #split #block 
## MULTI-LINE MAP ##

# define a method called acronymize that takes a sentence as an argument
def acronymize(sentence)
  # split the sentence into an array of words
  words = sentence.split(" ")
  # map over the array of words
  first_letters = words.map do |word|
    # return the first letter of each word
    return word[0]
  end 
  # join the array of first letters into a single string and upcase it
  return first_letters.join.upcase
end

## SINGLE-LINE REFACTOR ##

def acronymize(sentence)
  sentence.split.map { |word| word[0] }.join.upcase
end



# CHALLENGE: We want any text passed as a string to the encrypt method to be encrypted using the Caesar cypher
# each letter in the text is shifted a certain number of places in the alphabet
# we'll be backshifting them by 3 places

def encrypt(text)
  alphabet = ("A".."Z").to_a
  letters = text.upcase.split("")
  encryption = letters.map do |character|
    if alphabet.include?(character)
      index = alphabet.index(character)
      alphabet[index - 3]
    else
      character
    end
  end
  return encryption.join
end
#split #range #alphabet 