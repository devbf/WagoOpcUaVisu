# WagoOpcUaVisu
Trying to control my Wago PFC100 with a web application which connects to the PLC via OPC UA.
This is a hobby project of mine and a work in progress.

# First step: Test out OPC UA connection

Steps in eCockpit!:
1) Assuming you have a running program on it which compiles and has some variables in it.
2) Disconnect from the running PLC
3) Right click on Application (PFC100)
4) Click on Symbol Configuration
5) Select "Support OPC UA Features"
6) Install [this](https://github.com/FreeOpcUa/python-opcua) via `pip install opcua`
7) Get the IP address of your PLC
8) Test if you can connect to your PLC via OPC UA with this script (slightly modified version of [this](https://github.com/FreeOpcUa/python-opcua/blob/master/examples/client-minimal.py)

More coming soon 
