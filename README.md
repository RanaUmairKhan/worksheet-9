# worksheet-9
import json

def load_tasks():
    try:
        with open('tasks.json') as f:
            tasks = json.load(f)
        return tasks
    except FileNotFoundError:
        return []

def save_tasks(tasks):
    with open('tasks.json', 'w') as f:
        json.dump(tasks, f)

def add_task():
    task = input("Enter the task you want to add: ")
    tasks = load_tasks()
    tasks.append({'task': task, 'completed': False})
    save_tasks(tasks)
    print("Task added successfully!")

def view_tasks():
    tasks = load_tasks()
    print("TODO List:")
    for i, task in enumerate(tasks):
        if task['completed']:
            status = "(Completed)"
        else:
            status = "(Not completed)"
        print(f"{i + 1}. {task['task']} - {status}")

def remove_task():
    task_id = int(input("Enter the task ID you want to remove: "))
    tasks = load_tasks()
    removed_task = tasks.pop(task_id - 1)
    save_tasks(tasks)
    print(f"Task {task_id} removed successfully!")

def mark_task_completed():
    task_id = int(input("Enter the task ID you want to mark as completed: "))
    tasks = load_tasks()
    tasks[task_id - 1]['completed'] = True
    save_tasks(tasks)
    print(f"Task {task_id} marked as completed!")

def main():
    while True:
        print("""
        TODO List App
        1. Add Task
        2. View Tasks
        3. Remove Task
        4. Mark Task as Completed
        5. Exit
        """)
        choice = input("Enter your choice: ")

        if choice == '1':
            add_task()
        elif choice == '2':
            view_tasks()
        elif choice == '3':
            remove_task()
        elif choice == '4':
            mark_task_completed()
        elif choice == '5':
            break
        else:
            print("Invalid choice. Please enter a valid option.")

if __name__ == '__main__':
    main()
