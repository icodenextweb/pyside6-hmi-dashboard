# pyside6-hmi-dashboard
A high-performance Human Machine Interface (HMI) built with PySide6 and Python, featuring asynchronous state management.


#Note :-
The source code for this project is strictly confidential under a Non-Disclosure Agreement (NDA) for a private client. 
This repository serves as an architectural overview and case study of the system I developed.


#Tech Stack & Tools:-
*Core Language: Python 3
*UI Framework:  PySide6 
*Data Processing: openpyxl, datetime, CSV data logging
*Hardware Integration: Serial connections `pyserial` concept via `connection.py`
*Architecture: Multi-threading `QThread`, Asynchronous execution, Signal event handling
*Environment: Virtual Environments `venv`, Windows Taskbar integration `ctypes`


#System Interface:-
1.Industrial HMI Dashboard for Steam Sterilizer Application showing real-time Chamber and Jacket metrics:-
<img width="1920" height="1020" alt="hmi screen" src="https://github.com/user-attachments/assets/364a242f-f958-44d2-a3f3-27ab941e1578" />

2.Hardware Connection Module managing dynamic COM ports and Serial Baud Rates:-
<img width="1920" height="1020" alt="hmi_connection" src="https://github.com/user-attachments/assets/35c3e271-23b7-45cd-8bb4-67b6d4d6ae31" />


#Engineering Challenges Solved:- 
1. Eliminating UI Freezing
*The Problem:  Running heavy tasks—like loading large Excel files and waiting for serial data from hardware on the main thread caused the application window to freeze.
*The Solution: Architected a robust multi-threaded system.
               I isolated the Excel parsing logic into a dedicated `QThread` and decoupled the hardware communication into a separate `PLCWorker` thread.
               The main thread is strictly reserved for UI rendering.

2. Safe State Management & Cross Thread Communication:- 
*The Problem:  Background threads cannot directly update GUI elements without causing fatal crashes.
*The Solution: Implemented PySide6's strict Signal and Slot mechanism.
               For example, when the `QThread` finishes parsing operator names, it emits a signal `Finished Reading` carrying the payload,
               which safely triggers a slot on the main thread to update the UI.

3. Hardware/Software Integration & Resilience:-
Built a resilient serial connection pipeline that monitors active COM ports dynamically using a `QTimer`.
The system automatically handles hardware disconnections by pausing the session, safely halting background workers, and cleanly resuming once the hardware port is re-established.

#My Role and Responsibilities:- 
As the primary developer, I engineered the end-to-end architecture. 
I designed the threading model to prevent UI locks, integrated third-party libraries like `openpyxl` for data management, 
managed hardware connections, and successfully delivered a highly responsive, production-ready desktop application.

