
# Scheduling_Algorithms_Interface

## Overview

**Scheduling_Algorithms_Interface** is a graphical simulation tool that lets users explore and compare classic CPU scheduling algorithms through an interactive visual interface. Developed as a project for the **IN422** university course, this application provides a clear visualization of how different scheduling strategies operate and performs side-by-side comparisons of their performance. Users can input custom task parameters and watch in real-time as the scheduler handles these tasks, all within a Pygame-driven GUI. The project’s objective is to allow users to **simulate, visualize, and compare** five fundamental scheduling algorithms (**Round Robin (RR), Rate Monotonic (RM), Earliest Deadline First (EDF), First-Come-First-Served (FCFS), and Shortest Job Next (SJN)**) in order to understand their behavior and performance differences. This README provides an overview of the project, its features, and instructions on how to install and use the application effectively.

## Features

- **Multiple Scheduling Algorithms:** Includes **five scheduling algorithms** – *RR, RM, EDF, FCFS*, and *SJN*. Each algorithm is implemented according to its scheduling rules, allowing users to simulate how tasks are ordered and executed under each strategy. Real-time algorithms like RM and EDF consider periodic tasks and deadlines, whereas RR, FCFS, and SJN handle general scheduling scenarios. This variety gives users a broad perspective on preemptive vs. non-preemptive and real-time vs. batch scheduling approaches.

- **Interactive Pygame GUI:** Offers a user-friendly **graphical interface** built with Pygame. The interface provides forms to input task parameters, buttons to add or remove tasks, and options to select and run each scheduling algorithm. Visual representations of the CPU execution timeline are displayed for each algorithm, with color-coded bars indicating when each task starts and finishes on the CPU. The GUI updates in real-time, and includes navigation controls (e.g., “Help”, “Next”, “Previous”, and “Back/Escape” to return to menus) to guide the user through the simulation steps.

- **Visualization of Scheduling Timelines:** For each algorithm run, the application draws an **execution timeline** that shows the sequence of task execution on a simulated CPU timeline. Task names are labeled on colored time blocks, and important time markers are shown. This helps users visually compare how different algorithms schedule the same set of tasks (for example, how a Round Robin time-slices tasks versus how SJN picks the shortest job first).

- **Performance Metrics Display:** After simulating an algorithm, the tool calculates key **performance metrics** for the schedule and displays them on the result screen. These metrics include each task’s *Completion Time (CT), Turnaround Time (TAT),* and *Waiting Time (WT)*, as well as the **average turnaround time** and **average waiting time** across all tasks. This quantitative feedback lets users evaluate efficiency: e.g., SJN typically yields a lower average waiting time, while Round Robin might have higher overhead due to context switching. For the real-time algorithms (RM and EDF), the simulation also evaluates *CPU utilization* and checks schedulability (ensuring the task set can be scheduled within deadlines), providing insight into feasibility under given task loads.

- **Algorithm Comparison Mode:** The application includes a dedicated **comparison feature** where users can compare algorithms based on various criteria and performance measures. In the comparison screen, users select a criterion from a dropdown (such as *Average Waiting Time, CPU Utilization, Fairness, Preemption,* etc.), and the interface will highlight which scheduling algorithm performs best for that chosen criterion. This feature helps in understanding the trade-offs: for example, one algorithm may minimize waiting time while another maximizes fairness or CPU throughput.

- **Configurable Round Robin Quantum:** Round Robin scheduling in the simulator allows the user to configure the time **quantum slice** (time slot length) via an input box. This quantum can be set between 1 and 20 units. Users can experiment with different quantum sizes to see how it affects scheduling behavior (e.g., smaller quanta yield more frequent context switches, which can be observed in the timeline visualization).

- **Threaded Simulation Execution:** To ensure a smooth and responsive user experience, the simulation of scheduling algorithms runs in a separate background thread. This allows the graphical interface to remain interactive during the computation phase. Users can cancel or navigate without freezing the application, which simulates the concurrent behavior of real operating systems handling multiple processes.

- **Help and Guidance:** The interface comes with built-in **help screens** to guide new users. A “Help” button in the main menu opens a step-by-step tutorial (with images) on how to use the application – from entering tasks to interpreting the output. Additionally, a “Help Algorithms” section (accessible from the algorithm selection screen) provides brief explanations of each scheduling algorithm and when to use them. These resources make the tool self-contained and educational for those new to scheduling concepts.

## Installation

**Prerequisites:** Ensure you have **Python 3.x** installed on your system. This project is developed in Python and has been tested with a modern version of Python 3. You will also need the **Pygame** library, which the application uses for all graphics and interface components.

**Steps:**
1.	**Clone or Download the Repository:** Download the project files to your local machine. The key files are `main.py`, `algorithms.py`, `init.py`, and an `Images/` directory (containing help images), along with this README.

2.	**Install Pygame:** If not already installed, install Pygame using pip. Run the following command in your terminal or command prompt: `pip install pygame`
This will install Pygame (a cross-platform set of Python modules designed for writing video games and multimedia applications).

3. **Verify Other Dependencies:** The project uses only standard Python libraries beyond Pygame (such as `collections.dequ`, `functools.reduce`, and `math` for computations). These come bundled with Python, so no additional installs should be necessary.

4.	**Run the Application:** Navigate to the project directory in your terminal. Launch the app by running the main Python script: `python main.py`
Ensure that you run this in an environment where a display is available (the Pygame window will open to show the GUI, so on a server you might need a display or X11 forwarding).

If everything is set up correctly, a window titled **“Scheduling Algorithms”** will appear, presenting the main menu of the simulator.

## Usage Guide

Once the application is running, you can interact with the GUI to simulate scheduling algorithms. Here’s a step-by-step guide to using the tool:

1.	**Main Menu – Input Tasks:** Upon launch, the main menu is displayed with an empty list of tasks and input fields. Each task consists of five fields:
- **Task Name:** An identifier for the task (string).
- **Arrival Time:** The time at which the task arrives (integer, in CPU time units).
- **Execution Time (Burst)**: The CPU time required by the task to complete (integer).
- **Period:** For periodic tasks (used in RM/EDF), the interval before the task repeats. For one-time tasks, this can be a large number or equal to its deadline.
- **Deadline:** For deadline-based scheduling (EDF), the relative deadline by which the task should finish. If tasks have no specific deadline, this can be set equal to their period or a large value to simulate no tight deadline.

Begin by entering values for at least one task (in the range 1 to 20). Click into each field and type the desired number or text. By default, one row of task input is shown. Use the **“Add”** button to add more task rows (up to a maximum of 10 tasks). Use the **“Delete”** button to remove the last task row if needed. All fields are required – the app will show an error message if any field is left blank or zero where not allowed (execution time, period, and deadline must be >= 1).

There is also a field labeled **“Quantum”** at the top-right of the main menu. This is only relevant for the Round Robin algorithm. Enter the time-slice quantum (in the range 1 to 20). If you enter an invalid value (like 0 or too high), the program will warn you and reset it to a default safe value.

2.	**Launch Simulation:** After entering your task set (and setting the quantum if using RR), click the **“Launch”** button. The application will validate the inputs. If everything is okay, it will proceed to the algorithm selection screen. (If there are issues – such as missing values or disallowed zeros – an error message will be displayed on the screen, and you should fix the inputs before proceeding.)

3.	**Select Scheduling Algorithm:** In the **algorithm selection screen**, you will see a list of buttons corresponding to the five scheduling algorithms:
- *Round Robin (RR)*
- *Rate Monotonic (RM)*
- *Earliest Deadline First (EDF)*
- *First-Come-First-Serve (FCFS)*
- *Shortest Job Next (SJN)*

Click on the algorithm you want to simulate. For example, clicking **“Round Robin (RR)”** will run the Round Robin scheduling simulation on the tasks you provided.

Additionally, there are two special buttons:
- **“Help Algorithms”** – clicking this opens a help screen that provides descriptions and background on each algorithm (useful if you need a refresher on how they work or what their intended use-cases are).

- **“Algorithms Comparison”** – clicking this opens the comparison mode (described in step 5 below), where you can compare algorithms on different performance criteria.

You can return to the main menu at any time by pressing the **Escape (Esc)** key.

4.	Viewing Simulation Results: Once you select an algorithm, the simulator will display the results screen for that algorithm. This screen includes:
- An **execution timeline** showing each task’s execution on a timeline (the horizontal axis is time). Each scheduled portion of a task is drawn as a colored bar. The task name is labeled on each bar, with its start time indicated below. If the task finishes, the end time is labeled as well. For algorithms that involve preemption (like RR, EDF, RM), you will see multiple bars for the same task if it gets interrupted and resumed later.
- A **metrics panel** below the timeline, listing performance metrics. For each task, you’ll see its Completion Time (the time the task finished), Turnaround Time (finish time minus arrival time), and Waiting Time (turnaround minus execution time). These are displayed in a list for all tasks. Below that, the **average turnaround time** and **average waiting time** for all tasks are shown, providing an aggregate measure of performance for that algorithm’s schedule. In case of EDF and RM, you might also see CPU utilization and a note on schedulability (e.g., if the task set could be scheduled within deadlines or not).
- A prompt “*Esc to return*” at the bottom, indicating you can press Escape to go back to the algorithm selection menu.

This visualization and data allow you to analyze how the chosen algorithm performed. For example, you can observe if shorter tasks indeed finished earlier under SJN, or how RR cycled through tasks each quantum. You can also note differences in waiting times: e.g., FCFS may cause long waits for tasks arriving later if an early task has a long burst, whereas RR can alleviate that at the cost of more context switches.

When you have reviewed the results, press **Esc** to return to the algorithm selection screen. From there, you can choose another algorithm to simulate on the same task set (allowing direct comparisons by trying different algorithms one by one).

5.	**Comparison Mode (Optional):** If you click **“Algorithms Comparison”** from the selection screen, you will enter the comparison mode. At the top of this screen is a **dropdown menu** listing various comparison criteria (e.g., *Preemption, Task Type, Priority, Fairness, Average Waiting Time, CPU Utilization,* etc.). Select a criterion that you’re interested in. The application will then display which algorithm is considered best for that criterion, and in some cases, it may list other algorithms for reference. For instance, if you select **“Average Waiting Time”**, the comparison might highlight **SJN as the best** (since Shortest Job Next minimizes waiting time on average) and mention other algorithms for context. If you select **“CPU Utilization”**, it might show **EDF as best** (as EDF can schedule tasks up to 100% CPU utilization in ideal conditions) with others listed for comparison. This feature encapsulates general wisdom and results from scheduling theory to help users decide which algorithm might be optimal under certain conditions or goals.

The comparison mode does not run new simulations but provides general comparative insights. It’s a useful summary tool, especially for educational purposes, to reinforce why one might choose one scheduling algorithm over another in a given scenario. After viewing the comparisons, you can press **Esc** to return to the algorithm selection screen.

6.	**Help Sections:** At any point in the main menu or other screens, you can access help:
- Main menu **“Help”** button: Shows a guided tour on how to use the application, with images illustrating each step from task entry to reading the results.
- **“Help Algorithms”** in selection menu: Shows informational slides on each algorithm (their definitions, how they work, etc.).

Navigate through help screens using the **“Next”** and **“Previous”** buttons. Press Esc to exit any help screen and return to the previous menu.

7.	**Exit:** To close the application, you can either press the window’s close button or hit the **Esc** key until you return to the main menu and then close, or simply close the window. The application will shut down the Pygame window and exit.

By following these steps, you can experiment with different scheduling strategies for various task sets. This tool is especially useful for students and enthusiasts to observe how scheduling algorithms differ in practice, under a unified interface.

## Technologies Used
- **Python 3.x:** The core language used for development. The scheduling logic (task sorting, queue handling, time progression, etc.) is implemented in Python, taking advantage of data structures like lists, dictionaries, and deques for managing tasks and schedule queues.
- **Pygame:** Used to create the graphical user interface and visualizations. All drawing of text, buttons, and timeline graphics are done using Pygame’s rendering functions. Pygame handles the main loop, event handling (keyboard/mouse input), and screen updates at a steady frame rate, which is crucial for the interactive experience.
- **Standard Library Modules:** The project uses Python’s standard libraries such as collections (for an efficient queue via deque), functools (for utilities like reduce in calculations), and math (for computations like greatest common divisor and ceiling, used in real-time scheduling math). These helped implement algorithm-specific logic (e.g., computing hyper-period for EDF/RM schedules or ensuring numerical calculations for utilization and response time).
- **Threading (Python threading module):** To simulate concurrent task execution and to maintain GUI responsiveness, the project uses Python's built-in threading module. The scheduling simulation runs on a background thread, ensuring the main thread remains free for rendering and event handling. This design mirrors the real-world behavior of multitasking systems and improves the user experience during simulations.

Overall, the combination of **Python’s ease of writing algorithms** and **Pygame’s visualization capabilities** made it possible to create an interactive educational tool for scheduling algorithms.

## Contributors
This project was designed and implemented by a team of three students as part of the IN422 course:
- **Laura Filet** 
- **Chloé Tonso** 
- **Caroline Rodrigues**

Each contributor played a significant role in bringing the project to completion. The collaboration involved designing the interface, coding the scheduling logic, ensuring correctness of simulations, and creating helpful documentation and guides (like the help screens). 

## License
This project is released **without an explicit license**. It is an academic course project, and no specific open-source license has been provided. As such, the code is intended primarily for educational use. If you wish to use or modify this code, please acknowledge the authors. In absence of a license, all rights are reserved by the original contributors.


