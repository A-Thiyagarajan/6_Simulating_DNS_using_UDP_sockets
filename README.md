# 6_Simulating_DNS_using_UDP_sockets
## AIM: 
The aim of simulating DNS using UDP sockets is to create a basic DNS server that can receive DNS queries over UDP and respond with the appropriate IP address for a given domain. In this simulation, we're simplifying DNS functionality, focusing on basic domain-to-IP mapping and handling simple queries.
## ALGORITHM 
1.Initialize DNS Server:
<BR>
Create a UDP socket to handle communication.
Bind the socket to a specific IP address and port to listen for incoming DNS queries.
<BR>
2.Define DNS Server Configuration:
<BR>
Set the DNS server IP address and port.
Prepare a mapping of domain names to corresponding IP addresses.
<BR>
3.Listen for DNS Queries:
<BR>
Enter a loop to continuously listen for incoming UDP messages.
Receive DNS Query:
When a DNS query is received, extract the domain name from the received data.
<BR>
4.Check Domain-to-IP Mapping:
Check if the received domain name exists in the predefined mapping.
If it does, retrieve the corresponding IP address.
If it doesn't, prepare an error response.
<BR>
5.Send DNS Response:
<BR>
If the domain is found, send the IP address back to the client.
If the domain is not found, send an error response.
<BR>
6.Handle Multiple Requests:
<BR>
The server remains in the listening state to handle multiple DNS queries.
Close the Server:
Optionally, include a mechanism to gracefully close the server when needed.
<BR>
## PROGRAM
### CLIENT:
```
import socket

#DNS records mapping domain names to IP addresses

DNS_DATABASE = {
    "example.com": "192.0.2.1",
    "google.com": "8.8.8.8",
    "facebook.com": "69.63.176.13",
    #Add more records as needed
}

def handle_dns_query(data):
    domain = data.decode().strip()
    if domain in DNS_DATABASE:
        return DNS_DATABASE [domain]
    else:
        return "Domain not found"

def main():
    #Creating a UDP socket 
    server_socket = socket.socket (socket.AF_INET, socket.SOCK_DGRAM)
    #Bind the socket to localhost and a specific port 
    server_address = ('localhost', 9999) 
    server_socket.bind(server_address)

    print("DNS server is running...")
    while True:
        #Receive data from the client
        data, client_address = server_socket.recvfrom(1024) 
        print (f"Received DNS query from (client_address)")

        #Handle DNS query and get the response 
        response = handle_dns_query(data)

        #Send the response back to the client 
        server_socket.sendto(response.encode(), client_address)

main()
```



### SERVER:
```
import socket

def main():
    # Creating a UDP socket
    client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

    # Server address and port 
    server_address = ('localhost', 9999)

    # DNS query
    query = "google.com"

    # Send the DNS query to the server 
    client_socket.sendto (query.encode(), server_address)

    #Receive the response from the server
    response, = client_socket.recvfrom(1024)
    print (f"Response from server: {response.decode()}")

main ()
```


## OUPUT
### CLIENT:

![324246523-538a9190-e1ae-4780-8bca-2b87f6ece668](https://github.com/A-Thiyagarajan/6_Simulating_DNS_using_UDP_sockets/assets/118707693/262a64f0-743c-491f-aac4-f9d011ac7ad5)

### SERVER: 
![324246528-1bf6774e-3912-422c-90f8-8d1b808a33ae](https://github.com/A-Thiyagarajan/6_Simulating_DNS_using_UDP_sockets/assets/118707693/e3f20971-18c3-4443-a74b-bcb646005820)

## RESULT
Thus the Experiment implemented sucessfully
