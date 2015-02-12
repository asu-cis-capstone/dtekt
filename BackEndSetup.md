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
<h3>Run:</h3>

    chmod 400 [name of .pem file]
    ssh -i [name of .pem file] ubuntu@[name of AWS instance]

<h1>Installing Node and testing</h1>

    sudo apt-get install git
    git clone https://github.com/heroku/node-js-sample.git
    cd node-js-sample/
    sudo add-apt-repository ppa:chris-lea/node.js
    sudo apt-get update
    sudo apt-get install nodejs
    npm install
    npm start
    
<h3>Edit index.js to use port 8080 instead of 5000</h3>
    
    vim index.js
    
<h4>change:</h4>

    app.set('port', (process.env.PORT || 5000))
    
<h4>to:</h4>

    app.set('port', (process.env.PORT || 8080))

<h1>Configure network</h1>

    sudo vim /etc/sysctl.conf" and uncomment "net.ipv4.ip_forward
    sudo sysctl -p /etc/sysctl.conf
    cat /proc/sys/net/ipv4/ip_forward
    sudo iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080
    sudo iptables -A INPUT -p tcp -m tcp --sport 80 -j ACCEPT
    sudo iptables -A OUTPUT -p tcp -m tcp --dport 80 -j ACCEPT
    npm start
    
<h3>In AWS:</h3>
<ol type="1">
    <li value="1">Click on the security group you created that is listed in the instance</li>
    <li>Click on the "inbound" tab</li>
    <li>Click "edit"</li>
    <li>Click "Add Rule"</li>
    <li>Type: HTTP and Source: Anywhere</li>
    <li>Save</li>
</ol>

<h1> Installing Xamarin </h1>
<ol type="1">
    <li value="1">Navigate to Xamarin's webpage (http://developer.xamarin.com/) </li>
    <li>Under the "pricing" tab, scroll down to the FAQ and click the link for student pricing</li>
    <li>Fill in the required info and await an email where you will need to show proof of your student status</li>
    <li>Download and install Xamarin when confirmation email is received</li>
</ol>

<h2>Linking Xamarin and Visual Studio</h2>
    refer to documentation at the following URL:
    http://developer.xamarin.com/guides/cross-platform/getting_started/visual_studio_with_xamarin/cross_platform_visual_studi     o_project_setup_walkthrough/
