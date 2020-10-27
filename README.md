# WagoOpcUaVisu
Trying to control my Wago PFC100 with a web application which connects to the PLC via OPC UA.
This is a hobby project of mine and a work in progress.

# First step: Test out OPC UA connection

Steps in eCockpit!:
- Assuming you have a running program on it which compiles and has some variables in it.
- Disconnect from the running PLC
- Right click on Application (PFC100)
- Click on Symbol Configuration
- Select "Support OPC UA Features"
- In the tab "Symbol Configuration" choose some IOs you want to manipulate via OPC UA 
- Install [this](https://github.com/FreeOpcUa/python-opcua) via `pip install opcua`
- Get the IP address of your PLC
- Test if you can connect to your PLC via OPC UA with this script (slightly modified version of [this](https://github.com/FreeOpcUa/python-opcua/blob/master/examples/client-minimal.py))

    ```python
    import sys
    sys.path.insert(0, "..")


    from opcua import Client


    if __name__ == "__main__":

    client = Client("opc.tcp://192.168.99.99:4840/")
    # client = Client("opc.tcp://admin@localhost:4840/freeopcua/server/") #connect using a user
    try:
        client.connect()

        # Client has a few methods to get proxy to UA nodes that should always be in address space such as Root or Objects
        root = client.get_root_node()
        print("Objects node is: ", root)

        # Node objects have methods to read and write node attributes as well as browse or populate address space
        print("Children of root are: ", root.get_children())


    finally:
        client.disconnect()
    ```

- Now you should see something like this `Children of root are:  [Node(TwoByteNodeId(i=87)), Node(TwoByteNodeId(i=86)), Node(TwoByteNodeId(i=85))]` as output
- This is very cryptic and you don´t know which node is which
- To solve this, download the program UAExpert from Unified Automation
- Now connect to your OPC UA server with the same IP + port combination you used in the python example
- On the left hand side of the program in the Address Space window, select the address space including the word CODESYSSPV3...
- Go down the tree: Root/Objects/DeviceSet/WAGO 750-8100.../Resources/Application/GlobalVars/IoConfig_Globals_Mapping
- Here you should see the formerly in eCockpit! selected IOs

More coming soon 
