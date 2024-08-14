# HackerBay-club
import socket

def scan_ports(host, ports):
    open_ports = []
    for port in ports:
        with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
            s.settimeout(1)  # Timeout for the connection attempt
            result = s.connect_ex((host, port))  # Try to connect to the port
            if result == 0:  # Connection was successful
                open_ports.append(port)
    return open_ports

if __name__ == "__main__":
    target_host = input("Enter the target host (e.g., 192.168.1.1 or example.com): ")
    ports_to_scan = list(range(1, 1025))  # Scan ports from 1 to 1024

    print(f"Scanning ports on {target_host}...")
    open_ports = scan_ports(target_host, ports_to_scan)
    
    if open_ports:
        print(f"Open ports on {target_host}: {', '.join(map(str, open_ports))}")
    else:
        print(f"No open ports found on {target_host}.")
