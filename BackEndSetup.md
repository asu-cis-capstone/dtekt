<h1>Launching AWS Instance</h1>
<ol type="1">
    <li value="1">Create account</li>
    <li>Click EC2</li>
    <li>Launch instance</li>
    <li>Select Ubuntu 14.04</li>
    <li>Select first tier</li>
    <li>Configure network</li>
    <li>Add storage</li>
    <li>Name the instance</li>
    <li>Create a security group with only your IP (for now)</li>
    <li>Download security key</li>
</ol>

<h1>SSHing into AWS</h1>
<ol type="1">
    <li value="1">Run "chmod 400 [name of .pem file]"</li>
    <li>Run "ssh -i [name of .pem file] ubuntu@[name of AWS instance]"</li>
</ol>

<h1>Installing Node and testing</h1>
<ol type="1">
    ```shell
    sudo apt-get install git
    git clone https://github.com/heroku/node-js-sample.git
    cd node-js-sample/
    sudo add-apt-repository ppa:chris-lea/node.js
    sudo apt-get update
    sudo apt-get install nodejs
    npm install
    npm start
    ```
    <li>Edit index.js to use port 8080 instead of 5000</li>
</ol>

<h1>Configure network</h1>
<ol type="1">
    <li value="1">"sudo vim /etc/sysctl.conf" and uncomment "net.ipv4.ip_forward"</li>
    <li>sudo sysctl -p /etc/sysctl.conf</li>
    <li>cat /proc/sys/net/ipv4/ip_forward</li>
    <li>sudo iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080</li>
    <li>sudo iptables -A INPUT -p tcp -m tcp --sport 80 -j ACCEPT</li>
    <li>sudo iptables -A OUTPUT -p tcp -m tcp --dport 80 -j ACCEPT</li>
    <li>npm start</li>
</ol>
<h2>In AWS:</h2>
<ol type="1">
    <li value="8">Click on the security group you created that is listed in the instance</li>
    <li>Click on the "inbound" tab</li>
    <li>Click "edit"</li>
    <li>Click "Add Rule"</li>
    <li>Type: HTTP and Source: Anywhere</li>
    <li>Save</li>
</ol>