# Helm Chart for tftpd

This is an example Helm chart for tftpd, to demonstrate how to run a UDP
service behind a LoadBalancer Service on minikube

## Instructions

Install this chart:

    $ helm upgrade --install tftp ~/path/to/this/chart/

Wait until it is ready:

    $ helm status tftp

Start tunnel to minikube LoadBalancers:

    $ minikube tunnel

In another terminal, we can note the LoadBalancer IP:

    $ kubectl get svc

Now we can use the `tftp` client to retrieve a file:

    $ tftp $LOADBALANCERIP
    tftp> verbose
    Verbose mode on.
    tftp> trace
    Packet tracing on.
    tftp> binary
    mode set to octet
    tftp> get file1.txt
    getting from 10.104.126.213:file1.txt to file1.txt [octet]
    sent RRQ <file=file1.txt, mode=octet>
    received DATA <block=1, 31 bytes>
    Received 31 bytes in 0.0 seconds [60783 bit/s]
    tftp> quit

And make sure that the file has our expected contents:

    $ cat file1.txt
    contents of file1.txt go here!

## License

This project is licensed under the MIT License. Please see the
[LICENSE](LICENSE) file for details.
