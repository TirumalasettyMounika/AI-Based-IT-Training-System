import streamlit as st

# Set page config
st.set_page_config(
    page_title="AI-Based IT Training System",
    page_icon="🤖",
    layout="wide",
    initial_sidebar_state="collapsed"
)

# Custom CSS for styling
st.markdown("""
<style>
.header {
    font-size: 40px;
    font-weight: bold;
    color: #2E86C1;
    text-align: center;
    padding: 20px;
    background-color: #F4F6F6;
    border-radius: 10px;
    margin-bottom: 20px;
}
.card {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    border-radius: 5px;
    padding: 16px;
    margin: 10px;
    background-color: #f9f9f9;
}
.card:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}
</style>
""", unsafe_allow_html=True)

# Main heading
st.markdown('<div class="header">AI-Based IT Training System</div>', unsafe_allow_html=True)

# Initialize session state
if "page" not in st.session_state:
    st.session_state.page = "User Profile"

page = st.session_state.page

# User Profile Page
if page == "User Profile":
    st.title("User Profile")
    
    # User Profile Form
    with st.form("user_profile_form"):
        name = st.text_input("Name")
        email = st.text_input("Email Address")
        gender = st.selectbox("Gender", ["Male", "Female", "Other"])
        programming_languages = st.multiselect("Select programming language you want to learn", ["Python", "Java", "C++", "SQL"])
        submit = st.form_submit_button("Save Profile")
    
    if submit:
        st.session_state.programming_languages = programming_languages
        st.session_state.page = "Mock Exams"
        st.rerun()

elif page == "Mock Exams":
    st.title("Test your knowledge!!")
    
    # Store the selected level in session state
    if 'level' not in st.session_state:
        st.session_state.level = "Beginner"  # Default level
    
    # Allow the user to select the difficulty level
    level = st.selectbox("Select Difficulty Level", ["Beginner", "Intermediate", "Advanced"], key="level_select")
    
    # Update the session state with the selected level
    st.session_state.level = level
    
    mcq_questions = {
    "Python": {
        "Beginner": [
            ("What is the correct way to create a function in Python?", 
             ["def function_name[]:", "function_name():", "def function_name():", "function function_name():"], 2),
            ("Which of the following is a mutable data type in Python?", 
             ["tuple", "list", "string", "int"], 1),
            ("Which of the following is the correct syntax to print 'Hello World' in Python?", 
             ["echo 'Hello World'", "print('Hello World')", "println('Hello World')", "System.out.println('Hello World')"], 1),
            ("What does the 'len()' function do in Python?", 
             ["Returns the length of a number", "Returns the length of an object (e.g., list, string)", 
              "Returns a list", "It has no functionality"], 1),
            ("Which of the following statements is used to terminate a loop in Python?", 
             ["stop", "break", "exit", "quit"], 1),
        ],
        "Intermediate": [
            ("Which of the following Python data types is immutable?", 
             ["list", "dict", "set", "tuple"], 3),
            ("What is the output of the following Python code?\n```python\nx = [1, 2, 3]\nx.append([4, 5])\nprint(len(x))\n```", 
             ["3", "4", "5", "6"], 1),
            ("Which of the following is used to handle exceptions in Python?", 
             ["try...except", "try...catch", "try...finally", "exception...catch"], 0),
            ("What will be the output of the following Python code?\n```python\ndef func(x):\n    return x * 2\nprint(func(3))\n```", 
             ["3", "6", "33", "None"], 1),
            ("Which of the following will create a dictionary in Python?", 
             ["{1, 2, 3}", "[1: 'a', 2: 'b']", "{'a': 1, 'b': 2}", "(1, 2)"], 2),
        ],
        "Advanced": [
            ("Which method in Python is used to check if a key exists in a dictionary?", 
             ["has_key()", "contains_key()", "in", "get_key()"], 2),
            ("What is the purpose of the '__init__' method in Python?", 
             ["It initializes the Python interpreter", "It is used to initialize object attributes", 
              "It initializes a module", "It initializes variables inside a function"], 1),
            ("Which of the following is correct way to use list comprehension in Python?", 
             ["[x for x in range(10)]", "range[10]", "x in range(10) for x", "x, for x in range(10)"], 0),
            ("Which of the following Python modules is used for working with regular expressions?", 
             ["os", "math", "re", "sys"], 2),
            ("What is the output of the following code?\n```python\nclass A:\n    def __init__(self):\n        self.value = 0\n    def increment(self):\n        self.value += 1\n\nclass B(A):\n    def increment(self):\n        self.value += 2\n\nobj = B()\nobj.increment()\nprint(obj.value)\n```", 
             ["0", "1", "2", "3"], 2),
        ]
    },
    "Java": {
        "Beginner": [
            ("What is Java?", 
             ["A scripting language", "A programming language", "A database", "A framework"], 1),
            ("Which keyword is used to define a class in Java?", 
             ["class", "Class", "define", "struct"], 0),
            ("Which data type is used to represent a single character in Java?", 
             ["String", "char", "int", "boolean"], 1),
            ("Which method is the entry point for a Java application?", 
             ["main()", "start()", "run()", "init()"], 0),
            ("Which of the following is used to create a new object in Java?", 
             ["create object", "new", "object()", "initialize"], 1),
        ],
        "Intermediate": [
            ("Which of the following is used to inherit from a class in Java?", 
             ["implements", "extends", "inherits", "super"], 1),
            ("What is the default value of an instance variable of type 'boolean' in Java?", 
             ["false", "true", "0", "null"], 0),
            ("Which of the following is correct syntax to call a static method in Java?", 
             ["object.method()", "Class.method()", "this.method()", "static.method()"], 1),
            ("Which of the following is used to handle exceptions in Java?", 
             ["try...catch", "try...finally", "throw...catch", "try...exit"], 0),
            ("Which of the following is the correct syntax to declare an array in Java?", 
             ["int[] arr;", "int arr[];", "int arr;", "Both a and b are correct."], 3),
        ],
        "Advanced": [
            ("Which of the following interfaces is implemented by all classes that can be printed in Java?", 
             ["Printable", "PrintableInterface", "PrintInterface", "java.lang.Printable"], 3),
            ("What does the 'super' keyword do in Java?", 
             ["Refers to the superclass of the current object", "Initializes a new object", 
              "Exits the method", "Calls a method of the current class"], 0),
            ("Which of the following is true about Java Generics?", 
             ["They allow for type-safe data structures", "They are used for method overloading", 
              "They do not support primitive data types", "All of the above"], 3),
            ("What is the purpose of the 'final' keyword in Java?", 
             ["To declare a constant", "To prevent method overriding", "To prevent inheritance of a class", 
              "All of the above"], 3),
            ("Which of the following classes can be used to create a thread in Java?", 
             ["Thread", "Runnable", "Executor", "All of the above"], 3),
        ]
    },
    "C++": {
        "Beginner": [
            ("Which of the following is the correct way to declare a variable in C++?", 
             ["int num;", "num int;", "int = num;", "num; int"], 0),
            ("Which of the following is the correct syntax for a 'for' loop in C++?", 
             ["for (int i = 0; i < 10; i++)", "for (i = 0; i < 10; i++)", "for (int i = 0; i < 10; i++) {}", 
              "for int i in range(10)"], 0),
            ("What is the correct way to include a header file in C++?", 
             ["#import <iostream>", "#include <iostream>", "#define <iostream>", "#include iostream"], 1),
            ("Which of the following is used to output to the console in C++?", 
             ["echo", "System.out.println()", "cout", "print()"], 2),
            ("Which of the following types is a fundamental data type in C++?", 
             ["string", "char", "Integer", "list"], 1),
        ],
        "Intermediate": [
            ("Which of the following is used to dynamically allocate memory in C++?", 
             ["new", "malloc", "alloc", "Both a and b"], 3),
            ("Which of the following is a valid operator in C++?", 
             ["++", "+=", "==", "All of the above"], 3),
            ("What is the output of the following C++ code?\n```cpp\nint main() {\n    int x = 5;\n    int y = 2;\n    cout << x / y;\n    return 0;\n}\n```", 
             ["3", "2", "2.5", "Error"], 1),
            ("Which of the following is a correct way to declare a class in C++?", 
             ["class MyClass;", "class MyClass() { }", "MyClass class { }", "class MyClass { }"], 3),
            ("Which of the following is a feature of a constructor in C++?", 
             ["It is called automatically when an object is created", "It has no return type", 
              "It can be overloaded", "All of the above"], 3),
        ],
        "Advanced": [
            ("What is the purpose of a virtual function in C++?", 
             ["To allow dynamic dispatch of functions", "To prevent function overriding", "To create a static method", 
              "To allow multiple inheritance"], 0),
            ("What is the output of the following C++ code?\n```cpp\nclass Base {\npublic:\n    virtual void show() { cout << 'Base' << endl; }\n};\n\nclass Derived : public Base {\npublic:\n    void show() { cout << 'Derived' << endl; }\n};\n\nint main() {\n    Base* b;\n    Derived d;\n    b = &d;\n    b->show();\n    return 0;\n}\n```", 
             ["Base", "Derived", "Error", "Nothing is printed"], 1),
            ("What is the purpose of a destructor in C++?", 
             ["It is used to release resources when an object is destroyed", "It initializes an object when created", 
              "It is used to allocate memory", "It can be overloaded"], 0),
            ("Which of the following is true about C++ exceptions?", 
             ["Exception handling in C++ uses 'try', 'throw', and 'catch'", "Exception handling is mandatory in C++", 
              "'throw' can only be used for built-in types", "Exceptions in C++ cannot be inherited"], 0),
            ("What does the 'mutable' keyword do in C++?", 
             ["Allows a member variable to be modified even if the object is const", 
              "Allows dynamic memory allocation", "Indicates that a variable is global", 
              "Prevents a variable from being modified"], 0),
        ]
    },
    "SQL": {
        "Beginner": [
            ("Which of the following SQL statements is used to retrieve data from a database?", 
             ["SELECT", "GET", "EXTRACT", "FETCH"], 0),
            ("What is the SQL command to delete all rows from a table without removing the table itself?", 
             ["DELETE FROM table;", "DROP TABLE table;", "REMOVE ALL FROM table;", "TRUNCATE TABLE table;"], 0),
            ("Which SQL clause is used to sort the result set?", 
             ["ORDER BY", "SORT BY", "GROUP BY", "LIMIT"], 0),
            ("Which of the following is used to specify a condition in an SQL 'SELECT' statement?", 
             ["WHERE", "IF", "WHEN", "CONDITION"], 0),
            ("Which SQL statement is used to insert new data into a table?", 
             ["INSERT INTO", "ADD INTO", "APPEND INTO", "INSERT"], 0),
        ],
        "Intermediate": [
            ("Which of the following SQL functions is used to find the highest value in a column?", 
             ["MAX()", "HIGH()", "TOP()", "LARGEST()"], 0),
            ("What does the 'JOIN' clause do in SQL?", 
             ["Combines rows from two or more tables", "Sorts data from multiple tables", 
              "Filters records from multiple tables", "Limits the number of rows in a result set"], 0),
            ("Which SQL keyword is used to eliminate duplicate values in a query result?", 
             ["DISTINCT", "UNIQUE", "NO_DUPLICATES", "REMOVE_DUPLICATES"], 0),
            ("Which of the following is used to modify existing data in a table in SQL?", 
             ["UPDATE", "MODIFY", "SET", "CHANGE"], 0),
            ("Which of the following statements will return the number of rows in a table in SQL?", 
             ["COUNT(*)", "NUM_ROWS()", "ROWS()", "COUNT()"], 0),
        ],
        "Advanced": [
            ("What is the purpose of the 'GROUP BY' clause in SQL?", 
             ["It groups rows that have the same values in specified columns", 
              "It sorts rows in ascending or descending order", "It filters rows based on a condition", 
              "It aggregates rows in the result set"], 0),
            # Add more advanced SQL questions as needed...
        ]
    }
}
    selected_questions = []
    for lang in st.session_state.programming_languages:
        selected_questions.extend(mcq_questions.get(lang, {}).get(level, []))
    
    # Store selected_questions in session state
    st.session_state.selected_questions = selected_questions
    
    if 'question_index' not in st.session_state:
        st.session_state.question_index = 0
    if 'answers' not in st.session_state:
        st.session_state.answers = {}
    if 'exam_started' not in st.session_state:
        st.session_state.exam_started = False
    
    if not st.session_state.exam_started:
        if st.button("Take Exam"):
            st.session_state.exam_started = True
            st.rerun()
    else:
        total_mcq = len(selected_questions)
        
        if st.session_state.question_index < total_mcq:
            question, options, correct_index = selected_questions[st.session_state.question_index]
            st.write(f"Question {st.session_state.question_index + 1}: {question}")
            choice = st.radio("Choose one:", options, key=f"mcq_{st.session_state.question_index}")
            
            if st.button("Next Question"):
                st.session_state.answers[st.session_state.question_index] = choice
                st.session_state.question_index += 1
                st.rerun()
        else:
            if st.button("Submit Exam"):
                st.success("Exam Submitted! Check results.")
                st.session_state.page = "Results & Next Steps"
                st.session_state.question_index = 0
                st.rerun()

elif page == "Results & Next Steps":
    st.title("Results & Next Steps")

    # Retrieve selected questions from session state
    selected_questions = st.session_state.selected_questions
    
    # Retrieve user-selected skill level
    skill_level = st.session_state.get("skill_level", "Beginner")  # Default to Beginner if not set

    # Calculate the score
    total_questions = len(st.session_state.answers)
    correct_answers = sum(
        1 for i, (question, options, correct_index) in enumerate(selected_questions)
        if st.session_state.answers.get(i) == options[correct_index]
    )
    
    score = (correct_answers / total_questions) * 100 if total_questions > 0 else 0

    # Display the score
    st.write(f"Your score: {score:.2f}%")

    # Apply the threshold and provide feedback
    if score >= 70:
        st.success("Congratulations! You have passed the exam with a score of 70% or above.")
        
        # Show "Choose a Different Level" and "Start the Course" buttons
        col1, col2 = st.columns(2)
        with col1:
            if st.button("Choose a Different Level"):
                st.session_state.page = "Mock Exams"
                st.session_state.exam_started = False
                st.session_state.question_index = 0
                st.session_state.answers = {}
                st.rerun()
        with col2:
            if st.button("Start the Course"):
                st.session_state.page = "Course Materials"
                st.rerun()
    
    else:
        if skill_level == "Beginner":
            st.info(f"It's okay! You're still a beginner. Start the course to learn {st.session_state.get('course_name', 'your chosen subject')}.")
            
            # Only show "Retake Exam" and "Start the Course" for beginners
            col1, col2 = st.columns(2)
            with col1:
                if st.button("Retake Exam"):
                    st.session_state.page = "Mock Exams"
                    st.session_state.exam_started = False
                    st.session_state.question_index = 0
                    st.session_state.answers = {}
                    st.rerun()
            with col2:
                if st.button("Start the Course"):
                    st.session_state.page = "Course Materials"
                    st.rerun()
        
        else:
            st.warning("Your score is below 70%. It would be appreciated if you choose a previous level.")
            
            # Show all buttons (Retake Exam, Choose a Different Level, Start the Course)
            col1, col2, col3 = st.columns(3)
            with col1:
                if st.button("Retake Exam"):
                    st.session_state.page = "Mock Exams"
                    st.session_state.exam_started = False
                    st.session_state.question_index = 0
                    st.session_state.answers = {}
                    st.rerun()
            with col2:
                if st.button("Choose a Different Level"):
                    st.session_state.page = "Mock Exams"
                    st.session_state.exam_started = False
                    st.session_state.question_index = 0
                    st.session_state.answers = {}
                    st.rerun()
            with col3:
                if st.button("Start the Course"):
                    st.session_state.page = "Course Materials"
                    st.rerun()


elif page == "Course Materials":
    st.title("Course Materials")
    
    # Retrieve the selected subject and difficulty level
    selected_subject = st.session_state.programming_languages[0]  # Assuming the user selected one subject
    selected_level = st.session_state.level  # Retrieve the level from session state
    
    # Define course materials for each subject and difficulty level
    course_materials = {
        "Python": {
    "Beginner": [
        {"topic": "Introduction to Python", 
         "theory": "Python is a versatile, high-level programming language that is easy to learn and use. It emphasizes readability and simplicity, making it an ideal choice for beginners. Python is used for a wide variety of applications, including web development, data analysis, artificial intelligence, and more.",
         "examples": [
            "Example 1: Print 'Hello, World!'",
            "```python\nprint('Hello, World!')\n```",
            "Example 2: Basic arithmetic operations",
            "```python\nx = 10\ny = 20\nsum = x + y\nprint(sum)\n```"
        ]},
        
        {"topic": "Variables and Data Types", 
         "theory": "Variables store data values. In Python, you do not need to declare a variable type, as Python automatically infers the type. Common data types include integers (int), floating-point numbers (float), and strings (str).",
         "examples": [
            "Example 1: Declaring variables",
            "```python\nx = 10\nname = 'Alice'\nprice = 99.99\n```",
            "Example 2: Type conversion",
            "```python\nx = 10\nstr_x = str(x)  # Convert integer to string\nprint(str_x)\n```"
        ]},
        
        {"topic": "Control Structures", 
         "theory": "Control structures include if-else, loops (for, while), and conditionals that help determine the flow of the program based on certain conditions.",
         "examples": [
            "Example 1: If-else statement",
            "```python\nage = 18\nif age >= 18:\n    print('Adult')\nelse:\n    print('Not an adult')\n```",
            "Example 2: For loop",
            "```python\nfor i in range(5):\n    print(i)\n```"
        ]}
    ],
    
    "Intermediate": [
        {"topic": "Functions", 
         "theory": "Functions are reusable blocks of code that allow you to perform specific tasks. They help to make your code modular and maintainable. Functions can accept parameters and return values.",
         "examples": [
            "Example 1: Defining a function",
            "```python\ndef greet(name):\n    print(f'Hello, {name}')\ngreet('Bob')\n```",
            "Example 2: Function with parameters",
            "```python\ndef add_numbers(a, b):\n    return a + b\nresult = add_numbers(5, 10)\nprint(result)  # Output: 15\n```"
        ]},
        
        {"topic": "File Handling", 
         "theory": "File handling allows you to read and write files on the system. Python makes file operations easy with functions like open(), read(), write(), and close().",
         "examples": [
            "Example 1: Reading a file",
            "```python\nwith open('example.txt', 'r') as file:\n    content = file.read()\n    print(content)\n```",
            "Example 2: Writing to a file",
            "```python\nwith open('output.txt', 'w') as file:\n    file.write('Hello, Python!')\n```"
        ]},
        
        {"topic": "Error Handling", 
         "theory": "Error handling helps manage exceptions that may occur during program execution. The try-except block is used to handle errors and allow the program to continue running.",
         "examples": [
            "Example 1: Try-except block",
            "```python\ntry:\n    x = 10 / 0\nexcept ZeroDivisionError:\n    print('Cannot divide by zero!')\n```",
            "Example 2: Custom exceptions",
            "```python\nclass MyCustomError(Exception):\n    pass\n\ntry:\n    raise MyCustomError('This is a custom error!')\nexcept MyCustomError as e:\n    print(e)\n```"
        ]}
    ],
    
    "Advanced": [
        {"topic": "Object-Oriented Programming", 
         "theory": "Object-Oriented Programming (OOP) is a paradigm based on the concept of objects. It allows you to organize your code into classes, each containing methods (functions) and attributes (variables). Inheritance, polymorphism, and encapsulation are key principles of OOP.",
         "examples": [
            "Example 1: Creating a class",
            "```python\nclass Car:\n    def __init__(self, make, model):\n        self.make = make\n        self.model = model\n    def display_info(self):\n        print(f'{self.make} {self.model}')\n\nmy_car = Car('Toyota', 'Corolla')\nmy_car.display_info()\n```",
            "Example 2: Inheritance",
            "```python\nclass ElectricCar(Car):\n    def __init__(self, make, model, battery_size):\n        super().__init__(make, model)\n        self.battery_size = battery_size\n    def display_battery(self):\n        print(f'Battery size: {self.battery_size} kWh')\n\nmy_tesla = ElectricCar('Tesla', 'Model S', 100)\nmy_tesla.display_info()\nmy_tesla.display_battery()\n```"
        ]},
        
        {"topic": "Modules and Packages", 
         "theory": "Modules are files containing Python code that can be imported into other programs. A package is a collection of modules organized in directories. Python has many built-in modules, such as 'math' and 'os'.",
         "examples": [
            "Example 1: Importing a module",
            "```python\nimport math\nprint(math.sqrt(16))  # Output: 4.0\n```",
            "Example 2: Creating a package",
            "```python\n# Create a directory named 'my_package'\n# Inside 'my_package', create a module 'math_ops.py' with functions\n# my_package/math_ops.py\n\ndef add(a, b):\n    return a + b\n\n# Now, import and use the module\nfrom my_package import math_ops\nresult = math_ops.add(5, 10)\nprint(result)  # Output: 15\n```"
        ]},
        
        {"topic": "Decorators", 
         "theory": "Decorators are a powerful tool in Python that allow you to modify the behavior of functions or methods. They are commonly used for logging, access control, memoization, etc.",
         "examples": [
            "Example 1: Simple decorator",
            "```python\ndef my_decorator(func):\n    def wrapper():\n        print('Before function call')\n        func()\n        print('After function call')\n    return wrapper\n\n@my_decorator\ndef greet():\n    print('Hello, World!')\ngreet()\n```",
            "Example 2: Decorator with arguments",
            "```python\ndef repeat(n):\n    def decorator(func):\n        def wrapper(*args, **kwargs):\n            for _ in range(n):\n                func(*args, **kwargs)\n        return wrapper\n    return decorator\n\n@repeat(3)\ndef say_hello():\n    print('Hello!')\n\nsay_hello()\n```"
        ]}
    ]
},
        "Java": {
    "Beginner": [
        {"topic": "Introduction to Java", 
         "theory": "Java is a high-level, object-oriented programming language that is platform-independent. Java is widely used in web development, mobile applications (Android), and enterprise-level systems.",
         "examples": [
            "Example 1: Print 'Hello, World!'",
            "```java\npublic class HelloWorld {\n    public static void main(String[] args) {\n        System.out.println('Hello, World!');\n    }\n}\n```",
            "Example 2: Basic arithmetic operations",
            "```java\npublic class Arithmetic {\n    public static void main(String[] args) {\n        int x = 10;\n        int y = 20;\n        int sum = x + y;\n        System.out.println(sum);\n    }\n}\n```"
        ]},
        
        {"topic": "Variables and Data Types", 
         "theory": "In Java, variables store data values. Java is a statically-typed language, so every variable must be declared with a specific type. Common data types in Java include int, double, char, and String.",
         "examples": [
            "Example 1: Declaring variables",
            "```java\nint age = 25;\nString name = 'Alice';\ndouble price = 99.99;\n```",
            "Example 2: Type conversion",
            "```java\nint x = 10;\ndouble y = (double) x;  // Type casting\nSystem.out.println(y);  // Output: 10.0\n```"
        ]},
        
        {"topic": "Control Structures", 
         "theory": "Control structures in Java include conditional statements (if-else, switch) and loops (for, while) that help manage the flow of program execution.",
         "examples": [
            "Example 1: If-else statement",
            "```java\nint age = 18;\nif (age >= 18) {\n    System.out.println('Adult');\n} else {\n    System.out.println('Not an adult');\n}\n```",
            "Example 2: For loop",
            "```java\nfor (int i = 0; i < 5; i++) {\n    System.out.println(i);\n}\n```"
        ]}
    ],
    
    "Intermediate": [
        {"topic": "Functions (Methods)", 
         "theory": "In Java, functions are called methods and are blocks of code designed to perform a specific task. Methods can accept parameters and return values.",
         "examples": [
            "Example 1: Defining a method",
            "```java\npublic class Greeting {\n    public static void greet(String name) {\n        System.out.println('Hello, ' + name);\n    }\n    public static void main(String[] args) {\n        greet('Bob');\n    }\n}\n```",
            "Example 2: Method with parameters",
            "```java\npublic class Calculator {\n    public static int addNumbers(int a, int b) {\n        return a + b;\n    }\n    public static void main(String[] args) {\n        int result = addNumbers(5, 10);\n        System.out.println(result);  // Output: 15\n    }\n}\n```"
        ]},
        
        {"topic": "File Handling", 
         "theory": "File handling allows you to read from and write to files in Java using classes like File, FileReader, FileWriter, and BufferedReader.",
         "examples": [
            "Example 1: Reading a file",
            "```java\nimport java.io.*;\n\npublic class FileReaderExample {\n    public static void main(String[] args) throws IOException {\n        BufferedReader br = new BufferedReader(new FileReader('example.txt'));\n        String content = br.readLine();\n        System.out.println(content);\n        br.close();\n    }\n}\n```",
            "Example 2: Writing to a file",
            "```java\nimport java.io.*;\n\npublic class FileWriterExample {\n    public static void main(String[] args) throws IOException {\n        BufferedWriter bw = new BufferedWriter(new FileWriter('output.txt'));\n        bw.write('Hello, Java!');\n        bw.close();\n    }\n}\n```"
        ]},
        
        {"topic": "Error Handling", 
         "theory": "Error handling in Java is done using exception handling. The try-catch block is used to catch exceptions and handle errors gracefully.",
         "examples": [
            "Example 1: Try-catch block",
            "```java\npublic class ErrorHandling {\n    public static void main(String[] args) {\n        try {\n            int result = 10 / 0;\n        } catch (ArithmeticException e) {\n            System.out.println('Cannot divide by zero!');\n        }\n    }\n}\n```",
            "Example 2: Custom exceptions",
            "```java\nclass MyCustomException extends Exception {\n    public MyCustomException(String message) {\n        super(message);\n    }\n}\n\npublic class CustomExceptionExample {\n    public static void main(String[] args) throws MyCustomException {\n        throw new MyCustomException('This is a custom exception');\n    }\n}\n```"
        ]}
    ],
    
    "Advanced": [
        {"topic": "Object-Oriented Programming", 
         "theory": "Java is an object-oriented programming (OOP) language, which means it focuses on the concept of objects and classes. Key principles of OOP include inheritance, polymorphism, encapsulation, and abstraction.",
         "examples": [
            "Example 1: Creating a class",
            "```java\nclass Car {\n    String make;\n    String model;\n    public Car(String make, String model) {\n        this.make = make;\n        this.model = model;\n    }\n    public void displayInfo() {\n        System.out.println(make + ' ' + model);\n    }\n}\n\npublic class Main {\n    public static void main(String[] args) {\n        Car myCar = new Car('Toyota', 'Corolla');\n        myCar.displayInfo();\n    }\n}\n```",
            "Example 2: Inheritance",
            "```java\nclass ElectricCar extends Car {\n    int batterySize;\n    public ElectricCar(String make, String model, int batterySize) {\n        super(make, model);\n        this.batterySize = batterySize;\n    }\n    public void displayBattery() {\n        System.out.println('Battery size: ' + batterySize + ' kWh');\n    }\n}\n\npublic class Main {\n    public static void main(String[] args) {\n        ElectricCar tesla = new ElectricCar('Tesla', 'Model S', 100);\n        tesla.displayInfo();\n        tesla.displayBattery();\n    }\n}\n```"
        ]},
        
        {"topic": "Modules and Packages", 
         "theory": "Java allows you to create packages to organize your classes. A package is a group of related classes and interfaces. You can use the `import` statement to use classes from other packages.",
         "examples": [
            "Example 1: Importing a package",
            "```java\nimport java.util.*;\n\npublic class Main {\n    public static void main(String[] args) {\n        ArrayList<String> list = new ArrayList<>();\n        list.add('Java');\n        list.add('Python');\n        System.out.println(list);\n    }\n}\n```",
            "Example 2: Creating a package",
            "```java\n// Create a directory named 'mypackage' and add this code in a file 'Car.java' inside that directory.\npackage mypackage;\n\npublic class Car {\n    String make;\n    String model;\n    public Car(String make, String model) {\n        this.make = make;\n        this.model = model;\n    }\n}\n\n// In your main program, use this package as follows:\nimport mypackage.Car;\n\npublic class Main {\n    public static void main(String[] args) {\n        Car myCar = new Car('Toyota', 'Corolla');\n    }\n}\n```"
        ]},
        
        {"topic": "Lambda Expressions", 
         "theory": "Lambda expressions in Java provide a clear and concise way to represent one method interface using an expression. They allow us to pass behavior as arguments to functions or methods.",
         "examples": [
            "Example 1: Simple lambda expression",
            "```java\nimport java.util.*;\n\npublic class Main {\n    public static void main(String[] args) {\n        List<String> list = Arrays.asList('apple', 'banana', 'cherry');\n        list.forEach(s -> System.out.println(s));\n    }\n}\n```",
            "Example 2: Lambda with parameters",
            "```java\ninterface Addable {\n    int add(int a, int b);\n}\n\npublic class Main {\n    public static void main(String[] args) {\n        Addable adder = (a, b) -> a + b;\n        System.out.println(adder.add(5, 10));  // Output: 15\n    }\n}\n```"
        ]}
    ]
},
        "C++": {
    "Beginner": [
        {"topic": "Introduction to C++", 
         "theory": "C++ is a general-purpose, object-oriented programming language. It is an extension of the C programming language with object-oriented features like classes and objects. C++ is used in system software, game development, and real-time applications.",
         "examples": [
            "Example 1: Print 'Hello, World!'",
            "```cpp\n#include <iostream>\nusing namespace std;\nint main() {\n    cout << 'Hello, World!';\n    return 0;\n}\n```",
            "Example 2: Basic arithmetic operations",
            "```cpp\n#include <iostream>\nusing namespace std;\nint main() {\n    int x = 10, y = 20;\n    int sum = x + y;\n    cout << sum;\n    return 0;\n}\n```"
        ]},
        
        {"topic": "Variables and Data Types", 
         "theory": "In C++, variables store data values, and every variable has a specific type, such as int, float, double, or char. C++ requires the explicit declaration of variables before usage.",
         "examples": [
            "Example 1: Declaring variables",
            "```cpp\nint age = 25;\nchar grade = 'A';\nfloat price = 99.99;\n```",
            "Example 2: Type conversion",
            "```cpp\nint x = 10;\nfloat y = (float) x;  // Type casting\ncout << y;  // Output: 10.0\n```"
        ]},
        
        {"topic": "Control Structures", 
         "theory": "C++ uses control structures such as if-else statements and loops (for, while) to control the flow of execution based on conditions and repetitions.",
         "examples": [
            "Example 1: If-else statement",
            "```cpp\nint age = 18;\nif (age >= 18) {\n    cout << 'Adult';\n} else {\n    cout << 'Not an adult';\n}\n```",
            "Example 2: For loop",
            "```cpp\nfor (int i = 0; i < 5; i++) {\n    cout << i << ' ';\n}\n```"
        ]}
    ],
    
    "Intermediate": [
        {"topic": "Functions", 
         "theory": "Functions in C++ are blocks of reusable code that allow you to perform specific tasks. Functions can accept parameters and return values, improving code modularity and reusability.",
         "examples": [
            "Example 1: Defining a function",
            "```cpp\n#include <iostream>\nusing namespace std;\nvoid greet(string name) {\n    cout << 'Hello, ' << name;\n}\nint main() {\n    greet('Bob');\n    return 0;\n}\n```",
            "Example 2: Function with return value",
            "```cpp\n#include <iostream>\nusing namespace std;\nint add(int a, int b) {\n    return a + b;\n}\nint main() {\n    int result = add(5, 10);\n    cout << result;  // Output: 15\n    return 0;\n}\n```"
        ]},
        
        {"topic": "File Handling", 
         "theory": "C++ provides file handling mechanisms to read from and write to files using classes like ifstream, ofstream, and fstream.",
         "examples": [
            "Example 1: Reading a file",
            "```cpp\n#include <iostream>\n#include <fstream>\nusing namespace std;\nint main() {\n    ifstream infile('example.txt');\n    string content;\n    getline(infile, content);\n    cout << content;\n    infile.close();\n    return 0;\n}\n```",
            "Example 2: Writing to a file",
            "```cpp\n#include <iostream>\n#include <fstream>\nusing namespace std;\nint main() {\n    ofstream outfile('output.txt');\n    outfile << 'Hello, C++!';\n    outfile.close();\n    return 0;\n}\n```"
        ]},
        
        {"topic": "Error Handling", 
         "theory": "C++ provides error handling via exceptions using try-catch blocks. This allows you to manage unexpected errors and ensure program stability.",
         "examples": [
            "Example 1: Try-catch block",
            "```cpp\n#include <iostream>\nusing namespace std;\nint main() {\n    try {\n        int result = 10 / 0;\n    } catch (const exception& e) {\n        cout << 'Error: ' << e.what();\n    }\n    return 0;\n}\n```",
            "Example 2: Custom exceptions",
            "```cpp\n#include <iostream>\n#include <exception>\nusing namespace std;\nclass MyCustomException : public exception {\n    const char* what() const noexcept override {\n        return 'Custom exception occurred!';\n    }\n};\nint main() {\n    throw MyCustomException();\n    return 0;\n}\n```"
        ]}
    ],
    
    "Advanced": [
        {"topic": "Object-Oriented Programming", 
         "theory": "C++ is an object-oriented programming (OOP) language that emphasizes encapsulation, inheritance, and polymorphism. You define classes and create objects to model real-world entities.",
         "examples": [
            "Example 1: Creating a class",
            "```cpp\n#include <iostream>\nusing namespace std;\nclass Car {\npublic:\n    string make;\n    string model;\n    Car(string m, string mo) : make(m), model(mo) {}\n    void displayInfo() {\n        cout << make << ' ' << model;\n    }\n};\nint main() {\n    Car myCar('Toyota', 'Corolla');\n    myCar.displayInfo();\n    return 0;\n}\n```",
            "Example 2: Inheritance",
            "```cpp\n#include <iostream>\nusing namespace std;\nclass ElectricCar : public Car {\npublic:\n    int batterySize;\n    ElectricCar(string m, string mo, int b) : Car(m, mo), batterySize(b) {}\n    void displayBattery() {\n        cout << 'Battery size: ' << batterySize << ' kWh';\n    }\n};\nint main() {\n    ElectricCar tesla('Tesla', 'Model S', 100);\n    tesla.displayInfo();\n    tesla.displayBattery();\n    return 0;\n}\n```"
        ]},
        
        {"topic": "Templates", 
         "theory": "C++ templates allow you to define functions and classes that work with any data type, which provides flexibility and reusability. Templates are key to generic programming in C++.",
         "examples": [
            "Example 1: Function template",
            "```cpp\n#include <iostream>\nusing namespace std;\ntemplate <typename T>\nT add(T a, T b) {\n    return a + b;\n}\nint main() {\n    cout << add(5, 10);  // Output: 15\n    cout << add(2.5, 3.5);  // Output: 6.0\n    return 0;\n}\n```",
            "Example 2: Class template",
            "```cpp\n#include <iostream>\nusing namespace std;\ntemplate <typename T>\nclass Box {\npublic:\n    T value;\n    Box(T v) : value(v) {}\n    void display() {\n        cout << value;\n    }\n};\nint main() {\n    Box<int> intBox(10);\n    Box<string> stringBox('Hello');\n    intBox.display();\n    stringBox.display();\n    return 0;\n}\n```"
        ]},
        
        {"topic": "STL (Standard Template Library)", 
         "theory": "C++ includes a collection of template classes and functions that implement algorithms and data structures like vectors, lists, maps, and more. STL is a powerful feature of C++ for efficient and reusable code.",
         "examples": [
            "Example 1: Using vectors",
            "```cpp\n#include <iostream>\n#include <vector>\nusing namespace std;\nint main() {\n    vector<int> nums = {1, 2, 3, 4, 5};\n    for (int num : nums) {\n        cout << num << ' ';\n    }\n    return 0;\n}\n```",
            "Example 2: Using maps",
            "```cpp\n#include <iostream>\n#include <map>\nusing namespace std;\nint main() {\n    map<string, int> age;\n    age['Alice'] = 25;\n    age['Bob'] = 30;\n    cout << age['Alice'];  // Output: 25\n    return 0;\n}\n```"
        ]}
    ]
},
        "SQL": {
    "Beginner": [
        {"topic": "Introduction to SQL", 
         "theory": "SQL (Structured Query Language) is a domain-specific language used for managing and manipulating relational databases. It allows you to query, update, and manage data stored in tables.",
         "examples": [
            "Example 1: Select all records from a table",
            "```sql\nSELECT * FROM Employees;\n```",
            "Example 2: Basic SELECT with a WHERE condition",
            "```sql\nSELECT name, age FROM Employees WHERE age > 30;\n```"
        ]},
        
        {"topic": "Creating and Modifying Tables", 
         "theory": "SQL allows you to create and modify tables to store data. The CREATE TABLE statement is used to define a table, and ALTER TABLE allows for adding or modifying columns.",
         "examples": [
            "Example 1: Create a table",
            "```sql\nCREATE TABLE Employees (\n    id INT PRIMARY KEY,\n    name VARCHAR(100),\n    age INT\n);\n```",
            "Example 2: Alter a table",
            "```sql\nALTER TABLE Employees ADD email VARCHAR(100);\n```"
        ]},
        
        {"topic": "Basic Data Retrieval", 
         "theory": "The SELECT statement is used to retrieve data from one or more tables. You can filter and sort the data using WHERE and ORDER BY clauses.",
         "examples": [
            "Example 1: Select specific columns",
            "```sql\nSELECT name, age FROM Employees;\n```",
            "Example 2: Select with sorting",
            "```sql\nSELECT name, age FROM Employees ORDER BY age DESC;\n```"
        ]}
    ],
    
    "Intermediate": [
        {"topic": "Joins", 
         "theory": "SQL joins allow you to combine rows from two or more tables based on a related column. Common types of joins are INNER JOIN, LEFT JOIN, RIGHT JOIN, and FULL JOIN.",
         "examples": [
            "Example 1: INNER JOIN",
            "```sql\nSELECT Employees.name, Departments.name\nFROM Employees\nINNER JOIN Departments ON Employees.dept_id = Departments.id;\n```",
            "Example 2: LEFT JOIN",
            "```sql\nSELECT Employees.name, Departments.name\nFROM Employees\nLEFT JOIN Departments ON Employees.dept_id = Departments.id;\n```"
        ]},
        
        {"topic": "Group By and Aggregate Functions", 
         "theory": "GROUP BY allows you to group rows that have the same values in specified columns. Aggregate functions like COUNT, AVG, MAX, and MIN can be used to perform calculations on each group.",
         "examples": [
            "Example 1: Using COUNT",
            "```sql\nSELECT dept_id, COUNT(*) FROM Employees GROUP BY dept_id;\n```",
            "Example 2: Using AVG",
            "```sql\nSELECT dept_id, AVG(age) FROM Employees GROUP BY dept_id;\n```"
         ]}
    ],

    "SQL": {
    "Advanced": [
        {"topic": "Subqueries", 
         "theory": "A subquery is a query within another query. It can be used in SELECT, INSERT, UPDATE, or DELETE statements. Subqueries are often used to retrieve data that will be used by the main query.",
         "examples": [
            "Example 1: Using subquery in SELECT",
            "```sql\nSELECT name, age FROM Employees WHERE dept_id = (SELECT id FROM Departments WHERE name = 'HR');\n```",
            "Example 2: Using subquery in WHERE",
            "```sql\nSELECT name, age FROM Employees WHERE age > (SELECT AVG(age) FROM Employees);\n```"
        ]},
        
        {"topic": "Indexes", 
         "theory": "Indexes are special data structures that improve the speed of data retrieval operations on a database table. They work by providing quick access to rows in the table based on the indexed columns.",
         "examples": [
            "Example 1: Creating an index",
            "```sql\nCREATE INDEX idx_employee_name ON Employees(name);\n```",
            "Example 2: Dropping an index",
            "```sql\nDROP INDEX idx_employee_name;\n```"
        ]},
        
        {"topic": "Transactions and ACID Properties", 
         "theory": "A transaction is a sequence of one or more SQL operations executed as a single unit of work. Transactions follow the ACID properties (Atomicity, Consistency, Isolation, Durability) to ensure data integrity.",
         "examples": [
            "Example 1: Starting a transaction",
            "```sql\nBEGIN TRANSACTION;\n```",
            "Example 2: Committing a transaction",
            "```sql\nCOMMIT;\n```",
            "Example 3: Rolling back a transaction",
            "```sql\nROLLBACK;\n```"
        ]},
        
        {"topic": "Views", 
         "theory": "A view is a virtual table based on the result of a SELECT query. It does not store data itself but provides a way to simplify complex queries and enhance data security by restricting access to specific columns or rows.",
         "examples": [
            "Example 1: Creating a view",
            "```sql\nCREATE VIEW EmployeeDetails AS\nSELECT name, age, department FROM Employees;\n```",
            "Example 2: Selecting from a view",
            "```sql\nSELECT * FROM EmployeeDetails;\n```",
            "Example 3: Dropping a view",
            "```sql\nDROP VIEW EmployeeDetails;\n```"
        ]},
        
        {"topic": "Stored Procedures and Triggers", 
         "theory": "Stored procedures are a set of SQL statements that can be executed as a single unit. Triggers are special types of stored procedures that are automatically executed or fired when certain events occur in the database.",
         "examples": [
            "Example 1: Creating a stored procedure",
            "```sql\nCREATE PROCEDURE GetEmployeeDetails()\nBEGIN\nSELECT * FROM Employees;\nEND;\n```",
            "Example 2: Executing a stored procedure",
            "```sql\nCALL GetEmployeeDetails();\n```",
            "Example 3: Creating a trigger",
            "```sql\nCREATE TRIGGER AfterEmployeeInsert\nAFTER INSERT ON Employees\nFOR EACH ROW\nBEGIN\n    INSERT INTO AuditLog(action, timestamp) VALUES('INSERT', NOW());\nEND;\n```"
        ]}
    ]
}
        }
    }
    
    # Get the list of topics for the selected subject and level
    topics = course_materials.get(selected_subject, {}).get(selected_level, [])
    
    # Initialize topic index in session state
    if 'topic_index' not in st.session_state:
        st.session_state.topic_index = 0
    
    # Display the current topic
    if topics:
        current_topic = topics[st.session_state.topic_index]
        st.subheader(current_topic["topic"])
        st.write("**Theory:**")
        st.write(current_topic["theory"])
        st.write("**Examples:**")
        for example in current_topic["examples"]:
            st.write(f"- {example}")
        
        # Navigation buttons
        col1, col2 = st.columns(2)
        with col1:
            if st.session_state.topic_index > 0:
                if st.button("Previous Topic"):
                    st.session_state.topic_index -= 1
                    st.rerun()
        with col2:
            if st.session_state.topic_index < len(topics) - 1:
                if st.button("Next Topic"):
                    st.session_state.topic_index += 1
                    st.rerun()
            else:
                if st.button("Finish Course"):
                    st.session_state.page = "Topic Mock Test"  # Direct to mock test after finishing course
                    st.rerun()
    else:
        st.warning("No course materials available for the selected subject and level.")

elif page == "Topic Mock Test":
    st.title("Mock Test for Selected Topics")
    
    # Define mock test questions for the selected topics
    topic_mock_questions = {
    "Python": {
        "Beginner": [
            ("What is a variable in Python?", ["A storage location", "A function", "A loop", "A class"], 0),
            ("Which function is used to print output?", ["print()", "echo()", "printf()", "display()"], 0),
            ("What is the result of 5 + 3 * 2?", ["16", "11", "10", "13"], 1),
            ("Which data type stores text?", ["int", "float", "str", "bool"], 2)
        ],
        "Intermediate": [
            ("Which keyword defines a function?", ["define", "func", "def", "function"], 2),
            ("How do you open a file in Python?", ["open('file.txt', 'r')", "read('file.txt')", "file.read('file.txt')", "open('file.txt') as file"], 0),
            ("Which statement handles exceptions?", ["try-except", "catch-throw", "do-while", "if-else"], 0),
            ("What happens when opening a non-existent file for reading?", ["An error occurs", "A new file is created", "Nothing happens", "It returns None"], 0)
        ],
        "Advanced": [
            ("Which is NOT an OOP principle?", ["Encapsulation", "Polymorphism", "Abstraction", "Recursion"], 3),
            ("Which keyword is used for inheritance?", ["inherits", "extends", "super", "class"], 2),
            ("Which module provides decorators?", ["functools", "decorators", "lambda", "utils"], 0),
            ("Which function imports a module dynamically?", ["import_module", "load_module", "importlib", "sys_import"], 0)
        ]
    },
    "Java": {
        "Beginner": [
            ("Which keyword defines a class?", ["class", "define", "public", "object"], 0),
            ("What is Java’s entry point?", ["main()", "start()", "run()", "execute()"], 0),
            ("Which data type stores a single character?", ["char", "string", "int", "boolean"], 0),
            ("What happens if you divide by zero?", ["An exception occurs", "Returns 0", "Prints Infinity", "Ignores the operation"], 0)
        ],
        "Intermediate": [
            ("How do you define a method?", ["def method()", "method()", "void method()", "function method()"], 2),
            ("Which class is used for file handling?", ["File", "FileReader", "FileWriter", "All of the above"], 3),
            ("Which keyword handles exceptions?", ["catch", "try", "throws", "exception"], 1),
            ("What happens when accessing an invalid array index?", ["ArrayIndexOutOfBoundsException", "NullPointerException", "IOException", "IndexError"], 0)
        ],
        "Advanced": [
            ("Which is NOT an OOP principle?", ["Encapsulation", "Polymorphism", "Abstraction", "Iteration"], 3),
            ("Which access modifier allows package visibility?", ["private", "protected", "default", "public"], 2),
            ("Which feature enables multiple implementations of an interface?", ["Encapsulation", "Abstraction", "Polymorphism", "Inheritance"], 2),
            ("What syntax is used for lambda expressions?", ["()->", "=>", "::", "lambda:"], 0)
        ]
    },
    "C++": {
        "Beginner": [
            ("What is C++ known as?", ["A scripting language", "An object-oriented language", "A markup language", "A database language"], 1),
            ("Which output function is used in C++?", ["print", "display", "cout", "write"], 2),
            ("Which type stores decimal numbers?", ["int", "char", "float", "bool"], 2),
            ("Which symbol ends a statement?", [".", ",", ";", "!"], 2)
        ],
        "Intermediate": [
            ("Which keyword defines a function?", ["def", "func", "void", "function"], 2),
            ("Which header file is for file handling?", ["<file>", "<iostream>", "<fstream>", "<string>"], 2),
            ("Which statement handles errors?", ["try-catch", "if-else", "switch-case", "throw-else"], 0),
            ("What does a function return if no return type is specified?", ["int", "void", "null", "undefined"], 1)
        ],
        "Advanced": [
            ("Which concept allows code reuse?", ["Encapsulation", "Inheritance", "Polymorphism", "Abstraction"], 1),
            ("Which keyword defines a template function?", ["function", "template", "generic", "define"], 1),
            ("Which STL container stores key-value pairs?", ["vector", "list", "map", "set"], 2),
            ("Which OOP principle is used in function overloading?", ["Encapsulation", "Polymorphism", "Abstraction", "Inheritance"], 1)
        ]
    },
    "SQL": {
        "Beginner": [
            ("What does SQL stand for?", ["Structured Query Language", "Sequential Query Language", "System Query Language", "Standard Query Language"], 0),
            ("Which command retrieves data?", ["INSERT", "SELECT", "DELETE", "UPDATE"], 1),
            ("Which clause filters results?", ["WHERE", "HAVING", "ORDER BY", "GROUP BY"], 0),
            ("Which command creates a table?", ["CREATE TABLE", "ADD TABLE", "MAKE TABLE", "DEFINE TABLE"], 0)
        ],
        "Intermediate": [
            ("Which statement joins tables?", ["COMBINE", "MERGE", "JOIN", "CONNECT"], 2),
            ("Which function counts rows?", ["SUM", "COUNT", "TOTAL", "NUMBER"], 1),
            ("Which function calculates average?", ["SUM", "MEAN", "AVG", "MEDIAN"], 2),
            ("Which JOIN returns only matching rows?", ["LEFT JOIN", "RIGHT JOIN", "INNER JOIN", "OUTER JOIN"], 2)
        ],
        "Advanced": [
            ("What is a subquery?", ["A query inside another query", "A query with no tables", "A stored procedure", "A temporary table"], 0),
            ("Which command creates an index?", ["CREATE INDEX", "ADD INDEX", "DEFINE INDEX", "MAKE INDEX"], 0),
            ("What does ACID stand for?", ["Atomicity, Consistency, Isolation, Durability", "Accuracy, Consistency, Integration, Durability", "Atomicity, Coherence, Integration, Dependability", "Availability, Coherence, Integrity, Durability"], 0),
            ("What is a stored procedure?", ["To store data", "To optimize indexes", "To execute pre-defined SQL statements", "To create temporary tables"], 2)
        ]
    }
}

     # Store topic_mock_questions in session state
    st.session_state.topic_mock_questions = topic_mock_questions
    
    if 'topic_question_index' not in st.session_state:
        st.session_state.topic_question_index = 0
    if 'topic_answers' not in st.session_state:
        st.session_state.topic_answers = {}
    if 'topic_exam_started' not in st.session_state:
        st.session_state.topic_exam_started = False
    
    if not st.session_state.topic_exam_started:
        # Allow user to select topic and difficulty
        selected_topic = st.selectbox("Select Topic", list(topic_mock_questions.keys()))
        selected_difficulty = st.selectbox("Select Difficulty", list(topic_mock_questions[selected_topic].keys()))
        
        if st.button("Start Mock Test"):
            st.session_state.topic_exam_started = True
            st.session_state.selected_topic = selected_topic
            st.session_state.selected_difficulty = selected_difficulty
            st.rerun()
    else:
        # Fetch selected topic and difficulty from session state
        selected_topic = st.session_state.selected_topic
        selected_difficulty = st.session_state.selected_difficulty
        
        # Fetch questions for the selected topic and difficulty
        questions = st.session_state.topic_mock_questions.get(selected_topic, {}).get(selected_difficulty, [])
        total_topic_mcq = len(questions)
        
        if st.session_state.topic_question_index < total_topic_mcq:
            question, options, correct_index = questions[st.session_state.topic_question_index]
            st.write(f"Question {st.session_state.topic_question_index + 1}: {question}")
            choice = st.radio("Choose one:", options, key=f"topic_mcq_{st.session_state.topic_question_index}")
            
            if st.button("Next Question"):
                st.session_state.topic_answers[st.session_state.topic_question_index] = choice
                st.session_state.topic_question_index += 1
                st.rerun()
        else:
            if st.button("Submit Mock Test"):
                st.success("Mock Test Submitted! Check results.")
                st.session_state.page = "Topic Results"
                st.session_state.topic_question_index = 0
                st.rerun()


elif page == "Topic Results":
    st.title("Mock Test Results for Selected Topics")
    
    # Retrieve topic_mock_questions and selected topic/difficulty from session state
    topic_mock_questions = st.session_state.topic_mock_questions
    selected_topic = st.session_state.selected_topic
    selected_difficulty = st.session_state.selected_difficulty
    
    # Fetch questions for the selected topic and difficulty
    questions = topic_mock_questions.get(selected_topic, {}).get(selected_difficulty, [])
    
    # Calculate the score
    total_topic_questions = len(st.session_state.topic_answers)
    correct_topic_answers = 0
    
    for i in range(total_topic_questions):
        user_answer = st.session_state.topic_answers.get(i)
        if user_answer is not None:
            question, options, correct_index = questions[i]
            if user_answer == options[correct_index]:
                correct_topic_answers += 1
    
    score = (correct_topic_answers / total_topic_questions) * 100 if total_topic_questions > 0 else 0
    
    # Display the score
    st.write(f"Your score: {score:.2f}%")
    
    # Provide feedback and options based on the score
    if score >= 70:
        st.success("Congratulations! You have passed the mock test with a score of 70% or above.")
        
        # Determine the next level
        levels = ["Beginner", "Intermediate", "Advanced"]
        current_level_index = levels.index(selected_difficulty)
        
        if current_level_index < len(levels) - 1:
            # Redirect to the next difficulty level of the same course
            next_level = levels[current_level_index + 1]
            if st.button(f"Continue to {next_level} Level"):
                # Update the selected difficulty to the next level
                st.session_state.selected_difficulty = next_level
                # Redirect to Course Materials for the next level
                st.session_state.page = "Course Materials"
                st.rerun()
        else:
            # If the user passes the Advanced level, redirect to Coding Questions
            st.success("You have completed all levels! Now, let's solve some coding questions.")
            if st.button("Go to Coding Questions"):
                st.session_state.page = "Coding Questions"
                st.rerun()
    else:
        st.warning("Your score is below 70%. It would be appreciated if you review the topics again.")
        
        # Options to retake the course or mock test
        col1, col2 = st.columns(2)
        with col1:
            if st.button("Retake Course"):
                st.session_state.page = "Course Materials"
                st.session_state.topic_index = 0
                st.rerun()
        with col2:
            if st.button("Retake Mock Test"):
                st.session_state.page = "Topic Mock Test"
                st.session_state.topic_exam_started = False
                st.session_state.topic_question_index = 0
                st.session_state.topic_answers = {}
                st.rerun()
    
    if st.button("Back to Course Materials"):
        st.session_state.page = "Course Materials"
        st.rerun()
