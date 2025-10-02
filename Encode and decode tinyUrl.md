# Intuition
The goal is to shorten a long URL into a short one and later restore it.  
We can assign each unique URL a numeric ID and convert that ID into a **base62 string** (`[a-zA-Z0-9]`) to produce short, compact, and unique codes.

---

# Approach
1. **Data Structures**  
   - `url_to_id`: Maps each long URL → unique integer ID.  
   - `id_to_url`: Maps each integer ID → original URL.  
   - `counter`: Increments with each new URL.

2. **Encoding (long → short)**  
   - If the URL is already encoded, reuse its ID.  
   - Otherwise, increment `counter`, assign it as ID, and store mappings.  
   - Convert the ID into a base62 string (`encode_id`).  
   - Append it to `"http://tinyurl.com/"`.

3. **Decoding (short → long)**  
   - Remove the prefix to extract the base62 string.  
   - Convert the base62 string back into an integer ID (`decode_id`).  
   - Look up the original URL from `id_to_url`.

4. **Base62 Conversion**  
   - `encode_id`: Repeatedly divide by 62 to build string.  
   - `decode_id`: Convert string back to integer treating it as base62.

---

# Complexity
- **Time Complexity**
  - Encoding: `O(1)` average (dictionary + base62 conversion).  
  - Decoding: `O(1)` average (dictionary + base62 conversion).  

- **Space Complexity**  
  - `O(n)` for storing mappings of `n` unique URLs.  

---

# Code
```python
import string

class Codec:

    def __init__(self):
        self.counter = 0
        self.url_to_id = {}
        self.id_to_url = {}
        self.base = "http://tinyurl.com/"
        self.charset = string.ascii_letters + string.digits

    def encode_id(self, id):
        if id == 0:
            return self.charset[0]
        base62 = []
        while id:
            id, rem = divmod(id, 62)
            base62.append(self.charset[rem])
        return ''.join(reversed(base62))

    def decode_id(self, base62_str):
        id = 0
        for char in base62_str:
            id = id * 62 + self.charset.index(char)
        return id

    def encode(self, longUrl: str) -> str:
        if longUrl in self.url_to_id:
            id = self.url_to_id[longUrl]
        else:
            self.counter += 1
            id = self.counter
            self.url_to_id[longUrl] = id
            self.id_to_url[id] = longUrl
        shortUrl = self.base + self.encode_id(id)
        return shortUrl

    def decode(self, shortUrl: str) -> str:
        base62_str = shortUrl.replace(self.base, "")
        id = self.decode_id(base62_str)
        return self.id_to_url.get(id, "")

# Example usage:
# codec = Codec()
# short = codec.encode("https://example.com")
# original = codec.decode(short)
