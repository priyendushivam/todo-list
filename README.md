# To-Do List Application

This is a simple console-based To Do List application written in C++. The application allows users to add, display, search, update, and delete tasks. Each task is stored with a unique ID and a description. The tasks are saved to a file so that they persist between program executions.

## Features

- **Add Task**: Create new tasks with a unique ID and description.
- **Display Tasks**: View all the current tasks.
- **Search Task**: Find a task by its ID.
- **Delete Task**: Remove a task by its ID.
- **Update Task**: Modify the description of an existing task.

## How to Use

1. **Clone the repository**:
```sh
git clone "https://github.com/PShivam02/todo-list.git"
cd <repository_directory>
```

2. **Compile the program**:
```sh
g++ -o todo_app todo.cpp
```

3. **Run the program**:
```sh
./todo_app
```

## Code Explanation
### Data Structure
A `todo` struct is used to store the ID and description of each task:

```cpp
struct todo {
    int id;
    string task;
};
```

### Functions
1. **addtodo()**: This function adds a new task to the to-do list.
   - Clears the console screen.
   - Prompts the user to enter a task description.
   - Increments the ID counter.
   - Saves the task to `todo.txt` and updates `id.txt` with the new ID.
   - Asks the user if they want to add another task.

2. **print(todo s)**: This function prints the ID and description of a task.
   - Used by other functions to display tasks.
     
3. **readData()**: This function reads and displays all tasks from `todo.txt`.
   - Clears the console screen.
   - Reads tasks from `todo.txt` and calls `print()` to display each task.
     
4. **searchData()**: This function searches for a task by its ID.
   - Clears the console screen.
   - Prompts the user to enter the task ID.
   - Searches through `todo.txt` for the task and displays it using `print()`.
     
5. **deleteData()**: This function deletes a task by its ID.
   - Clears the console screen.
   - Calls `searchData()` to find the task.
   - Prompts the user to confirm deletion.
   - Copies all tasks except the one to be deleted to a temporary file and replaces the original file.
6. **updateData()**: This function updates a task by its ID.
   - Clears the console screen.
   - Calls `searchData()` to find the task.
   - Prompts the user to confirm updating.
   - Prompts the user to enter a new task description.
   - Copies all tasks to a temporary file, replacing the old task description with the new one, and replaces the original file.

### Main Function
The `main()` function initializes the application, reads the current ID from `id.txt`, and displays a menu to the user:

```cpp
int main() {
    // Initial setup
    system("cls");
    cout << "\t___________________________________________________________________" << endl;
    cout << "\t_                      To Do List Application                     _" << endl;
    cout << "\t___________________________________________________________________" << endl << endl << endl << endl;
    
    ifstream read;
    read.open("id.txt");
    if (!read.fail()) {
        read >> ID;
    } else {
        ID = 0;
    }
    read.close();
    
    while (true) {
        cout << endl;
        cout << "\n\t1. Add Task";
        cout << "\n\t2. Display Tasks";
        cout << "\n\t3. Search Task";
        cout << "\n\t4. Delete Task";
        cout << "\n\t5. Update Task";
        
        int choice;
        cout << "\n\n\tEnter choice: ";
        cin >> choice;
        
        switch (choice) {
            case 1:
                addtodo();
                break;
            case 2:
                readData();
                break;
            case 3:
                searchData();
                break;
            case 4:
                deleteData();
                break;
            case 5:
                updateData();
                break;
        }
    }
}
```

## Files
- **todo.txt**: Stores the tasks with their IDs.
- **id.txt**: Stores the current task ID counter.

## Notes
-Ensure that the `todo.txt` and `id.txt` files are in the same directory as the executable.
-The program uses `system("cls")` to clear the console screen, which may not be portable to non-Windows systems. You may need to replace it with `system("clear")` for Unix-based systems.
