# Description

Go implementation of yubikey server to be able to run your own server on network who can't have access to the official servers.

Store all information inside a sqlite database, need to create other connectors for different backend

I followed the [yubikey protocol in version 2.0](https://code.google.com/p/yubikey-val-server-php/wiki/ValidationProtocolV20) to implement this server

# Usage

    // to build the server
    $go build 
    
    // will add a new application and display the id and key
    $./yubikey-server -app "NameOfYourApp"
    
    // will add a new key in the system
    $./yubikey-server -name "YourName" -pub "publicKey" -secret "AESSecret"
    
    // will revoke/delete a key 
    $./yubikey-server -delete "YourName" 
    
    // will start the server on the default port 3000
    $./yubikey-server -s
    
# How to query the server
Get http call:

    http://<server ip>:<server port>/wsapi/2.0/verify?otp=<your otp>&id=<app id>&nonce=test42

Will return: 

    nonce=test42
    opt=vvcfvelvtdfvtvviihlihlvgnbhnffbgjhdevrfckbfi
    status=OK
    t=2015-01-03T02:11:05+04:00
    h=Vx8RgAAtjypv504iSPbT5nYCt3U=

otp is the one time password generated by your key and app id the the id returned by the server when you created a new application with the "-app <name>" argument
