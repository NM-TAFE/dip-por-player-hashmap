# Scenario

You are employed as a junior software developer at a boutique software house called Softwares-RUs in Perth. You have been assigned to the Games team and will provide some of the code required for various games that the company builds and releases.

## Task Overview

In the previous task, you implemented a dynamic data structure (a Double Linked List) to store player information. In this task, you will be building upon that work by creating a hash map (in Python) using the player data from the Double Linked List. This will optimize the search and retrieval of player information in the game.

## Requirements

1. **Coding Style:** Your code must adhere to the [PEP-8 – Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/). Familiarize yourself with PEP-8 before continuing as SRU has adopted it as their standard code style. Proper coding style enhances code readability and maintainability.

2. **Git Repository:** The use of a Git repository is standard practice at Softwares-R-Us. Most of the steps in this task require the use of Git and GitHub. Version control is crucial for tracking changes, collaborating with team members, and managing project history.

3. **Task Completion:** There are multiple steps in this task, and you must perform each step to a satisfactory level. Note that the results of the tasks outlined in this scenario will be needed for future tasks as well.

4. **Documentation:**

   - Answer any questions in the provided template (if available) and include relevant screenshots to demonstrate your work.
   - For programming tasks, provide the actual source code as a ZIP-file of the project. Remove the Virtual Environment folder (`venv` or `.venv`) from the ZIP-file before uploading.
   - Document your code properly using docstrings for entire classes and methods. Use inline comments to clarify certain parts of the code. Code documentation aids in understanding and maintaining the codebase.

5. **Testing:** It is expected that the software you create is of high quality and passes a certain level of testing. You will be provided with guidelines regarding the extent of testing expected of you. Ensure that your code is thoroughly tested and meets the specified requirements.

6. **External Resources:** If you use any external resources, provide proper references. Citing sources acknowledges the work of others and allows for further exploration of the topics.

## Learning Objectives

By completing this task, you will:

- Gain experience in creating a hash map data structure in Python.
- Understand how to integrate data from a Double Linked List into a hash map.
- Apply proper coding style following the PEP-8 guidelines.
- Utilize Git and GitHub for version control and project management.
- Practice code documentation using docstrings and inline comments.
- Enhance your problem-solving skills by building upon existing code to implement new data structures.
- Develop skills in software testing and quality assurance.

## Additional Guidance

- Review the concepts of hash maps and their implementation in Python. Understand how they can be used to optimize search and retrieval operations.
- Analyze the existing code from the Double Linked List implementation and identify the relevant player data to be used in the hash map.
- Consider the appropriate hash function to use for mapping player data to the hash map.
- Develop a comprehensive testing plan to ensure the correctness and efficiency of your hash map implementation.
- Follow the provided guidelines for testing and ensure that your code meets the specified quality standards.

Remember, building upon existing code and integrating new data structures requires careful planning and attention to detail. Take your time to understand the requirements, design your approach, and test your code thoroughly.

If you have any questions or need further clarification, don't hesitate to reach out to your instructor or peers for assistance. Good luck with the task!

## Knowledge and Reflection Questions

Answer the knowledge and reflection questions based on the scenario and the task. Your answers will be reviewed by your instructor. These questions are in the file `knowledge-and-reflection.md` you can find in the root of the repository. Some questions are better answered now, while others will be best answered after you have completed the task. Make sure to answer the questions in your own words and back up your answers with proper reasoning or references.

## Step-by-Step Implementation Guide

### Task synopsis

**Hash Map:** Implement a hash map in Python to split player data across multiple double linked lists (`PlayerList`). The hash map will handle collisions by chaining player data using the PlayerList data structure from the previous task.
Note: you **must** use the `PlayerList` class from the previous task to handle collisions and players must be added to the hash map as nodes in a player list.

### Step 1: Review the Existing Code

Your PlayerList is a dynamic data structure: insertions and deletions are easy. But you realise that searching for a player in the PlayerList has a time complexity of O(n) because you have to traverse the entire list to find the player. You decide to implement a hash map to store the player data, which will optimize the search and retrieval of player information.

### Step 2: Implement the Hash Map

You will implement a hash map in Python to store player data. The hash map will use the player data from the PlayerList and handle collisions by chaining player data using the PlayerList data structure. The hash map must include the following methods:

- `put(key, name)`: Add a new player to PlayerList in a corresponding index in the hash map.
- `get(key)`: Retrieve a player from the PlayerList with the corresponding index in the hash map.
- `remove(key)`: Remove a player from the PlayerList with the corresponding index in the hash map.
- `size()`: Return the number of players in the hash map.

You can choose to implement the hash map pythonically such that it behaves like a mutable mapping type (e.g., a dictionary). To do this you could implement the `__getitem__`, `__setitem__`, `__len__`, and `__delitem__` methods, instead of their respective `get`, `put`, `size`, and `remove` methods.

#### Initialising the Hash Map

The hashmap shall have a SIZE of 10 to start with. It should create a list of 10 `PlayerList` objects to store the player data. The `PlayerList` objects will be used to handle collisions.

Important: Consider that the `PlayerList` is **mutable** so code like the following will not work as expected:

```python
class PlayerHashMap:
    SIZE: int = 10
    def __init__(self):
        self.hashmap = [PlayerList()] * self.SIZE # THIS IS BAD!
```

The previous code will create 10 references to the same `PlayerList` object. This means that if you add a player to one of the `PlayerList` objects, it will be added to all of them. Instead, you should create 10 different `PlayerList` objects.

#### Examples: Pseudocode

Here, we'll use **setitem** to add a player to the hash map.

```python
def get_index(self, key: str | Player) -> int:
    if isinstance(key, Player):
        return hash(key) % self.SIZE # TODO: implement __hash__ in player
    else:
        return Player.hash(key) % self.SIZE # TODO implement a hash class method in Player

def __setitem__(self, key: str, name: str) -> none:
    """ Psuedo code:
    1. Use the key to calculate an index into the hash map
       (TODO: Implement a hash function in Player class that returns a player hash and then modulate it by the size of the hashmap)
    2. Get the PlayerList at that index
    3. Check if the player is already in that player list.
         If it is, update the player's name.
         If it isn't, create a player and add the player to the player list.

     """
     # get player's appropriate PlayerList:
     player_list = self.hashmap[self.get_index(key)]
     # check if player is in the list
     # if it is, update the player's name
     # if it isn't, create a player and add the player to the player list


```

````python
### Step 3: Extend the Player Class to provide a hash

You will extend the `Player` class to provide a hash method that will be used to calculate the index in the hash map where the player will be stored. The hash method should return an integer that will be used as the index in the hash map. The integer should be calculated using the player's key (uid) and return an int between 0-255.

In Python, there is a magic method called `__hash__` that is called when the hash() function is called on an object. You can override this method to provide a custom hash for your object.

```python

@classmethod
def your_chosen_hash_function(cls, key: str) -> int:
    ...

def __hash__(self):
    return self.your_chosen_hash_function(self.uid)

````

> **Tip:** To help choose a hash function, see the knowledge and reflection questions.

Finally, while not strictly necessary, you may want to implement a `__eq__` method to compare two players. This will be useful for testing and it is customary that two players returning the same hash are considered equal.

```python
def __eq__(self, other):
    return self.uid == other.uid
```

### Step 4: Test the Hash Map

Create a new test file called `test_hash_map.py` and write comprehensive tests to ensure the correctness and efficiency of your hash map implementation. Your tests should cover all the methods in the hash map and handle edge cases such as adding, retrieving, and removing players from the hash map.
