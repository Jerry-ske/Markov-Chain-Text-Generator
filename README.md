# Markov-Chain-Text-Generator 
import random

def build_markov_chain(text, n=1):
    words = text.split()
    index = n
    markov_chain = {}

    for i in range(len(words) - n):
        key = tuple(words[i:i+n])
        next_word = words[i + n]
        if key in markov_chain:
            markov_chain[key].append(next_word)
        else:
            markov_chain[key] = [next_word]
    return markov_chain

def generate_text(chain, n=1, max_words=50):
    key = random.choice(list(chain.keys()))
    output_words = list(key)

    for _ in range(max_words - n):
        next_words = chain.get(key)
        if not next_words:
            break
        next_word = random.choice(next_words)
        output_words.append(next_word)
        key = tuple(output_words[-n:])
    
    return ' '.join(output_words)

# Example training text
training_text = """Artificial Intelligence is transforming the world. 
Machine learning enables systems to learn from data and improve over time without being explicitly programmed."""

# Build and use the Markov Chain
chain = build_markov_chain(training_text, n=2)  # 2-word sequence
generated = generate_text(chain, n=2, max_words=30)

print("Generated Text:\n", generated)
