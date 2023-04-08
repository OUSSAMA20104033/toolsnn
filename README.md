import os
import subprocess
import requests
import getpass

def install_package(package_name):
    print(f"Installing {package_name}...")
    os.system(f"pkg install {package_name} -y")

def check_package(package_name):
    try:
        subprocess.check_output([package_name, "--version"])
        print(f"{package_name} is already installed")
        return True
    except subprocess.CalledProcessError:
        print(f"{package_name} is not installed")
        return False

def check_and_install(package_name):
    if not check_package(package_name):
        install_package(package_name)

def scan_network():
    print("Scanning network...")
    os.system("nmap -sn 192.168.1.0/24")

def get_public_ip():
    print("Getting public IP address...")
    response = requests.get("https://api.ipify.org")
    print(f"Public IP address: {response.text}")

def main():
    print("Starting network tool...")
    username = getpass.getuser()
    print(f"Welcome {username}!")
    check_and_install("nmap")
    check_and_install("whois")
    get_public_ip()
    scan_network()

if __name__ == "__main__":
    main()
