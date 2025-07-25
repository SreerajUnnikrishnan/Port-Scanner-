# Port-Scanner-
import socket
from datetime import datetime

# Target IP (change to your test target)
target = input("Enter the IP address to scan: ")
# Port range
start_port = int(input("Enter start port: "))
end_port = int(input("Enter end port: "))

print(f"\nStarting scan on host: {target}")
start_time = datetime.now()

try:
    for port in range(start_port, end_port + 1):
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        socket.setdefaulttimeout(1)  # 1-second timeout
        result = s.connect_ex((target, port))  # 0 means open
        if result == 0:
            print(f"[+] Port {port} is open")
        s.close()

except KeyboardInterrupt:
    print("\nExiting...")
except socket.gaierror:
    print("Hostname could not be resolved.")
except socket.error:
    print("Could not connect to server.")

end_time = datetime.now()
print(f"\nScan completed in: {end_time - start_time}")
