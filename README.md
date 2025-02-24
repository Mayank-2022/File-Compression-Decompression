This README is well-structured and informative. To enhance it, you could add a **Requirements** and **Project Setup** section at the end. Here's an improved version:

---

# **File Compression-Decompression Using Huffman's Algorithm**

## About

Huffman Algorithm is an efficient way for file compression and decompression.  
This program follows Huffman’s algorithm exactly. It reads frequent characters from the input file and replaces them with shorter binary codewords.  
The original file can be produced again without losing any bit.

## Usage

### Compression:
```sh
./encode <file to compress>
```
An output file named `<inputfile>.spd` will be produced.

### Decompression:
```sh
./decode <file to uncompress>
```

## File Structure

| **Content**             | **Description**                                      |
|------------------------|--------------------------------------------------|
| **N (1 byte)**          | Total number of unique characters                |
| **Character (1 byte)**  | Character in the input file                      |
| **Binary codeword**     | Huffman-encoded binary string (max bytes)        |
| **p (1 byte)**         | Padding count (p times `0` bits for alignment)   |
| **DATA**               | Encoded content after mapping                    |

**Example:**  
Text: `aabcbaab`

| **Content**                | **Comment**                                    |
|----------------------------|----------------------------------------------|
| `3`                        | `N=3` (characters: `a`, `b`, `c`)           |
| `a -> "1"`                 | `a` is encoded as `"1"`                      |
| `b -> "01"`                | `b` is encoded as `"01"`                     |
| `c -> "00"`                | `c` is encoded as `"00"`                     |
| `4`                        | Padding count                                |
| `[0000]`                   | 4 zeroes padding                            |
| `[1] [1] [01] [00] [01] [1] [1] [01]` | Encoded content |

## Algorithm

1. **(Pass 1)** Read the input file.
2. Create a sorted linked list of characters based on frequency:
   ```cpp
   for each character ch in file:
       if ch exists in linked list at node p:
           p.freq++
           sort linked list by frequency
       else:
           add new node at beginning of list with frequency = 1
   ```
3. Construct Huffman tree:
   - Create a new node `q` and join two least frequent nodes as its left and right children.
   - Insert `q` into the sorted list.
   - Repeat the process until only one node remains (ROOT of the tree).
   - Perform a **preorder traversal** to assign codewords and recreate the linked list.
4. Write the **character-to-codeword mapping table** to the output file.
5. **(Pass 2)** Read the input file again.
6. Replace each character with its corresponding **codeword** and write it to the output file.
7. End.

## Requirements

Ensure you have the following dependencies:

- **GCC or Clang** (for C/C++ compilation)
- **Make** (for building the project)
- **Linux/macOS/Windows (WSL recommended for Windows users)**

## Project Setup

Follow these steps to set up and run the project:

1. **Clone the repository:**
   ```sh
   git clone https://github.com/Mayank-2022/File-Compression-Decompression
   cd huffman-compression
   ```

2. **Compile the source code:**
   ```sh
   make
   ```
   This will generate the `encode` and `decode` executables.

3. **Run the program:**
   - To compress a file:
     ```sh
     ./encode input.txt
     ```
   - To decompress a file:
     ```sh
     ./decode input.txt.spd
     ```

4. **Clean up (optional):**
   ```sh
   make clean
   ```
   This removes compiled binaries.

## Contributing

Feel free to submit **issues** and **pull requests**.  
Bug reports and testing on different platforms are especially appreciated.

## License

This project is licensed under the [MIT License](https://opensource.org/licenses/MIT).